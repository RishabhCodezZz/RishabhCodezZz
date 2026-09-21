<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  <b>AI/ML Engineer</b> — agentic systems, RAG, applied ML.<br>
  I build things that report what they actually measured, including when the result was worse than I expected.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:rishabhsanu11@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://leetcode.com/rishabhk_11"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
</p>

---

Final-year **B.Tech CSE (AI & ML)** at B.V. Raju Institute of Technology, Hyderabad — graduating May 2027.<br>
**Open to AI/ML Engineer roles** (full-time from mid-2027, internships before then).<br>
Paper accepted at **CML 2026, Springer** — Scopus-indexed proceedings, in press. Former Campus Ambassador, Perplexity AI.

## Projects

| Project | What it is | The number that matters |
|---|---|---|
| **[ARGUS](https://github.com/RishabhCodezZz/ARGUS)** | 11-agent hierarchical due-diligence system on Google ADK (my thesis) | Groundedness **1.00** on clean runs · 140 tests · ablation study with committed raw evidence |
| **[Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent)** · [live ↗](https://meraki-ai-voice-agent.onrender.com) | Real-time streaming voice agent (STT → LLM → TTS over one WebSocket) | **~1.3–2.2 s** to first audio, down from 4.0 s · 97 tests in CI |
| **[Arbiter](https://github.com/RishabhCodezZz/Arbiter)** | Fraud **decision** system that prices outcomes in ₹, not a fraud classifier | **+₹1.678 crore** vs no fraud system (95% CI ₹1.51–1.85 cr) on 92,427 held-out real transactions |
| **[NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG)** | Multilingual RAG diet assistant (EN / Hindi / Telugu) | **1.6%** hallucination rate, **0%** safety violations across the eval suite |
| **[Credit Risk](https://github.com/RishabhCodezZz/Credit-Risk-Detection)** | 3-class credit-score classifier, built as a leakage audit | Proved public notebooks on this dataset are inflated by **+0.1197 macro-F1** from customer leakage |
| **[CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection)** | Multi-modal audio-visual deepfake detection with per-modality attribution | 0.95 in-domain AUC vs **0.61 zero-shot** — the gap is the finding, reported not hidden |

<details>
<summary><b>The interesting part of each one</b></summary>

<br>

**ARGUS** — I predicted that removing code execution would cause hallucinated numbers. It did not; groundedness held at 1.00. What disappeared was 100% of the derived analytical content — answers stayed accurate and got shallow. Two agents make zero LLM calls on purpose (contradiction detection and the release gate), because a check should not grade its own kind of work. Runs entirely on the free Gemini tier, so it costs $0 to reproduce.

**Meraki** — latency came down one measured change at a time: clause-level chunking instead of sentence-level (4.0 → 3.2 s), then a streaming TTS endpoint (3.2 → ~1.3–2.2 s). The first was a surprise: the persona asks for one-sentence replies, so a sentence-only rule meant pipelining never engaged at all. Barge-in is task cancellation — one `asyncio.Task` per turn. Tests include a regression guard for a real bug where a global dict handed one visitor's API keys to the next.

**Arbiter** — built solo. Benchmarked XGBoost head-to-head against a real LLM (`gpt-oss:20b`, given a fair shot) on identical data: XGBoost wins by 3.65x on PR-AUC and ~60x on latency, so the LLM only writes the explanation — delete it and every decision stays byte-identical. Rebuilding the Kaggle-winning solution's future-leaking version priced what refusing leakage costs: +0.0066 PR-AUC. Honesty is nearly free, and now that is a measurement instead of a claim.

**NutriBot** — refuses foods that conflict with a stated allergy or condition even when they appear in retrieved context, verified by the eval suite rather than assumed from the prompt. The LLM judge deliberately runs on a different provider than generation. Retrieval is `all-mpnet-base-v2` with cross-encoder reranking, not raw vector similarity straight into the prompt.

**Credit Risk** — each customer appears ~8 times, so a naive row split puts the same customer on both sides. The leaky split reports macro-F1 0.8171; the honest customer-grouped split gets 0.6974. Causal `shift(1)` features, 10 variants ranked on out-of-fold score only, holdout touched exactly once. Two hypotheses that failed are kept in the notebook on purpose.

**CrossFuse** — `SYNC_MIN_AUC = 0.70` was fixed in advance so the sync head's failure (AUC 0.507) could not be quietly reported as a working signal, with the root cause diagnosed: ~97% of the corpus's fakes are Wav2Lip, whose objective *is* correct lip-sync. Identity-disjoint splits enforced by assertion, bootstrap 95% CIs and explicit *n* on every number.

</details>

## Open source

**[Docling](https://github.com/docling-project/docling)** (IBM Research · 66k★) — [PR #3949](https://github.com/docling-project/docling/pull/3949), **merged**. Root-caused a regression that had been silently dropping hyperlinks from ODT paragraphs, headings and list items since v2.118.0. Landed across three rounds of maintainer review with new edge-case tests and no regressions.

**[Feast](https://github.com/feast-dev/feast)** (7.3k★) — [PR #6772](https://github.com/feast-dev/feast/pull/6772), under review. `feast apply` in remote mode registered feature views but never provisioned their tables, so every later write to a new feature failed with an HTTP 500 at materialization. Proposed three fix designs to the reporter and built the one they picked: two feature-server endpoints that provision from protobuf payloads, plus an end-to-end lifecycle test.

## Stack

**Languages** · Python, JavaScript, SQL<br>
**ML** · PyTorch, scikit-learn, XGBoost / LightGBM / CatBoost, pandas, NumPy, Optuna, SHAP, OpenCV<br>
**LLM & agents** · Google ADK, Gemini, Ollama, Hugging Face, ChromaDB, Deepgram<br>
**Backend & infra** · FastAPI, asyncio, WebSockets, React, pytest, GitHub Actions, Git, MySQL, GCP, Render<br>
**Tooling** · Claude Code, Cursor
