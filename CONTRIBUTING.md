# Contributing to Verbalized Sampling

Thanks for wanting to contribute. This repo improves through real test results, prompt variants, and model coverage — not speculation.

---

## What We're Looking For

1. **Prompt variants** — modified versions of the system prompt that work better for specific use cases (e.g., coding, research, creative writing)
2. **Example outputs** — side-by-side comparisons showing VS vs. standard output on the same query
3. **Model coverage** — test results for models not yet in the compatibility table

---

## How to Submit

1. Fork the repo
2. Create a branch: `git checkout -b your-contribution-name`
3. Add your changes (see format guidelines below)
4. Open a pull request with a clear title and description

---

## Example Output Format

When submitting example outputs, use this table format in your PR description or in a file under `examples/`:

| Field | Value |
|---|---|
| Model | GPT-4.1 |
| Query | "Give me a startup idea in logistics" |
| Standard output | "An app that connects shippers with spare truck capacity — Uber for freight." |
| VS output | "A cooperative logistics network for rural post offices to share last-mile delivery routes, priced as a municipal utility." |
| Probability ceiling used | 0.10 |
| Notes | VS required 2 rounds before settling on a non-Uber framing |

---

## Model Coverage

When testing a new model, include:

- Model name and version
- Whether the `<response>` / `<probability>` structure was followed
- Whether tail sampling actually shifted the output (compare 3+ queries)
- Any prompt adjustments needed to get it working
- A 1–2 sentence summary of behavior

---

## Code of Conduct

Be direct and evidence-based. Submit results you actually ran, not outputs you imagine would happen.
