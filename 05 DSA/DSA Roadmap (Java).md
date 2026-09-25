---
tags: [dsa, roadmap]
language: java
---
# 🧩 DSA Roadmap (Java)

> [!goal] Targets by week 24
> - **350–400 quality problems** (mostly medium), each one logged
> - Solve an unseen medium in ≤ 25 min and explain it clearly while coding
> - LeetCode contest rating ~1800+ (a good signal, not a must)
> - Every pattern in [[Pattern Playbook]] at least at "can recognize + implement"

## Method (this matters more than the number of problems)
1. **Learn the pattern** (theory + 2 canonical problems with a solution walkthrough)
2. **Solve 8–15 problems** in that pattern, easy → medium → 1–2 hard
3. **25-min rule:** stuck → look at a hint only → another 10 min → read the solution → **re-code it from memory** the next day
4. **Log it** with the *DSA Problem* template: pattern, key insight (one line), complexity, mistakes
5. **Revise** (`#revise`) on days 3, 7, and 21
6. **Speak while you solve.** Practise the interview voice: clarify → examples → brute force → optimize → code → test → complexity

## Week-by-week
| Week | Pattern(s) | Target |
|---|---|---|
| W1 | Complexity, Java collections, arrays & hashing | 15 |
| W2 | Two pointers, sliding window, prefix sum | 18 |
| W3 | Stack, monotonic stack/queue, binary search (+ on answer) | 18 |
| W4 | Linked list, recursion, fast/slow pointers | 15 |
| W5 | Binary trees: traversals, BFS/DFS, diameter, LCA, serialize | 18 |
| W6 | BST, heaps, top-K, two heaps (median), merge K | 15 |
| W7 | Backtracking: subsets, permutations, combinations, N-Queens, word search | 15 |
| W8 | Graphs I: BFS/DFS, grids, islands, clone graph, bipartite | 15 |
| W9 | Graphs II: topo sort (Kahn), union-find, Dijkstra, multi-source BFS | 15 |
| W10 | DP I: 1-D (climbing, house robber, decode ways, coin change) | 15 |
| W11 | DP II: 2-D/grid/strings (LCS, edit distance, unique paths, palindromes) | 15 |
| W12 | DP III: knapsack (0/1, unbounded), LIS, partition, interval DP | 12 |
| W13 | Greedy, intervals (merge, meeting rooms, jump game) | 15 |
| W14 | Tries, bit manipulation, math, revision | 15 |
| W15 | Advanced graphs (MST Kruskal/Prim, Bellman-Ford, Floyd, bridges) + segment tree / Fenwick | 12 |
| W16 | DP IV: bitmask, tree DP, DP on subsequences, hard mix | 10 |
| W17–18 | Company-tagged mediums (Amazon, Google, Microsoft, Uber, Atlassian, Flipkart) | 40 |
| W19–22 | Maintenance: 2 mediums or 1 hard/day + contests | 60 |
| W23–26 | Timed mocks, weak-pattern repair | 40 |

## Problem sources
- ⭐ **NeetCode 150 → NeetCode 250** (pattern-organized; video explanations)
- **Striver's A2Z DSA sheet** / SDE sheet (very popular for Indian MNC prep)
- LeetCode **company-tagged** lists (Premium is worth it in W17+)
- *Grind 75* (Tech Interview Handbook) for a final pass
- Contests: LeetCode weekly (Sunday) + biweekly (Saturday); optional Codeforces Div 3

## Books
- *Grokking Algorithms* 2e (warm-up) · *The Algorithm Design Manual* (Skiena) · CLRS (reference only)
- *Cracking the Coding Interview* (classic) · *Beyond Cracking the Coding Interview* (2025, updated strategy)

Related: [[Pattern Playbook]] · [[Java DSA Toolkit]]

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 **Speed drills**: 3 easy problems in 20 min total, every Monday
- [ ] 🔴 **Hard Friday**: 1 hard problem, a 60-min limit, then write an editorial for it
- [ ] 🔴 **Contest discipline**: every LeetCode weekly + biweekly; upsolve every missed problem within 48 h
- [ ] ⚫ **Mock marathons** from W17: 2 problems in 45 min, spoken aloud, recorded

## 🧠 Cognitive tasks
- [ ] Predict the complexity and pattern *before* coding; log accuracy weekly
- [ ] Constraint flip: re-solve a problem with n = 10⁹ or a streaming input
- [ ] Teach-back: explain one solution per day in 2 minutes as if in an interview

## 🛰️ Orbit integration
- [ ] Topo sort → the DAG executor · heaps → timers/priority queues · union-find → dependency grouping · tries → prompt/tool name routing · sliding windows → rate limiters · consistent hashing → shard routing

> [!info] Go deeper
> 🧩 [[Pattern Playbook]] · [[Java DSA Toolkit]]

