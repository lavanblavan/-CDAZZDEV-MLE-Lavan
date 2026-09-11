# CDAZZDEV Senior MLE Assessment — Lavan

Submission repository for the Senior Machine Learning Engineer assessment (Financial AI + Agentic workflow).

| Task | Folder | Notebook | Colab |
|------|--------|----------|-------|
| **Task 1** — Financial AI equity research pipeline | [`task1_financial/`](task1_financial/) | [`task1.ipynb`](task1_financial/task1.ipynb) | [Open in Colab](https://colab.research.google.com/github/lavanblavan/-CDAZZDEV-MLE-Lavan/blob/main/task1_financial/task1.ipynb) |
| **Task 3** — Agentic financial research workflow | [`task3_agentic/`](task3_agentic/) | [`task3.ipynb`](task3_agentic/task3.ipynb) | [Open in Colab](https://colab.research.google.com/github/lavanblavan/-CDAZZDEV-MLE-Lavan/blob/main/task3_agentic/task3.ipynb) |

## Colab setup

Each notebook clones this repo into `/content/CDAZZDEV-MLE-Lavan`, then enters the task subfolder (`task1_financial` or `task3_agentic`) so `src/` is available. Add API keys in **Colab Secrets** before running:

- Task 1: `GROQ_API_KEY`
- Task 3: `OPENROUTER_API_KEY` (preferred) and/or `GROQ_API_KEY`

## Quick start (local)

Each task is self-contained with its own `requirements.txt` and `.env.example`.

```powershell
# Task 1
cd task1_financial
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt pytest
pytest
jupyter notebook task1.ipynb

# Task 3
cd ..\task3_agentic
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
pytest
jupyter notebook task3.ipynb
```

Never commit API keys. Use `.env` locally or Colab Secrets in the cloud.

## Submission documents

| File | Purpose |
|------|---------|
| [`CITATIONS.md`](CITATIONS.md) | AI tool and resource disclosure |
| [`REFLECTION.md`](REFLECTION.md) | Candidate reflection (≤600 words) |

## Candidate

**Lavan** · Repository: [lavanblavan/-CDAZZDEV-MLE-Lavan](https://github.com/lavanblavan/-CDAZZDEV-MLE-Lavan)
