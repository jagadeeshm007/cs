---
tags: [internals, linux, os]
week: W1
---
# 🐧 Linux & OS Internals (important parts only)

## 1. Syscalls & context switches
- User → kernel transitions cost ~100 ns–µs; context switches cost more (µs + cache/TLB pollution) → **fewer, bigger I/O calls**, and thread counts matter
- `strace -c` shows where a process spends its syscalls

## 2. Virtual memory
- Every process sees its own address space; pages (4 KB) map to physical frames through page tables; the **TLB** caches translations
- **Page faults**: minor (mapping only) vs major (disk read) → latency spikes
- `fork()` uses **copy-on-write** (why Redis `BGSAVE` memory spikes)
- Overcommit + the **OOM killer**: picks a victim by `oom_score`; in containers, the cgroup limit triggers it

## 3. Page cache & durability
- Reads/writes go through the **page cache**; `write()` returning ≠ on disk → **`fsync`** is what makes it durable (databases and Kafka reason about this)
- Sequential I/O + readahead is far faster than random I/O (this is why logs and LSM trees exist)

## 4. I/O multiplexing
- Blocking I/O (a thread per connection) → non-blocking + **epoll** (readiness events) → **io_uring** (submission/completion rings, fewer syscalls)
- The C10k problem and why event loops / goroutines / virtual threads solve it

## 5. CPU scheduling
- Linux uses the fair scheduler (CFS, replaced by EEVDF since 6.6); `nice`; CPU affinity
- **cgroup CPU quota** (`cpu.max`) → throttling in 100 ms periods → p99 latency spikes for bursty services

## 6. File descriptors & limits
Everything is a file: sockets, pipes, files → `ulimit -n`; "too many open files" = fd leak or pool misconfiguration; `lsof -p`

## 7. Load average & saturation
Load = runnable + uninterruptible (D state, usually I/O) tasks; compare it with the core count; use `vmstat 1` (r, b, si/so, wa), `iostat -x`, `pidstat`

## 🔬 Prove it
- [ ] `strace -f -c` a Java and a Go HTTP server under load; compare syscall profiles
- [ ] `perf top` / flame graph of a CPU-bound Go program
- [ ] Write 1 GB with and without `fsync` per 4 KB; compare throughput
- [ ] `vmstat 1` while causing memory pressure → watch swap/page faults
- [ ] Run a container with `--cpus=0.5`, send bursty load, and read `cpu.stat` (`nr_throttled`)
- [ ] Leak fds in a Go program until EMFILE; find it with `lsof`

## Interview questions #interview-q
What happens during a context switch · page cache and fsync · epoll vs threads · CPU throttling in containers · what the load average means
