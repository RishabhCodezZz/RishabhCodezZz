<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  <b>AI/ML engineer in training · agents, evaluation, backend systems</b><br/>
  I build AI applications, from agent workflows to streaming APIs, and test how they fail.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:rishabhsanu11@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://leetcode.com/u/MerakizZz/"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
</p>

> **Open to:** AI/ML and software engineering internships now, full-time roles from mid-2027 · Hyderabad or remote
> Final-year B.Tech CSE (AI & ML), B.V. Raju Institute of Technology · graduating May 2027

## Highlights

- **Merged open-source fix** in [Docling](https://github.com/docling-project/docling/pull/3949), and a [Feast fix](https://github.com/feast-dev/feast/pull/6772) under review.
- **Paper presented at CML 2026** (NutriRAG-ML); Springer proceedings in press.
- **Evaluation-first habit:** every project below ships with tests and a written list of what it does *not* prove.
- Former VIP Campus Partner at Perplexity AI.

## Featured projects

### [ARGUS](https://github.com/RishabhCodezZz/ARGUS): multi-agent financial due diligence

An 11-agent system on Google ADK and Gemini that traces every number in its answer back to a source, and pauses for a human when confidence is too low.

- **Code does the maths, not the model.** Financial metrics come from executed pandas code. Contradiction detection and the release gate run with zero LLM calls.
- **Mechanical claim checking:** each stated figure is matched against its source; the report is held below a 0.98 groundedness score.
- **Measured, not assumed:** 8 scenarios, 4 deterministic metrics (no LLM judge), and an ablation. Removing code execution kept groundedness but removed all derived analysis, so groundedness alone is not enough.
- **156 tests.** *Limits:* two fictional companies; real filings are untested.

https://github.com/user-attachments/assets/b78615b5-0e26-44a3-b2f9-595346ca4589

### [GateKeep](https://github.com/RishabhCodezZz/GateKeep): small fine-tuned models as RAG judges

A LangGraph RAG app over a machine-learning textbook and the scikit-learn docs. Four gates (route, relevance, grounding, sufficiency) decide each step. I fine-tuned open-source [Laya](https://huggingface.co/convaiinnovations/laya), inspired by typed-decision models such as [Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev).

- **Result (343 held-out questions):** Laya-gated pipeline **92.1% correct vs 91.5%** for LLM gates, at **~1.5 LLM calls per question vs 10.9**. Gemma still writes the answers.
- **Built end to end:** PDF parsing, FAISS retrieval, reranking, query rewriting with bounded retries, five interchangeable gate backends, calibrated confidence with per-gate fallback thresholds.
- **Local web demo** with supporting passages and a trace of which model made which check.
- Training notebooks, both evaluation rounds and the [full results](https://github.com/RishabhCodezZz/GateKeep/blob/HEAD/docs/RESULTS.md) are in the repo.

### [Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent) · [Live demo](https://meraki-ai-voice-agent.onrender.com): real-time voice agent

Deepgram speech-to-text, an Ollama LLM and Murf text-to-speech over one WebSocket. You can interrupt it mid-sentence.

- **Time to first audio 4.0 s → 1.28 s median** by synthesising clauses in parallel while the model keeps writing (10 runs, one machine, range 0.86 to 2.48 s).
- One cancellable `asyncio` task per turn; regression tests for two interruption bugs and a session-key leak found in review.
- **242 tests in CI.** *Demo notes:* bring your own free-tier API keys; it can take up to a minute to wake.

### [Arbiter](https://github.com/RishabhCodezZz/Arbiter): fraud decisions by expected cost

Chooses allow, step-up or block by the expected rupee cost of each action.

- XGBoost + LightGBM with Platt calibration. On a **held-out test month (92,427 transactions)** the estimated benefit over no system was **₹1.678 crore (95% CI ₹1.51–1.85 crore)**, an offline estimate under stated cost assumptions.
- **XGBoost beat `gpt-oss:20b` by 3.65× PR-AUC at ~60× lower latency.** The LLM only writes explanations.
- Time-based splits, a replayable tamper-checked audit log, fails closed if a model file is missing. 105 tests, solo build.

## More projects

| Project | What it is | Evidence |
|:---|:---|:---|
| [CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection) | Audio-visual deepfake detection tested on unseen datasets | Mean zero-shot AUC **0.61 → 0.855** (DFDC, Celeb-DF) with a CLIP backbone pretrained on FaceForensics++. Single seed, bootstrap intervals, identity-disjoint splits, tests in CI. |
| [NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG) | Multilingual (English, Hindi, Telugu) RAG diet assistant with allergy and condition checks | 48-case eval: recall@5 0.32, 9.0% hallucination rate, no observed safety violations |

<details>
<summary>What the CrossFuse experiments showed</summary>

My earlier EfficientNet-B4 model scored 0.95 AUC in-domain and about 0.61 on unseen datasets, because about 97% of its training fakes were Wav2Lip lip-sync videos while DFDC and Celeb-DF contain full-face swaps. The ablation points to FaceForensics++ pretraining as the main factor, though it uses one seed and one arm differs in learning rate. The repository also records what did not help: self-blended-image pretraining, a lip-sync head that stayed at chance, and a multi-GPU setup that ran about 3x slower.

</details>

## Open source

- **[Docling · PR #3949](https://github.com/docling-project/docling/pull/3949), merged:** fixed missing hyperlinks in ODT paragraphs, headings and list items, with edge-case tests, after maintainer review.
- **[Feast · PR #6772](https://github.com/feast-dev/feast/pull/6772), under review:** fixes remote-mode table provisioning after `feast apply`; adds two feature-server endpoints and an end-to-end lifecycle test.

## Tech stack

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch" />
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white" alt="scikit-learn" />
  <img src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black" alt="Hugging Face" />
  <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white" alt="GitHub Actions" />
</p>

- **Core:** Python, asyncio, FastAPI, WebSockets, pytest
- **ML and agents:** PyTorch, scikit-learn, XGBoost, LightGBM, Hugging Face, LangGraph, Google ADK
- **Also used:** JavaScript, React, Flask, ChromaDB, FAISS, Optuna, SHAP, Render
- **Model and voice services:** Gemini, Ollama Cloud, Deepgram, Murf
