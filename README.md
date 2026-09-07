<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  <b>AI/ML Engineer</b> — agentic systems, RAG, and applied ML.<br>
  I build things that report what they actually measured, including when the result was worse than I expected.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:rishabhsanu11@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://leetcode.com/rishabhk_11"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
</p>

---

🎓 **Final-year B.Tech CSE (AI & ML)** at B.V. Raju Institute of Technology, Hyderabad, India (graduating May 2027).
💼 **Open to full-time AI/ML Engineer roles** (joining mid-2027) and internships before then.

- 📄 Corresponding author on **NutriRAG-ML**, accepted at **CML 2026, Springer** (Scopus-indexed).
- 🔧 Merged a bug fix into **[Docling](https://github.com/docling-project/docling)** (IBM Research, 66k+ ⭐) — [PR #3949](https://github.com/docling-project/docling/pull/3949).
- 🔭 Currently building **ARGUS**, a multi-agent due-diligence system on Google's Agent Development Kit, as my thesis.
- 🎙️ Also shipping **[Meraki](https://meraki-ai-voice-agent.onrender.com)** — a real-time voice agent you can talk to right now in your browser.
- 🌐 Former **Campus Ambassador, Perplexity AI**.

---

## 🚀 Featured work

| Project | What it is | The number that matters |
|---|---|---|
| 🎙️ **[Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent)** · [live demo ↗](https://meraki-ai-voice-agent.onrender.com) | Real-time streaming voice agent (STT → LLM → TTS over one WebSocket) | **~1.2–1.9 s** to first audio, down from 4.0 s · 97 tests · CI on every push |
| ⚖️ **[Arbiter](https://github.com/RishabhCodezZz/Arbiter)** | Fraud **decision** system that prices outcomes in ₹, not a fraud classifier | **+₹1.678 crore** vs no fraud system (95% CI ₹1.51–1.85 cr) on 92,427 held-out real transactions |
| 🕵️ **[ARGUS](https://github.com/RishabhCodezZz/ARGUS)** | 11-agent hierarchical due-diligence system on Google ADK | Groundedness **1.00** on clean runs · 120 unit tests · ablation study with committed raw evidence |
| 🥗 **[NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG)** | Multilingual RAG diet assistant (EN / Hindi / Telugu) | **1.6%** hallucination rate, **0%** safety violations · published at CML 2026, Springer |
| 📉 **[Credit Risk](https://github.com/RishabhCodezZz/Credit-Risk-Detection)** | 3-class credit-score classifier, built as a leakage audit | Proved public notebooks on this dataset are inflated by **+0.1197 macro-F1** from customer leakage |
| 🎭 **[CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection)** | Multi-modal audio-visual deepfake detection with per-modality attribution | 0.95 in-domain AUC vs **0.61 zero-shot** — the gap is the finding, reported not hidden |

<br>

### 🎙️ [Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent) — real-time voice agent · **[try it live ↗](https://meraki-ai-voice-agent.onrender.com)**

A voice agent that starts talking before it has finished thinking. Reply text is cut into clause-sized chunks as it streams out of the model, synthesised concurrently, and scheduled gaplessly on the Web Audio clock.

* **Latency, measured:** time-to-first-audio ~1.2–1.9 s, brought down from 4.0 s by two changes that were each measured, not guessed — clause-level chunking (4.0 → 3.2 s) and a streaming TTS endpoint (3.2 → ~1.4 s).
* **Barge-in as task cancellation:** one `asyncio.Task` per turn; interrupting unwinds the in-flight HTTP request and every pending synthesis task, and the partial reply still enters history.
* **97 tests, no network and no keys**, run on every push — including a regression guard for a real bug where a global dict handed one visitor's API keys to the next.
* **Stack:** FastAPI · asyncio · WebSockets · Deepgram Nova-3 · Ollama Cloud · Murf · AudioWorklet

### ⚖️ [Arbiter](https://github.com/RishabhCodezZz/Arbiter) — fraud decision system

Built solo for **Razorpay's AI Buildathon 2026** (Track 02, AI Risk Manager). A merchant's dashboard has a P&L, not an accuracy line — so Arbiter prices allow / step-up / block in real rupees per transaction and picks whichever loses the least money.

* **Business impact:** +₹1.678 crore vs no fraud system, +₹77.03 lakh vs the industry-default 0.5 cutoff, on one untouched test month of 92,427 real transactions — both with bootstrap confidence intervals.
* **Where *not* to use AI:** benchmarked XGBoost head-to-head against a real LLM (`gpt-oss:20b`, given a fair shot) on identical data — XGBoost wins by **3.65x on PR-AUC and ~60x on latency**. The LLM only writes the explanation; delete it and every decision stays byte-identical.
* **Causal honesty, priced:** rebuilt the Kaggle-winning solution's future-leaking version to measure what refusing it costs — **+0.0066 PR-AUC**. Honesty is nearly free, and now that is a measurement instead of a claim.
* **105 tests** covering fail-closed behaviour, idempotency, and audit-log tamper detection — each failure mode broken on purpose and confirmed to recover.

### 🕵️ [ARGUS](https://github.com/RishabhCodezZz/ARGUS) — multi-agent due diligence

A research system that refuses to state a number it cannot trace back to a source. Runs entirely on the free Gemini tier — **$0 to reproduce**.

* **Architecture:** 11 agents on Google's ADK with cost-aware routing (a narrow question costs ~2–3 model calls, full research ~15–20), `ParallelAgent` fan-out, and a critic ⇄ refiner loop with a hard iteration cap.
* **Two agents make zero LLM calls on purpose** — contradiction detection and the release gate are pure Python, because a check should not grade its own kind of work.
* **Verification, not vibes:** all arithmetic runs as executed pandas; a deterministic matcher scores every stated figure, and anything below 0.98 genuinely pauses for human approve / reject / redirect.
* **The ablation surprised me:** I predicted removing code execution would cause hallucinated numbers. It did not — groundedness stayed at 1.00. What it removed was 100% of derived analytical content. Answers stayed accurate and got shallow. Raw evidence committed.

### 🥗 [NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG) — multilingual RAG · *published*

Retrieval-augmented diet assistant that auto-detects your language and answers in it, across English, Hindi and Telugu.

* **Published:** corresponding author, **CML 2026, Springer** (Scopus-indexed), as NutriRAG-ML.
* **Safety is tested, not prompted-and-hoped:** refuses foods conflicting with a stated allergy or condition even when they appear in retrieved context — verified by the eval suite at a **1.6% hallucination rate and 0% safety violations**.
* **No self-grading:** the eval suite's LLM-judge deliberately runs on a different provider than generation.
* **Stack:** Flask · ChromaDB · `all-mpnet-base-v2` · cross-encoder reranking · React

### 📉 [Credit Risk Detection](https://github.com/RishabhCodezZz/Credit-Risk-Detection) — a leakage audit

Most public notebooks on this dataset report an inflated score because each customer appears ~8 times and a naive row split puts the same customer on both sides. This one measures that inflation, then eliminates it.

* **The result:** the leaky random split reports macro-F1 0.8171; the honest customer-grouped split gets 0.6974 — **+0.1197 of pure leakage**, demonstrated rather than merely avoided.
* **Discipline:** split before any statistic is computed, causal `shift(1)` rolling features, 10 model variants ranked on out-of-fold score only, holdout touched **exactly once**.
* **Two hypotheses that failed are kept in the notebook on purpose** — customer-level averaging and per-class threshold tuning, both rejected by their own noise floor.
* **Final:** macro-F1 0.7046 · ROC-AUC 0.8715 · LightGBM/XGBoost/CatBoost ensemble · Optuna · SHAP

### 🎭 [CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection) — multi-modal deepfake detection

Audio-visual detection with four heads (video, audio, sync, fusion), trained on FakeAVCeleb and evaluated zero-shot on DFDC and Celeb-DF v2.

* **The central finding is a negative one:** 0.95 AUC in-domain collapses to ~0.61 cross-dataset. Strong in-domain numbers on this corpus substantially overstate real-world transfer — reported as measured, not tuned away.
* **A threshold fixed in advance** (`SYNC_MIN_AUC = 0.70`) so the sync head's failure (AUC 0.507) could not be quietly reported as a working signal — with the root cause diagnosed: ~97% of the corpus's fakes are Wav2Lip, whose objective *is* correct lip-sync.
* **Self-Blended Images pretraining failed and was cut**, with all four attempts and the partial fix documented instead of deleted.
* **Rigor:** identity-disjoint splitting enforced by assertion · bootstrap 95% CIs and explicit *n* on every number · 12-configuration ablation grid.

---

## 🌍 Open source

📄 **[Docling](https://github.com/docling-project/docling)** (IBM Research, 66k+ ⭐) — root-caused and fixed a hyperlink-extraction regression that dropped URLs across ODT paragraphs, headings and list items. Shipped through 3 rounds of maintainer review, 44 tests passing, zero regressions. **[PR #3949, merged](https://github.com/docling-project/docling/pull/3949)**.

---

## 🧰 Tech Stack

💻 **Languages** — Python, JavaScript, SQL
🧠 **ML** — PyTorch, scikit-learn, LightGBM, XGBoost, CatBoost, Optuna, SHAP, Hugging Face Transformers
🤖 **LLM / Agents** — Google ADK, Gemini, Ollama, ChromaDB, cross-encoder reranking, RAG evaluation
⚙️ **Backend** — FastAPI, Flask, asyncio, WebSockets, pytest
🛠️ **Tooling** — Git, GitHub Actions, Docker, Kaggle, Render

---

📫 **[rishabhsanu11@gmail.com](mailto:rishabhsanu11@gmail.com)** · **[LinkedIn](https://www.linkedin.com/in/rishabhk11/)**
