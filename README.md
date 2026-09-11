# CDAZZDEV Senior MLE Assessment — Lavan

Submission repository for the Senior Machine Learning Engineer assessment (Financial AI + Agentic workflow).

| Task | Folder | Notebook | Colab |
|------|--------|----------|-------|
| **Task 1** — Financial AI equity research pipeline | [`Financial_AI/`](Financial_AI/) | [`task1.ipynb`](Financial_AI/task1.ipynb) | [Open in Colab](https://colab.research.google.com/github/lavanblavan/-CDAZZDEV-MLE-Lavan/blob/main/Financial_AI/task1.ipynb) |
| **Task 3** — Agentic financial research workflow | [`Agentic_workflow/`](Agentic_workflow/) | [`task3.ipynb`](Agentic_workflow/task3.ipynb) | [Open in Colab](https://colab.research.google.com/github/lavanblavan/-CDAZZDEV-MLE-Lavan/blob/main/Agentic_workflow/task3.ipynb) |

## Quick start (local)

Each task is self-contained with its own `requirements.txt` and `.env.example`.

```powershell
# Task 1
cd Financial_AI
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt pytest
pytest
jupyter notebook task1.ipynb

# Task 3
cd ..\Agentic_workflow
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
pytest
jupyter notebook task3.ipynb
```

Never commit API keys. Use `.env` locally or Colab Secrets in the cloud. See each task README for details.

## AI tool disclosure

Per assessment policy, all AI-assisted work is disclosed in [`AI_CITATIONS.md`](AI_CITATIONS.md) (repo root) and in each task folder.

## Candidate

**Lavan** · Repository: [lavanblavan/-CDAZZDEV-MLE-Lavan](https://github.com/lavanblavan/-CDAZZDEV-MLE-Lavan)
