---
tags: [internals, go]
week: W3
---
# 🐹 Go Runtime Internals (important parts only)

## 1. Scheduler: G-M-P
- **G** = goroutine (starts with a small ~KB stack), **M** = OS thread, **P** = processor context (count = `GOMAXPROCS`), which holds a **local run queue** (256 slots) + a `runnext` slot
- `schedule()`: runnext → local queue → (occasionally) global queue → netpoller → **work stealing** from other Ps
- **Blocking syscall**: the M blocks, and its P is handed off to another M so other goroutines keep running
- **Network I/O**: goroutines park on the **netpoller** (epoll/kqueue); no thread is blocked, which is why Go handles 100k connections easily
- **Preemption**: cooperative at function calls + **async preemption via signals** (since 1.14), so tight loops can't starve the scheduler
- `GOMAXPROCS` and container CPU limits: newer Go versions respect cgroup limits (check the release notes for your version)

## 2. Stacks
- Contiguous, **growable stacks**: on overflow the runtime allocates 2× and **copies**, adjusting pointers. Deep recursion is cheap until it isn't
- Escape analysis (`-gcflags=-m`) decides stack vs heap. Stack allocation = free, no GC

## 3. Memory allocator
- TCMalloc-inspired: per-P **mcache** (no locks) → **mcentral** per size class → **mheap** (pages/spans from the OS)
- ~70 size classes; a tiny allocator for < 16 B noscan objects
- Performance lessons: reduce allocations (preallocate slices, reuse buffers, `sync.Pool`), avoid pointer-heavy structures in huge heaps (GC scan cost)

## 4. Garbage collector
- **Concurrent, tri-color mark-and-sweep**, non-generational, non-moving; a **hybrid write barrier** during marking; short STW phases
- The **pacer** starts GC to meet `GOGC` (heap growth target, default 100%); **`GOMEMLIMIT`** is a soft memory limit (set it in containers!)
- GC assist: goroutines that allocate fast are drafted to help mark → latency spikes under allocation storms
- Watch the newer "Green Tea" GC work (experimental in 1.25); check its status in your Go version

## 5. Channels (`runtime/chan.go`)
- `hchan`: a circular buffer + `sendq`/`recvq` (queues of waiting goroutines as `sudog`s) + a **mutex**
- Send to a waiting receiver = **direct handoff** (copy straight to the receiver's stack) · buffer full → the sender parks
- Close: wakes all receivers (zero values) and panics waiting senders. Sending on a closed channel panics; receiving from a nil channel blocks forever (useful in `select`)
- `select`: shuffles cases (fairness), locks all involved channels in address order, parks on all of them
- Channels are not free: for simple shared state, a `Mutex` is often faster

## 6. Interfaces
- Non-empty interface = **(itab, data)**; `any` = **(type, data)**; the itab caches the method table
- **nil gotcha**: an interface holding a typed nil pointer is **not nil** (`err != nil` is true)
- Converting a value to an interface may **allocate** (boxing)

## 7. Slices, maps, strings
- Slice header `(ptr, len, cap)`; `append` may reallocate (≈2× for small, smoother growth for large) → **aliasing bugs** when two slices share a backing array
- **Maps**: Swiss-table implementation since Go 1.24; iteration order is randomized; **concurrent write = fatal error** (not recoverable) → `sync.Mutex` or `sync.Map` (for specific read-heavy cases)
- Strings are immutable byte slices; `[]byte(s)` copies (the compiler optimizes some cases)

## 8. sync & context
- `sync.Mutex`: normal mode (spinning, barging) → **starvation mode** after 1 ms of waiting (FIFO handoff)
- `sync.WaitGroup`, `Once` (fast-path atomic), `RWMutex` (writer preference), `atomic.*` types
- `context`: a tree; cancellation closes the `Done()` channel and propagates to children; always `defer cancel()`

## 🔬 Prove it
- [ ] `GODEBUG=schedtrace=1000,scheddetail=1` while running 10k goroutines, some CPU-bound, some sleeping
- [ ] `go build -gcflags='-m -m'` on 5 functions: predict first which variables escape, then check
- [ ] `GODEBUG=gctrace=1` with `GOGC=50/100/400` and `GOMEMLIMIT`: plot GC frequency vs heap
- [ ] Benchmark channel vs mutex for a shared counter; unbuffered vs buffered pipelines
- [ ] Create a goroutine leak (blocked send), find it with the `pprof` goroutine profile, and catch it in tests with `goleak`
- [ ] Reproduce the typed-nil-interface bug; reproduce slice aliasing via `append`
- [ ] Trigger `fatal error: concurrent map writes`, then fix it
- [ ] `go tool trace` a worker pool: observe scheduling, GC, and syscalls

## Interview questions #interview-q
G-M-P and work stealing · what happens when a goroutine makes a blocking syscall vs network I/O · how channels work internally · the nil interface gotcha · why Go maps aren't concurrent-safe · `GOGC` vs `GOMEMLIMIT` · goroutine leaks
