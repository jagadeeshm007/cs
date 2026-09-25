---
tags: [internals, docker, containers]
week: W15
---
# 🐳 Container Internals (important parts only)

## 1. A container is just a Linux process with:
| Mechanism | Gives | Examples |
|---|---|---|
| **Namespaces** | Isolated *view* | `pid` (own PID 1), `net` (own interfaces), `mnt` (own mounts), `uts` (hostname), `ipc`, `user` (uid mapping), `cgroup` |
| **cgroups v2** | *Limits* & accounting | `cpu.max` (quota), `memory.max` (OOM), `pids.max`, `io.max` |
| **Root filesystem** | Its own files | **overlayfs**: read-only image layers (lowerdir) + a writable upperdir |
| **Security** | Reduced privileges | capabilities (drop ALL), **seccomp** syscall filter, AppArmor/SELinux, no-new-privileges, rootless |
**Containers share the host kernel** → a kernel exploit escapes the container. That's why untrusted code (LLM-generated!) needs **gVisor** (a user-space kernel), **Kata**, or **Firecracker** microVMs.

## 2. Images (OCI image spec)
- An image = a **manifest** → a **config** (env, entrypoint, history) + an ordered list of **layers** (tar archives, content-addressed by sha256); an **index** holds multi-arch variants
- Each Dockerfile instruction that changes the filesystem creates a layer; the **cache is invalidated from the first changed step onward** → copy dependency manifests first, then source
- Deleting a file in a later layer doesn't shrink the image (whiteout files) → multi-stage builds

## 3. The runtime stack
`docker` CLI → `dockerd` → **containerd** (images, snapshots, lifecycle) → `containerd-shim` (keeps the container alive independently) → **runc** (reads the OCI runtime `config.json`, calls `clone()` with namespace flags, sets up cgroups, `pivot_root`, `execve`)
Kubernetes skips dockerd: kubelet → CRI → containerd → runc (or `runsc` for gVisor via a RuntimeClass)

## 4. Networking (Docker default bridge)
Host bridge `docker0` ↔ **veth pair** ↔ the container's `eth0`; outbound via iptables MASQUERADE (NAT); `-p 8080:80` = a DNAT rule

## 5. The PID 1 problem
PID 1 gets **no default signal handlers** and must **reap zombies** → use the exec-form `ENTRYPOINT ["app"]` (not a shell form), handle SIGTERM, or use `tini` / `docker run --init`

## 🔬 Prove it
- [ ] **Containers from scratch in Go** (Liz Rice's talk): `clone` with `CLONE_NEWUTS|NEWPID|NEWNS`, `chroot`/`pivot_root`, mount `/proc`, set a cgroup memory limit → run `/bin/sh` → [[Assignments - Phase 4]]
- [ ] `lsns`, `ls -l /proc/<pid>/ns` for a running container; `nsenter` into it
- [ ] Set `--memory=64m`, allocate 100 MB → OOM kill; read `memory.events` in the cgroup
- [ ] `docker save` an image, untar it, inspect the manifest/config/layers by hand
- [ ] Bad vs good Dockerfile ordering: time rebuilds after a one-line code change
- [ ] Shell-form entrypoint + `docker stop` → a 10 s wait (SIGTERM ignored) → fix it with exec form
- [ ] Run a container with gVisor (`--runtime=runsc`) and compare `dmesg`/syscall behavior

## Interview questions #interview-q
Container vs VM · what namespaces and cgroups do · how image layers and caching work · why containers aren't a security boundary for untrusted code · the PID 1 problem
