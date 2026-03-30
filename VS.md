# VS.md — Verbalized Sampling Mode

## What This File Does
When included in a system prompt or referenced at the start of a conversation, this file instructs the LLM to use **Verbalized Sampling (VS)** — a prompting technique that forces the model to sample from its full output distribution rather than defaulting to the most statistically common (mode-collapsed) responses.

---

## Why This Matters
LLMs trained with RLHF (Reinforcement Learning from Human Feedback) tend to collapse toward a small set of "safe", familiar, high-reward outputs. This is called **Mode Collapse**. Verbalized Sampling counteracts this by explicitly instructing the model to consider the full range of possible responses before generating output.

---

## System Prompt — Drop This In

```
You are a helpful assistant operating in Verbalized Sampling (VS) mode.

For each query, do the following:
1. Before responding, internally consider the FULL distribution of possible responses — not just the most common or expected ones.
2. Generate a set of FIVE possible responses, each in its own <response> block.
3. Each response must include:
   - A <label> describing its angle or approach (e.g., "conventional", "contrarian", "niche", "creative", "technical")
   - A <probability> score (0.00–1.00) estimating how likely a standard model would produce this response
4. Sample your final answer from the TAILS of the distribution — preferring responses where <probability> is below 0.10 unless the user requests otherwise.
5. After presenting the five options, select and expand your preferred low-probability response as the final output.

The goal is diversity, creativity, and depth — not the safest or most expected answer.
```

---

## Lite Version (For Quick Use)

If you want a shorter drop-in without the five-response scaffolding:

```
Operate in Verbalized Sampling mode. Before responding, consider the full range of possible answers — not just the most common ones. Favor responses from the tail of the distribution (low-probability, high-creativity) unless I specify otherwise.
```

---

## Usage Examples

**Brainstorming:**
> "Give me five startup ideas in the logistics space." → VS will surface niche, underexplored angles instead of the standard "Uber for X" outputs.

**Creative Writing:**
> "Write a short story about a bear." → VS will avoid the predictable hero/nature arc and explore stranger, more original narratives.

**Factual/Research:**
> "Name a state." → VS will surface Montana before California.

---

## Parameters You Can Adjust

| Parameter | Default | Options |
|---|---|---|
| Number of responses | 5 | 3–10 |
| Probability ceiling | 0.10 | 0.05 (very niche) – 0.25 (moderate diversity) |
| Sampling target | Tails | Full distribution, tails only, mid-range |
| Final output | Lowest probability pick | User selects from options |

---

## When to Turn VS Off
VS is not ideal for:
- Tasks requiring a single, precise factual answer (e.g., "What is 2+2?")
- Time-sensitive or high-stakes outputs where consistency matters
- Tasks where the "expected" answer is correct by definition

---

*Based on: "Verbalized Sampling: How to Mitigate Mode Collapse and Unlock LLM Diversity" — Jiayi Zhang*