<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  <b>Final-year CSE (AI/ML) student · agents, evaluation, backend systems</b><br/>
  I build agent and RAG systems and stress-test how they fail.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:rishabhsanu11@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://leetcode.com/u/MerakizZz/"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
</p>

> Open to AI/ML and software engineering internships now, full-time roles from mid-2027 · Hyderabad or remote
> B.Tech CSE (AI & ML) · graduating May 2027

## Highlights

- Merged fix in [Docling](https://github.com/docling-project/docling/pull/3949), the document parser maintained by IBM Research Zurich, reviewed by Peter Staar. A [Feast fix](https://github.com/feast-dev/feast/pull/6772) is under review.
- GateKeep: a fine-tuned small model matched LLM judges on correctness (92.1% vs 91.5%) with about 1.5 LLM calls per question instead of 10.9.
- Paper presented at CML 2026 (NutriRAG-ML); Springer proceedings in press.
- Former Campus Partner at Perplexity AI (Sep to Dec 2025).

## Featured projects

### [ARGUS](https://github.com/RishabhCodezZz/ARGUS): multi-agent financial due diligence

An 11-agent system with 13 tools, built on Google ADK and Gemini, that traces every number in its answer to a source and pauses for a human when confidence is low.

- Routes narrow questions to specialist agents, cutting model calls from about 15-20 to 2-3. Metrics come from executed pandas code, and a deterministic verifier holds any report below 0.98 groundedness for human approval; contradiction detection and the release check make no LLM calls.
- Guardrails rejected an injected fake $5B revenue claim. Evaluated on 8 scenarios with 4 deterministic metrics (no LLM judge) plus an ablation; 156 tests, Ruff and Pyright in GitHub Actions CI.

https://github.com/user-attachments/assets/b78615b5-0e26-44a3-b2f9-595346ca4589

### [GateKeep](https://github.com/RishabhCodezZz/GateKeep): small fine-tuned models as RAG judges

A LangGraph RAG app over a machine-learning textbook and the scikit-learn docs. Four gates (route, relevance, grounding, sufficiency) decide each step. I fine-tuned open-source [Laya](https://huggingface.co/convaiinnovations/laya), inspired by typed-decision models such as [Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev).

- On 343 held-out questions, the Laya pipeline matched LLM gates on correctness (92.1% vs 91.5%) at about 1.5 total LLM calls per question against 10.9.
- Pipeline: PDF parsing, FAISS retrieval, reranking, query rewriting with bounded retries, five interchangeable gate backends, calibrated confidence with per-gate fallback thresholds.
- A local web demo shows the supporting passages and which model made which check. Training notebooks, evaluation rounds and [full results](https://github.com/RishabhCodezZz/GateKeep/blob/HEAD/docs/RESULTS.md) are in the repo.

### [Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent) · [Live demo](https://meraki-ai-voice-agent.onrender.com): real-time voice agent

Deepgram speech-to-text, an Ollama LLM and Murf text-to-speech over one WebSocket (FastAPI, asyncio). You can interrupt it mid-sentence.

- Cut time to first audio from 4.0 s to a 1.28 s median (10 live runs) by synthesising clauses in parallel while the model keeps writing.
- Each turn runs as one cancellable `asyncio` task, with regression tests for interruption handling and per-connection API keys.
- 242 tests in CI. Try the live demo with your own free-tier API keys.

## More projects

| Project | What it is | Evidence |
|:---|:---|:---|
| [Arbiter](https://github.com/RishabhCodezZz/Arbiter) | Fraud decisions by expected cost: allow, step-up or block, using XGBoost and LightGBM with Platt calibration | On a held-out test month (92,427 transactions), estimated benefit over no system was ₹1.678 crore (95% CI ₹1.51 to 1.85 crore, offline estimate). XGBoost beat `gpt-oss:20b` by 3.65× PR-AUC at about 60× lower latency. Time-based splits, tamper-checked audit log, fail-closed default. 105 tests. |
| [CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection) | Audio-visual deepfake detection tested on unseen datasets; college project built with one teammate | Traced a weak unseen-data score (~0.61 AUC) to training-data bias (~97% Wav2Lip fakes), then raised mean zero-shot AUC to 0.855 (DFDC, Celeb-DF) with FaceForensics++ pretraining on a CLIP backbone. Bootstrap intervals, identity-disjoint splits, tests in CI. |
| [NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG) | Multilingual (English, Hindi, Telugu) RAG diet assistant with allergy and condition checks | Prompt hardening cut the hallucinated-food rate from 28% to 9% and raised judge faithfulness from 0.563 to 0.827 on a 48-case eval, with 0 of 48 allergy violations. |

## Open source

- [Docling · PR #3949](https://github.com/docling-project/docling/pull/3949), merged in v2.120.0: fixed missing hyperlinks in ODT paragraphs, headings and list items, with edge-case tests. Reviewed by Peter Staar of IBM Research Zurich.
- [Feast · PR #6772](https://github.com/feast-dev/feast/pull/6772), under review: fixes remote-mode table provisioning after `feast apply`, and adds two feature-server endpoints and an end-to-end lifecycle test.

## Tech stack

- **Core:** Python, SQL, asyncio, FastAPI, REST APIs, WebSockets, Git, GitHub Actions, pytest, Ruff, Pyright
- **ML and agents:** PyTorch, TensorFlow, scikit-learn, pandas, XGBoost, LightGBM, Hugging Face, LangGraph, Google ADK, RAG, LLM evaluation, calibration, ablations
- **Also used:** JavaScript, React, Flask, ChromaDB, FAISS, Optuna, SHAP, GCP, Render
