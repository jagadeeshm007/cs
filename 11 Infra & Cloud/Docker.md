---
tags: [infra, docker, containers]
phase: 2-4
---
# 🐳 Docker & Containers

## Core → Advanced
- [ ] Images vs containers, layers, union FS, the build cache
- [ ] Dockerfile best practices: **multi-stage builds**, small base images (distroless, alpine caveats, scratch for Go), non-root user, `.dockerignore`, pinned versions
- [ ] Java images: layered jars / Buildpacks / Jib; JVM memory in containers
- [ ] Go images: static binary on `scratch`/distroless (~10–20 MB)
- [ ] Networking (bridge, host), volumes, bind mounts
- [ ] **Docker Compose** for local dev (Postgres, Redis, Kafka, Keycloak, observability stack)
- [ ] Under the hood: namespaces, cgroups, OCI spec, containerd/runc
- [ ] Security: image scanning (Trivy/Grype), SBOMs (Syft), signing (cosign), rootless
- [ ] BuildKit, multi-arch builds (`buildx`) for amd64/arm64

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Compose the full Orbit local stack (Postgres, Redis, Kafka, Keycloak, MinIO, Ollama)
- [ ] 🟡 Shrink images: Java < 150 MB (layers/Jib), Go < 20 MB (distroless/static)
- [ ] 🔴 `docker save` + untar: inspect the manifest/config/layers by hand
- [ ] ⚫ **Containers from scratch in Go** (W16)

## 🧠 Cognitive tasks
- [ ] Predict rebuild times for good vs bad Dockerfile ordering; verify
- [ ] PID 1 experiment: shell-form entrypoint + `docker stop`

## 🛰️ Orbit integration
- [ ] Every Orbit image: SBOM + cosign + Trivy gate

> [!info] Go deeper
> ⚙️ [[Container Internals]] · [[Linux & OS Internals]]

## Resources
- Docker docs · *Docker Deep Dive* (Poulton) · Liz Rice, *Containers from Scratch* talk
