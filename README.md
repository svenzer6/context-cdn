# Context CDN

> A token-efficient, license-aware context delivery layer for AI agents.

**Context CDN** is an open-source proposal for making the web easier, cheaper and safer for AI agents to read. Instead of forcing agents to scrape noisy HTML, publishers can expose clean, pre-computed and token-budget-aware context packages.

Author: **Burhan Çelebi**  
Contact: [drburhancelebi@icloud.com](mailto:drburhancelebi@icloud.com)

![Context CDN social card](/social-card-context-cdn.png)

## Why this matters

Most websites are optimized for browsers, not language models. AI agents often parse navigation menus, footers, scripts, ads and boilerplate before reaching the actual meaning. That creates:

- higher token cost,
- higher latency,
- lower context quality,
- unclear licensing and attribution boundaries.

Context CDN proposes a publisher-controlled layer for **canonical AI context**.

## Core idea

A website should be able to expose:

- clean Markdown versions of canonical content,
- pre-computed summaries at multiple token budgets,
- dynamic `/ai/context` endpoints,
- semantic topic relationships,
- machine-readable licensing policies,
- payment/permission flows for commercial AI use.

## Architecture

![Context CDN architecture](./assets/architecture.png)

The proposed architecture has four layers:

1. **Clean Markdown Extraction**  
   Convert HTML, CMS pages and docs into semantic Markdown.

2. **Topic Index + Summarisation**  
   Build `ai-index.json` with topics, sources, hashes, ETags and multi-resolution summaries.

3. **Dynamic Context API**  
   Serve endpoint responses such as `/ai/context?topic=pricing&budget=1000`.

4. **Licensing Layer**  
   Use RSL-style machine-readable licensing, including attribution, blocked usage and pay-per-use flows.

## Advanced recommendations

### Tokenizer-aware adaptive budgeting

Different LLMs tokenize text differently. Context CDN should select a pre-computed summary, apply a safety margin and return `estimated_tokens`, `tokenizer_used` and `budget_target`.

![Tokenizer-aware adaptive budgeting](assets/tokenizer_adaptive_budgeting.png)

### HTTP 402 payment negotiation

When content requires payment, Context CDN can return `402 Payment Required` with links to the license and payment endpoint.

![HTTP 402 payment negotiation](assets/payment_negotiation_402.png)

### Semantic topic graph

`ai-index.json` should include topic relationships so agents can discover adjacent context without crawling the whole site.

![Semantic topic graph](assets/semantic_topic_graph.png)

## Example API

```http
GET /ai/context?topic=pricing&budget=1000&format=md
Accept-LLM-Model: gpt-4.1
Accept-Context-Budget: 1000
```

Example JSON response:

```json
{
  "topic": "pricing",
  "version": "v42",
  "budget_requested": 1000,
  "budget_target": 850,
  "estimated_tokens": 812,
  "tokenizer_used": "openai:o200k_base",
  "license": {
    "ai_include": true,
    "ai_train": false,
    "payment": "attribution"
  },
  "citations": [
    {"url": "/pricing#plans", "etag": "p-v42"}
  ],
  "content": "..."
}
```

## Repository structure

```text
.
├── assets/
│   ├── architecture.png
│   ├── tokenizer_adaptive_budgeting.png
│   ├── payment_negotiation_402.png
│   ├── semantic_topic_graph.png
│   └── social-card-context-cdn.png
├── docs/
│   ├── whitepaper.md
│   ├── whitepaper.pdf
│   └── github-publish-checklist.md
├── examples/
│   ├── ai-index.example.json
│   └── llms.txt
├── metadata/
│   └── github_about.md
├── posts/
│   ├── linkedin_tr.md
│   ├── linkedin_en.md
│   ├── short_caption_tr.md
│   └── short_caption_en.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── CITATION.cff
├── LICENSE
└── README.md
```

## GitHub repository description

Use this as your GitHub **Description**:

> Open-source proposal for a token-efficient, license-aware context delivery layer for AI agents: clean Markdown, adaptive token budgets, semantic topic graphs and RSL/pay-per-use flows.

Suggested topics:

```text
ai-agents, llm, llms-txt, context-engineering, rag, open-source,
semantic-search, markdown, rsl, licensing, token-optimization,
agentic-ai, future-of-web
```

## Whitepaper

- [Markdown whitepaper](docs/whitepaper.md)
- [PDF whitepaper](docs/whitepaper.pdf)

## Contact

Burhan Çelebi  
Email: [drburhancelebi@icloud.com](mailto:drburhancelebi@icloud.com)

## License

This repository is released for open-source publication. See [LICENSE](LICENSE).
