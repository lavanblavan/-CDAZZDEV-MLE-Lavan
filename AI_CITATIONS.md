# AI tools used — CDAZZDEV Senior MLE Assessment

This submission follows the assessment AI policy: AI tools were used with full disclosure below. All outputs were reviewed, tested, and interpreted by the candidate (**Lavan**).

Task-specific detail also lives in:

- [`Financial_AI/AI_CITATIONS.md`](Financial_AI/AI_CITATIONS.md) — Task 1 (Financial AI)
- [`Agentic_workflow/AI_CITATIONS.md`](Agentic_workflow/AI_CITATIONS.md) — Task 3 (Agentic workflow)

## Tools (both tasks)

| Tool | Version / access | Purpose |
|------|------------------|---------|
| **Cursor (Composer)** | IDE assistant | Drafting and editing Python modules, tests, notebooks, prompts, and documentation; debugging and explaining evaluation results |
| **Groq API** | Free tier — `openai/gpt-oss-20b` | Runtime LLM for Task 1 analyst signals; fallback for Task 3 agents and sentiment |
| **OpenRouter API** | Free-tier models (Task 3) | Primary runtime LLM for Agent A and Agent B when a key is set |
| **Google Colab** | Free tier | Optional runtime for notebooks with Secrets-based API keys |

Third-party **frameworks** (not generative AI): LangChain, LangGraph, Pydantic, yfinance — used as libraries only in Task 3.

## Where AI was used

### Cursor (development — both tasks)

- Pipeline and evaluation logic (indicators, momentum rules, holdout comparison, replay)
- Agent routing, memory, critic rules, and typed schemas (Task 3)
- Prompt drafts (`Financial_AI/prompts/`, `Agentic_workflow/prompts/`)
- Notebook explanatory text, README updates, and `docs/RULE_SELECTION.md`
- Unit tests and review of holdout / agent trace output

### Groq / OpenRouter (runtime — not development)

- **Task 1** — structured BUY / HOLD / SELL JSON via `Financial_AI/src/signal.py`
- **Task 3** — Agent A tool selection and `DataBrief`; Agent B critique and `FinalReport`; `llm_sentiment` scoring; optional issuer extraction fallback

Structured outputs are validated in code (Task 1: `evaluate_llm_output()`; Task 3: Pydantic models in `schemas.py`). Market facts (prices, vol, headlines) come from Yahoo Finance, news RSS, and web search — not from the LLM.

## What was not delegated to AI

- Final holdout evaluation criteria and adoption of the `score` momentum rule (Task 1)
- Typed agent contracts and deterministic critic gap rules (Task 3)
- Memory relate/plan logic and disk cache TTLs (Task 3)
- API key handling (`.env` / Colab Secrets — never committed to git)
- Final interpretation of results as research, not investment advice

## Human verification

| Task | Checks |
|------|--------|
| Task 1 | `pytest` — 10 tests passing; `python -m scripts.select_rule`; manual Run All on `task1.ipynb` |
| Task 3 | `pytest tests/` — 42 tests passing; manual Run All on `task3.ipynb`; review of `logs/agent_trace.jsonl` |

No secrets appear in this repository or notebook cells.

## Cost

All tools listed above are used on **free tiers** only; no paid subscriptions or API spend required to run this submission.

---

*Candidate: Lavan · Repository: [lavanblavan/-CDAZZDEV-MLE-Lavan](https://github.com/lavanblavan/-CDAZZDEV-MLE-Lavan)*
