---
tags: [mindset, debugging]
---
# 🐞 Debugging Methodology

## The scientific method, applied
1. **Reproduce** it reliably (smallest failing case)
2. **Observe.** Logs, metrics, traces, error messages. Read the whole stack trace
3. **Hypothesize.** Write down 2–3 candidate causes
4. **Test** one variable at a time (binary search: `git bisect`, commenting out halves, feature flags)
5. **Fix** the root cause, not the symptom. Ask "why" 5 times
6. **Prevent it.** Add a regression test, alert, or guardrail, and write a post-mortem for big issues

## Toolbox
| Layer | Tools |
|---|---|
| Java | IntelliJ debugger, `jstack` (thread dumps), `jmap`/heap dumps + Eclipse MAT, JFR, async-profiler, Arthas |
| Go | Delve (`dlv`), `pprof` (cpu/heap/goroutine/block/mutex), `go test -race`, `GODEBUG` |
| Network | `curl -v`, `dig`, `tcpdump`/Wireshark, `ss`/`netstat`, `mtr` |
| Linux | `top`/`htop`, `vmstat`, `iostat`, `strace`, `lsof`, `perf`, `dmesg` |
| DB | `EXPLAIN (ANALYZE, BUFFERS)`, `pg_stat_statements`, `pg_locks`, slow query log |
| K8s | `kubectl describe/logs/events`, `kubectl debug`, k9s |
| Distributed | Trace IDs across services (OpenTelemetry), correlation IDs in logs |

## Classic bug families (know their symptoms)
- Race conditions and deadlocks · connection pool exhaustion · memory leaks / goroutine leaks
- Timezone/clock bugs · off-by-one · integer overflow · floating point for money (use `BigDecimal` / integer paise)
- N+1 queries · retry storms · cache inconsistency · out-of-order events · duplicate messages
