<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  <b>Final-year B.Tech CSE (AI/ML) · agents, RAG and evaluation</b><br/>
  I build agent and RAG systems, then measure where they fail.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:rishabhsanu11@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
</p>

Open to AI/ML and software engineering internships now, including ones that convert to full-time, and to full-time roles from mid-2027 (graduating May 2027). Based in Hyderabad; open to remote or relocating.

## Highlights

- Merged a fix into [Docling](https://github.com/docling-project/docling/pull/3949), the open-source document parser started at IBM Research. It shipped in v2.120.0.
- [GateKeep](https://github.com/RishabhCodezZz/GateKeep): fine-tuned 421M-parameter models matched LLM gates on answer correctness (92.1% vs 91.5% on 343 held-out questions) at about 1.5 LLM calls per question instead of 10.9.
- Corresponding author of NutriRAG-ML, presented at CML 2026. Springer proceedings are in press.

## Featured projects

### [ARGUS](https://github.com/RishabhCodezZz/ARGUS): multi-agent financial analysis with deterministic number checks

A system of 11 agents and 13 tools on Google ADK and Gemini that will not release a number it cannot trace to its source data. It runs on bundled sample data for two fictional companies.

- A code-only verifier extracts every number from the draft and matches it against the evidence. A report is released automatically only at 0.98 groundedness or higher with a clean critic pass; otherwise a person approves or rejects it.
- Narrow questions go to one specialist agent, which takes 2 to 3 model calls instead of about 15 to 20.
- It rejected an injected fake $5B revenue claim. Evaluated on 8 scenarios with 4 deterministic metrics (no LLM judge) plus an ablation. 156 offline tests, Ruff and Pyright run in GitHub Actions.

https://github.com/user-attachments/assets/b78615b5-0e26-44a3-b2f9-595346ca4589

### [GateKeep](https://github.com/RishabhCodezZz/GateKeep): small fine-tuned models as RAG gates

A LangGraph RAG app over a machine-learning textbook and the scikit-learn user guide. Four gates (route, relevance, grounding, sufficiency) decide each step. I fine-tuned one open-source [Laya](https://huggingface.co/convaiinnovations/laya) model per gate and compared them with Gemma 4 31B making the same decisions.

- On 343 held-out questions the Laya gates scored 92.1% against 91.5% for the LLM gates, a difference inside the bootstrap interval, at about 1.5 total LLM calls per question against 10.9. Median gate latency was 35 to 42 ms on a T4.
- What it did not show: the pipeline with no gates scored highest (95.6%), and the hybrid cascade missed my call-reduction target. Both are in the [full results](https://github.com/RishabhCodezZz/GateKeep/blob/HEAD/docs/RESULTS.md).
- Pipeline: Docling parsing, FAISS retrieval, cross-encoder reranking, five interchangeable gate backends, and calibrated confidence with per-gate thresholds. Training notebooks are in the repo.

### [Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent) · [Live demo](https://meraki-ai-voice-agent.onrender.com): real-time voice agent

Deepgram speech-to-text, Gemma on Ollama Cloud and Murf text-to-speech over one WebSocket (FastAPI, asyncio). It starts speaking before the reply is finished and stops when you talk over it.

- Time to first audio went from 4.0 s to a 1.28 s median over 10 live runs. The gains came from cutting the first chunk at a clause, Murf's streaming endpoint, synthesising up to three chunks at once, and a faster model.
- Each turn runs as one cancellable `asyncio` task, and API keys are held per connection. 242 offline tests (140 backend, 102 browser logic) run in CI.
- The live demo needs your own free-tier keys for Deepgram, Ollama and Murf. The free Render instance can take up to a minute to wake.

## More projects

- **[Arbiter](https://github.com/RishabhCodezZz/Arbiter)**: fraud decisions by expected cost (allow, step-up or block) using Platt-calibrated XGBoost and LightGBM. On a later test month of 92,427 transactions, simulated value was ₹1.68 crore above no system (95% bootstrap CI ₹1.51 to 1.85 crore, under stated cost assumptions). Tamper-checked audit log, fail-closed default, 105 tests.
- **[CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection)**: audio-visual deepfake detection, built with one teammate; I wrote most of the code. Mean AUC on two unseen datasets (DFDC, Celeb-DF v2) rose from 0.610 to 0.855 after FaceForensics++ pretraining on a CLIP backbone. Bootstrap intervals and identity-grouped splits.
- **[Credit-Risk-Detection](https://github.com/RishabhCodezZz/Credit-Risk-Detection)**: a leakage audit of a public credit-score dataset. A random row split inflated macro-F1 by 0.12; the customer-grouped pipeline reached macro-F1 0.70 and ROC-AUC 0.87 on held-out customers, scored once.
- **[NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG)**: multilingual (English, Hindi, Telugu) RAG diet assistant behind the NutriRAG-ML paper. Prompt hardening cut the hallucinated-food rate from 28% to 9% on a 48-case eval, with no allergy violations.

## Open source

- [Docling · PR #3949](https://github.com/docling-project/docling/pull/3949), merged in v2.120.0: fixed hyperlinks being dropped from ODT paragraphs, headings and list items, with regression tests. Reviewed and merged by the IBM Research maintainers.
- [Feast · PR #6772](https://github.com/feast-dev/feast/pull/6772), open and awaiting maintainer review: fixes remote-mode table provisioning after `feast apply`, and adds two feature-server endpoints and an end-to-end lifecycle test.

## Tech stack

- **Core:** Python, SQL, asyncio, FastAPI, REST APIs, WebSockets, Git, GitHub Actions, pytest, Ruff, Pyright
- **ML and agents:** PyTorch, scikit-learn, pandas, XGBoost, LightGBM, Hugging Face, LangGraph, Google ADK, FAISS, ChromaDB, Optuna
- **Methods:** RAG, fine-tuning, LLM evaluation, calibration, ablations
- **Also used:** JavaScript, React, Flask, SHAP, Render

Also: VIP Campus Partner at Perplexity AI, Sep to Dec 2025.
