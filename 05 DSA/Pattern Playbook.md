---
tags: [dsa, patterns]
---
# 🎯 Pattern Playbook: recognize → apply

| If the problem says... | Think... |
|---|---|
| Sorted array, find pair/triplet | Two pointers |
| Contiguous subarray/substring with a condition | Sliding window (variable) / prefix sum + hashmap |
| Subarray sum = K (negatives allowed) | Prefix sum + hashmap |
| "Next greater/smaller", histogram, stock span | Monotonic stack |
| Sliding-window max/min | Monotonic deque |
| Sorted / monotonic answer space, "minimize the max" | Binary search (on the answer) |
| Top/Kth largest, merge K sorted, streaming median | Heap(s) |
| All combinations/permutations/subsets | Backtracking |
| Shortest path, unweighted | BFS |
| Shortest path, weighted non-negative | Dijkstra |
| Negative weights | Bellman-Ford |
| Dependencies / ordering | Topological sort |
| Connectivity, grouping, cycle in undirected graph | Union-Find (DSU) |
| Prefix/word lookup, autocomplete | Trie |
| Overlapping intervals | Sort by start + merge / sweep line / min-heap of ends |
| Optimal value over choices with overlapping subproblems | DP (define state → transition → base → order) |
| "Count ways" | DP / combinatorics |
| Range queries with updates | Segment tree / Fenwick tree |
| Linked list cycle / middle | Fast & slow pointers |
| XOR tricks, subsets as masks | Bit manipulation |
| LRU/LFU, design a data structure | HashMap + doubly linked list / multiple maps |

## DP framework
1. **State**: what minimal info defines a subproblem? `dp[i]`, `dp[i][j]`, `dp[mask]`
2. **Transition**: how does the state build from smaller states?
3. **Base cases**
4. **Order** (top-down memo first, then convert to bottom-up, then space-optimize)
5. **Answer location**

## Interview communication script
1. Restate the problem and confirm the I/O, constraints, and edge cases (empty, duplicates, negatives, overflow)
2. Walk through 1–2 examples by hand
3. State the brute force + its complexity
4. Optimize: name the pattern and why it fits
5. Code cleanly (good names, helper methods)
6. Dry-run the code on an example; test edge cases
7. State time/space complexity; discuss follow-ups
