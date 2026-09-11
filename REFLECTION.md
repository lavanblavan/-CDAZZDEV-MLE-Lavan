# Reflection

**Candidate:** Lavan  
**Assessment:** CDAZZDEV Senior MLE — Financial AI & Agentic Workflow

---

## What I set out to build

Task 1 asked for an honest equity research pipeline: fetch prices, compute indicators without TA-Lib, pull news, and let an LLM synthesize a structured view — then evaluate whether any of it is useful on held-out data. Task 3 extended that foundation into a multi-agent system where the model chooses tools at runtime, a critic checks for gaps, and memory avoids redundant API calls on follow-ups.

The hardest design choice in Task 1 was separating **demonstration** from **proof**. A shiny LLM brief is easy; showing that a momentum rule beats alternatives on a holdout window — while admitting the sample is tiny — is harder but more honest. I compared three rule variants (`baseline`, `acceleration`, `score`) and adopted `score` because it had the best BUY–SELL spread with enough signals, not because it maximized a single headline metric.

Task 3 forced a different kind of discipline: **typed contracts** between agents. Raw string handoffs fail silently; Pydantic models for `DataBrief`, `CritiqueDecision`, and `FinalReport` made bugs visible early. The critic’s deterministic checks (missing 90-day vol, generic risks, hedge quality) sit alongside LLM judgment so the system does not publish incomplete research when a cheap rule can catch the gap.

## What worked well

Reusing Task 1 data and news modules inside Task 3 kept the agent layer focused on orchestration rather than re-implementing finance plumbing. LangGraph ReAct for Agent A genuinely varies tool order by question type — news-only queries skip price tools, full research runs the full set. Session memory plus disk cache with TTLs made follow-ups feel responsive without hammering Yahoo on every turn.

Testing was the safety net. Ten tests for Task 1 covered indicators and evaluation edge cases; forty-two for Task 3 covered routing, memory, critic gap detection, and schema parsing. When OpenRouter free-tier models changed behaviour, tests caught regressions before I noticed them in the notebook.

## Challenges and trade-offs

Free-tier LLM limits shaped the architecture. Groq’s OTPM cap meant smaller `max_tokens` and structured JSON prompts instead of long prose. OpenRouter model availability shifts — I added a fallback chain rather than hard-coding one model name.

Colab added friction for a monorepo layout: opening a notebook from GitHub does not copy `src/`, so the setup cell must clone the submission repo and `cd` into the task subfolder. That is extra ceremony but keeps one repo for reviewers.

Evaluation in Task 1 is deliberately modest. Walk-forward and replay cells show *how* to test signals, not that this pipeline beats the market. I think that is the right tone for an assessment: show rigour without over-claiming.

## How I used AI tools

Cursor accelerated boilerplate — module skeletons, test cases, README drafts — but I reviewed every file, ran pytest after each change, and made the final calls on rule selection, critic rules, and memory TTLs. Runtime LLMs (Groq, OpenRouter) produce analyst signals and agent JSON; they do not fetch prices or invent headlines. I treat them as synthesizers over verified tool output, not as sources of truth.

If I had more time, I would add integration tests with mocked LLM responses, a small Streamlit trace dashboard for Task 3, and clearer calibration plots linking LLM confidence to historical hit rates. The current submission prioritizes reproducibility, disclosure, and honest evaluation over feature breadth — which matches what I would want from a production-minded MLE hire.
