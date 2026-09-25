---
tags: [dsa, java, cheatsheet]
---
# 🧰 Java DSA Toolkit

```java
// Collections you'll use daily
Map<Integer,Integer> freq = new HashMap<>();
freq.merge(x, 1, Integer::sum);
freq.getOrDefault(x, 0);

Deque<Integer> stack = new ArrayDeque<>();   // push/pop/peek. Don't use Stack
Deque<Integer> queue = new ArrayDeque<>();   // offer/poll/peek

PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());

TreeMap<Integer,Integer> tm = new TreeMap<>();  // floorKey, ceilingKey, firstKey, pollFirstEntry
TreeSet<Integer> ts = new TreeSet<>();          // floor, ceiling, higher, lower

List<List<Integer>> graph = new ArrayList<>();
for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0])); // avoid a[0]-b[0] overflow
Arrays.fill(dp, -1);
long mid = lo + (hi - lo) / 2;   // avoid overflow
```

## Templates
```java
// Binary search on answer: first value where ok(x) is true
int lo = 0, hi = MAX;
while (lo < hi) { int mid = lo + (hi - lo) / 2; if (ok(mid)) hi = mid; else lo = mid + 1; }

// Union-Find with path compression + union by rank
int find(int x) { return parent[x] == x ? x : (parent[x] = find(parent[x])); }

// Dijkstra
PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> Integer.compare(a[1], b[1]));
// skip stale entries: if (d > dist[u]) continue;
```

## Gotchas
- `Integer` compared with `==` beyond the -128..127 cache → use `.equals`
- `int` overflow → use `long` for sums/products
- Recursion depth (~10k frames) → use iterative BFS/DFS for large inputs
- String concatenation in loops → `StringBuilder`
- Fast I/O for competitive programming: `BufferedReader` + `StringTokenizer`
