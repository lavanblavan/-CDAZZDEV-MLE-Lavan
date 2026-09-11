# Citations — AI tools and external resources

**Candidate:** Lavan  
**Repository:** [lavanblavan/-CDAZZDEV-MLE-Lavan](https://github.com/lavanblavan/-CDAZZDEV-MLE-Lavan)

This submission follows the assessment AI policy. Generative AI tools were used with full disclosure below. All outputs were reviewed, tested, and interpreted by the candidate.

---

## Generative AI tools

| Tool | Access | Used for |
|------|--------|----------|
| **Cursor (Composer)** | IDE assistant | Drafting and editing Python modules, LangGraph agents, unit tests, notebook markdown, prompts, and documentation; debugging evaluation and agent routing |
| **Groq API** | Free tier — `openai/gpt-oss-20b` | Task 1 runtime analyst signals; Task 3 fallback LLM for agents and sentiment scoring |
| **OpenRouter API** | Free-tier models (Task 3) | Primary runtime LLM for Agent A and Agent B when a key is set |
| **Google Colab** | Free tier | Optional cloud runtime for notebooks with Secrets-based API keys |

---

## Task 1 — Financial AI (`Financial_AI/`)

### Cursor (development)

- Indicator implementations (SMA, RSI, MACD, Bollinger) and three momentum rule variants
- Holdout evaluation, walk-forward replay, and `scripts/select_rule.py`
- Notebook explanatory text and `docs/RULE_SELECTION.md`
- README updates and test scaffolding

### Groq (runtime)

- Generates structured BUY / HOLD / SELL JSON via `src/signal.py` at notebook run time
- Prompt template in `prompts/analyst.md` (written and reviewed by the candidate)
- Output validated with `evaluate_llm_output()` (schema, confidence range, consistency)

### Not delegated to AI

- Final holdout criteria (BUY–SELL spread with minimum sample sizes, then Sharpe)
- Decision to adopt the `score` rule variant documented in `docs/RULE_SELECTION.md`
- Interpretation that results are diagnostic, not proof of trading alpha

---

## Task 3 — Agentic workflow (`Agentic_workflow/`)

### Cursor (development)

- Question routing and ticker resolution (`src/ticker.py`, `src/task_profile.py`)
- Prompt drafts (`prompts/agent_a.md`, `agent_b.md`, `extract_issuer.md`, `sentiment.md`)
- Unit tests, example question bank, notebook text, README updates

### OpenRouter / Groq (runtime)

- **Agent A** — tool selection and `DataBrief` JSON from observations
- **Agent B** — critique loop and `FinalReport` JSON
- **`llm_sentiment`** — headline scoring from −1 to +1
- **Follow-up answers** — `ask()` / `ask_agent_a()` may answer from stored brief + new facts
- **Issuer extraction fallback** — one LLM call when rules cannot parse a messy question

Structured outputs validated with Pydantic models in `src/schemas.py`. Tool facts (prices, vol, headlines) come from Yahoo Finance, news RSS, and web search — not from the LLM.

### Not delegated to AI

- Typed agent contracts (`DataBrief`, `CritiqueDecision`, `FinalReport`)
- Deterministic critic rules in `src/agent_b.py`
- Memory relate/plan logic and disk cache TTLs in `src/memory.py`
- Task-mode → required-tools mapping in `src/task_profile.py`

---

## Non-generative libraries and data sources

| Resource | Role |
|----------|------|
| **yfinance** | Price history and issuer metadata |
| **Yahoo Finance / Google News RSS / GDELT** | Headlines (Task 1) |
| **DuckDuckGo / Google News** | Web search snippets (Task 3) |
| **LangChain / LangGraph / Pydantic** | Agent orchestration and schema validation (Task 3) |
| **pandas / numpy / matplotlib / plotly** | Data handling and charts (Task 1) |

---

## Human verification

| Task | Checks performed |
|------|------------------|
| Task 1 | `pytest` — 10 tests passing; `python -m scripts.select_rule`; manual Run All on `task1.ipynb` |
| Task 3 | `pytest tests/` — 42 tests passing; manual Run All on `task3.ipynb`; review of `logs/agent_trace.jsonl` |

No API keys or secrets appear in this repository or notebook cells.

---

## Cost

All generative AI tools listed above are used on **free tiers** only; no paid subscriptions or API spend required to run this submission.
