---
tags: [cs, os]
phase: 1
---
# 🖥️ Operating Systems

**Why:** thread pools, GC pauses, container limits, file I/O, and "why is this slow" all come back to the OS.

## Core → Advanced
- [ ] Processes vs threads, context switching, and its cost
- [ ] CPU scheduling (CFS basics), user vs kernel mode, system calls
- [ ] Virtual memory, paging, TLB, page faults, the stack vs the heap
- [ ] File systems, page cache, `fsync`, and why sequential I/O is fast
- [ ] I/O models: blocking, non-blocking, `epoll`, io_uring. **This is how Netty, Go's netpoller, and Node work**
- [ ] Synchronization primitives: mutex, semaphore, condition variable, futex
- [ ] Deadlock conditions (Coffman) and prevention
- [ ] Linux: signals, file descriptors, `ulimit`, cgroups + namespaces (**this is what containers are**)
- [ ] Memory: OOM killer, swap, container memory limits vs JVM heap (`-XX:MaxRAMPercentage`)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 `strace -c` a Java and a Go HTTP server under load; compare syscall mixes
- [ ] 🟡 Tiny shell in Go: fork/exec via `os/exec`, pipes, signals (Ctrl-C forwarding)
- [ ] 🟡 10k platform threads vs 10k virtual threads: `vmstat 1` context switches + RSS
- [ ] 🔴 Write 1 GB with vs without `fsync` per 4 KB; explain it with the page cache
- [ ] ⚫ Build a "container" with `unshare` + cgroups v2 by hand (then in Go in W16)

## 🧠 Cognitive tasks
- [ ] Predict → verify: RSS of 10k platform threads (reserved vs committed stack)
- [ ] Symptom → hypotheses: "load average 40 on 8 cores, CPU 30%"
- [ ] Feynman: explain epoll to a junior in 3 minutes

## 🛰️ Orbit integration
- [ ] Size worker concurrency from measured context-switch and CPU numbers
- [ ] Container memory limits vs JVM `MaxRAMPercentage` for orbit-api

> [!info] Go deeper
> ⚙️ [[Linux & OS Internals]] · [[Container Internals]]

## Resources
- *Operating Systems: Three Easy Pieces* (free, ostep.org)
- *The Linux Programming Interface* (Kerrisk): reference
- *Systems Performance* 2e (Brendan Gregg): ch. 1–7

## Interview questions #interview-q
- Process vs thread? Why are goroutines/virtual threads cheaper?
- What happens on a page fault?
- How does `epoll` let one thread handle 10k connections?
