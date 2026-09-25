---
tags: [internals, ai, llm]
week: W19
---
# 🧬 LLM Inference Internals (what an AI engineer must understand)

## 1. Tokens
- Text → **tokens** via BPE-like tokenizers; ~0.75 English words per token on average, and **non-English text and code often need more tokens**
- You pay per token (input + output; output usually costs several times more) → token counts drive cost and latency

## 2. The forward pass
Token IDs → embeddings → N transformer blocks (**self-attention** mixes information across positions + an **MLP** transforms each position) → logits over the vocabulary → **sampling** → the next token → append → repeat (autoregressive)

## 3. Prefill vs decode (why latency looks the way it does)
| Phase | What | Bound by | Metric |
|---|---|---|---|
| **Prefill** | Process the whole prompt in parallel | Compute | **TTFT** (time to first token) grows with prompt length |
| **Decode** | One token at a time | **Memory bandwidth** (reading weights + KV cache) | **ITL/TPOT** (inter-token latency); total ≈ TTFT + n_out × ITL |
→ Long prompts hurt TTFT; long outputs hurt total latency. **Output length is the biggest latency lever.**

## 4. KV cache
- Attention needs keys/values of all previous tokens → cached per request so they aren't recomputed
- Memory ≈ 2 × layers × kv_heads × head_dim × tokens × bytes → long contexts eat GPU memory → fewer concurrent requests
- **Prompt caching** = reusing the KV cache for an identical **prefix** → much cheaper and faster input → **put stable content (system prompt, tool definitions, docs) first and variable content last** ⭐

## 5. Serving (how providers and vLLM work)
- **Continuous batching**: requests join and leave the batch every step → high GPU utilization
- **PagedAttention** (vLLM): the KV cache in fixed-size pages, like virtual memory → less fragmentation
- **Speculative decoding**: a small draft model proposes tokens, the big model verifies them in one pass
- **Quantization** (INT8/INT4, FP8): smaller and faster, with some quality loss; tensor/pipeline parallelism across GPUs
- Rate limits exist because GPU capacity is finite: they're in tokens per minute, not just requests

## 6. Sampling
- Logits → softmax(logits / **temperature**) → **top-k** / **top-p** (nucleus) truncation → sample
- Temperature 0 ≈ greedy but **not guaranteed deterministic** (batching and floating-point effects) → never rely on exact reproducibility; use evals

## 7. Structured output & tool calling
- **Constrained decoding**: at each step, mask tokens that would violate the JSON schema/grammar → guaranteed-parseable output
- **Tool calling**: tool schemas are injected into the prompt (they **cost tokens**) → the model emits a tool-call block → *your code* executes it → the result is appended as a message → the model continues. The model never executes anything itself
- Reasoning ("thinking") tokens are output tokens: better quality on hard tasks, at the cost of latency and money

## 8. Embeddings & vector search
- Embedding model: text → a fixed-size vector; similarity via cosine/dot product
- **HNSW**: a multi-layer proximity graph; search greedily from the top layer down. `M` (links per node), `ef_construction` (build quality), and `ef_search` (**recall vs latency** knob)
- IVF: cluster centroids + search the nearest lists (`nprobe`). Filtering + ANN is hard (pre- vs post-filtering → recall loss)
- Changing the embedding model = **re-embed everything** (version your indexes)

## 9. Context windows
Bigger ≠ better: cost grows linearly, attention quality degrades ("lost in the middle"), and latency increases → retrieve and compact instead of stuffing

## 🔬 Prove it
- [ ] Tokenize the same paragraph in English, Hindi/Telugu, JSON, and Go code; compare token counts
- [ ] Measure TTFT vs prompt length (1k/10k/50k tokens) and total latency vs `max_tokens`
- [ ] Enable prompt caching with a stable 5k-token prefix; compare latency and cost across 20 calls
- [ ] Implement softmax + temperature + top-p on toy logits in Go; visualize the distributions
- [ ] Run a small model with **Ollama** locally; watch tokens/s change with context length and concurrency
- [ ] Build **minbpe** (Karpathy) or a toy BPE tokenizer
- [ ] Build a simplified **HNSW** in Go; plot recall@10 vs `ef_search` against brute force → [[Assignments - Phase 5]]

## Interview questions #interview-q
Why is the first token slow and the rest fast? · How does prompt caching work, and how do you design prompts for it? · Why do tool definitions cost money? · How does structured output guarantee JSON? · HNSW trade-offs · Why isn't temperature 0 deterministic?
