# Verbalized Sampling (VS)

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Version](https://img.shields.io/badge/version-1.0.0-green.svg)

A prompting technique that forces LLMs to sample from their full output distribution — not just the safest, most expected answer.

> Based on ["Verbalized Sampling: How to Mitigate Mode Collapse and Unlock LLM Diversity"](https://arxiv.org/abs/your-link) — Jiayi Zhang. Read the full writeup on [Substack](https://dheemanthmajji.substack.com/p/why-all-our-llms-sound-the-same-and).

---

## The Problem: Mode Collapse

LLMs trained with RLHF collapse toward a narrow set of "safe" outputs. Ask one to name a state and it says California. Ask for a startup idea and it pitches "Uber for X." Ask for a story and you get the hero's journey.

This isn't intelligence — it's statistical gravity. The model defaults to the highest-probability response because that's what got rewarded during training.

**Verbalized Sampling breaks that gravity.**

---

## Quickstart

Paste this into your system prompt:

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

### Lite Version

For quick use without the five-response scaffolding:

```
Operate in Verbalized Sampling mode. Before responding, consider the full range of possible answers — not just the most common ones. Favor responses from the tail of the distribution (low-probability, high-creativity) unless I specify otherwise.
```

---

## Side-by-Side Examples

### "Name a state."

| Mode | Response |
|---|---|
| Standard | California |
| Verbalized Sampling | Montana |

Standard models weight toward high-population, high-salience states. VS surfaces the long tail — smaller, less frequently cited states that are equally valid answers.

---

### "Write a short story about a bear."

| Mode | Response |
|---|---|
| Standard | A bear ventures into the wilderness alone, faces a challenge, and emerges transformed — a classic hero's arc with themes of resilience. |
| Verbalized Sampling | A retired bear accountant audits the forest's honey economy and discovers a fungal cartel has been fixing prices for decades. He goes to the press. |

VS avoids the default narrative gravity (hero's journey, nature metaphors) and samples from genuinely unexpected angles.

---

## Parameters

| Parameter | Default | Options |
|---|---|---|
| Number of responses | 5 | 3–10 |
| Probability ceiling | 0.10 | 0.05 (very niche) – 0.25 (moderate diversity) |
| Sampling target | Tails | Full distribution, tails only, mid-range |
| Final output | Lowest probability pick | User selects from options |

---

## When to Turn It Off

VS is not ideal for:
- Tasks requiring a single, precise factual answer (e.g., "What is 2+2?")
- Time-sensitive or high-stakes outputs where consistency matters
- Tasks where the "expected" answer is correct by definition

---

## Model Compatibility

Tested on the following models:

| Model | Works? | Notes |
|---|---|---|
| GPT-4.1 | ✅ | Follows the `<response>` / `<probability>` structure reliably |
| Gemini 2.5 Pro | ✅ | Strong tail sampling; occasionally needs probability ceiling nudge |
| Claude Sonnet | — | *Add your results here* |

---

## Files

- [`VS.md`](./VS.md) — Full prompt reference with parameters, examples, and usage notes

---

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) to submit prompt variants, example outputs, or model coverage.

---

## License

MIT — see [LICENSE](./LICENSE).
