---
tags: [mindset, meta]
---
# 📚 How to Learn: Read → Build → Write → Teach

## The four-step loop for every topic
1. **Read** (30%). A book chapter, the official docs, or a course module. Read the **official docs first** for tools (Spring, Kafka, K8s); use books for concepts.
2. **Build** (50%). Apply it the same day in Orbit or a lab. Break it on purpose (kill a pod, drop a Kafka broker, add latency).
3. **Write** (15%). Create an atomic note in `Notes/` with the *Concept Note* template: what it is, why it exists, how it works, trade-offs, gotchas, and a diagram.
4. **Teach** (5%). Explain it out loud in 2 minutes, write a blog post, or answer a question on Stack Overflow or Reddit.

## Reading books well (not just finishing them)
- Skim the TOC and chapter summaries first (10 min), then read with a question in mind
- One *Book Note* per book (template) with a chapter-by-chapter summary **in your words**
- Stop every 20 pages and write down the 3 most important ideas without looking
- It's okay to skip chapters. Books are tools, not obligations

## Spaced repetition
- Use Anki (or Obsidian Spaced Repetition plugin) for **facts**: latency numbers, isolation anomalies, Kafka configs, K8s objects
- Use `#revise` for **skills** (DSA problems, design cases) and redo them on days 3, 7, and 21
- Retrieval practice > rereading

## Hands-on principles
- **Build from scratch once**, then use the library (your own Redis, rate limiter, HTTP server, Raft)
- **Read source code** of tools you use: Spring's `DispatcherServlet`, Go's `net/http`, Kafka's producer
- **Deliberately break things** and write down what you observed

## Obsidian workflow in this vault
- `Notes/` = your second brain (atomic, linked). Link every note to at least one topic note (e.g. `[[Kafka]]`)
- Use the graph view weekly to spot isolated notes, then link them or delete them
- Daily notes in `Journal/`; weekly review every Sunday
- Recommended community plugins (optional): **Dataview** (dashboards), **Excalidraw** (diagrams), **Spaced Repetition**, **Tasks**, **Calendar**
