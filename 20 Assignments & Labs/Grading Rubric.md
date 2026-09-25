---
tags: [assignments, rubric]
---
# 📏 Grading Rubric (self-grade every assignment)

Score each dimension 0–4. **Pass = ≥ 20/28 with no zeros.** Below that, redo the weakest part before moving on. Log it in the assignment's "Score" line.

| Dimension | 0 | 2 | 4 |
|---|---|---|---|
| **Correctness** | Doesn't work | Happy path works | All acceptance criteria + edge cases |
| **Tests** | None | Unit tests | Unit + integration (Testcontainers) + concurrency/failure tests |
| **Failure handling** | Crashes/hangs | Some errors handled | Timeouts, retries, idempotency, and cancellation all proven by tests |
| **Performance evidence** | None | A number without context | Benchmark/load test with setup, percentiles, and a bottleneck analysis |
| **Code quality** | Hard to read | Reasonable | Clear boundaries, idiomatic Java/Go, patterns used deliberately |
| **Documentation** | None | README | README + ADR + diagram + "what I'd do next" |
| **Explanation** | Can't explain | Can explain with notes | **5-minute teach-back without notes**, including trade-offs |

> [!tip] The "explain it" gate is the most important one. Record a 5-minute voice memo explaining the assignment. Listen back. Would an interviewer be convinced?
