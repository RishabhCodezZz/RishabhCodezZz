<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  <b>AI/ML Engineer</b> — agentic systems, RAG, and applied ML.<br>
  I build things that report what they actually measured, including when the result was worse than I expected.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:rishabhsanu11@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://leetcode.com/MerakizZz"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
</p>

---

🎓 **Final-year B.Tech CSE (AI & ML)** at B.V. Raju Institute of Technology, Hyderabad, India (graduating May 2027). Former **Campus Ambassador, Perplexity AI**.

💼 **Open to full-time AI/ML Engineer roles** (joining mid-2027) and internships before then.

📄 Paper accepted at **CML 2026, Springer** — in press (Scopus-indexed proceedings) &nbsp;·&nbsp; 🔧 Merged [PR #3949](https://github.com/docling-project/docling/pull/3949) into **[Docling](https://github.com/docling-project/docling)** (IBM Research, 66k+ ⭐)

---

## 🚀 Featured work

| Project | What it is | The number that matters |
|---|---|---|
| 🎙️ **[Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent)** · [live demo ↗](https://meraki-ai-voice-agent.onrender.com) | Real-time streaming voice agent (STT → LLM → TTS over one WebSocket) | **~1.2–1.9 s** to first audio, down from 4.0 s · 97 tests · CI on every push |
| ⚖️ **[Arbiter](https://github.com/RishabhCodezZz/Arbiter)** | Fraud **decision** system that prices outcomes in ₹, not a fraud classifier | **+₹1.678 crore** vs no fraud system (95% CI ₹1.51–1.85 cr) on 92,427 held-out real transactions |
| 🕵️ **[ARGUS](https://github.com/RishabhCodezZz/ARGUS)** | 11-agent hierarchical due-diligence system on Google ADK (my thesis) | Groundedness **1.00** on clean runs · 120 unit tests · ablation study with committed raw evidence |
| 🥗 **[NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG)** | Multilingual RAG diet assistant (EN / Hindi / Telugu) | **1.6%** hallucination rate, **0%** safety violations across the eval suite |
| 📉 **[Credit Risk](https://github.com/RishabhCodezZz/Credit-Risk-Detection)** | 3-class credit-score classifier, built as a leakage audit | Proved public notebooks on this dataset are inflated by **+0.1197 macro-F1** from customer leakage |
| 🎭 **[CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection)** | Multi-modal audio-visual deepfake detection with per-modality attribution | 0.95 in-domain AUC vs **0.61 zero-shot** — the gap is the finding, reported not hidden |

<br>

### 🎙️ [Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent) — real-time voice agent · **[try it live ↗](https://meraki-ai-voice-agent.onrender.com)**

A voice agent that starts talking before it has finished thinking. Reply text is cut into clause-sized chunks as it streams out of the model, synthesised concurrently, and scheduled gaplessly on the Web Audio clock.

* **How the latency came down**, one measured change at a time: clause-level chunking instead of sentence-level (4.0 → 3.2 s), then a streaming TTS endpoint (3.2 → ~1.4 s). The first was a surprise — the persona asks for one-sentence replies, so a sentence-only rule meant pipelining never engaged at all.
* **Barge-in as task cancellation:** one `asyncio.Task` per turn; interrupting unwinds the in-flight HTTP request and every pending synthesis task, and the partial reply still enters history.
* **Tests cover the quiet failures**, not the loud ones — including a regression guard for a real bug where a global dict handed one visitor's API keys to the next.

### ⚖️ [Arbiter](https://github.com/RishabhCodezZz/Arbiter) — fraud decision system

Built solo for **Razorpay's AI Buildathon 2026** (Track 02, AI Risk Manager). A merchant's dashboard has a P&L, not an accuracy line — so Arbiter prices allow / step-up / block in real rupees per transaction and picks whichever loses the least money.

* **Where *not* to use AI:** benchmarked XGBoost head-to-head against a real LLM (`gpt-oss:20b`, given a fair shot) on identical data — XGBoost wins by **3.65x on PR-AUC and ~60x on latency**. The LLM only writes the explanation; delete it and every decision stays byte-identical.
* **Causal honesty, priced:** rebuilt the Kaggle-winning solution's future-leaking version to measure what refusing it costs — **+0.0066 PR-AUC**. Honesty is nearly free, and now that is a measurement instead of a claim.
* **105 tests** covering fail-closed behaviour, idempotency and audit-log tamper detection — each failure mode broken on purpose and confirmed to recover, not assumed from reading the code.

### 🕵️ [ARGUS](https://github.com/RishabhCodezZz/ARGUS) — multi-agent due diligence

A research system that refuses to state a number it cannot trace back to a source. Runs entirely on the free Gemini tier — **$0 to reproduce**.

* **Cost-aware routing:** a narrow question costs ~2–3 model calls, full research ~15–20, instead of running the whole pipeline for everything. `ParallelAgent` fan-out, and a critic ⇄ refiner loop with a hard iteration cap.
* **Two agents make zero LLM calls on purpose** — contradiction detection and the release gate are pure Python, because a check should not grade its own kind of work.
* **Verification, not vibes:** all arithmetic runs as executed pandas; a deterministic matcher scores every stated figure, and anything below 0.98 genuinely pauses for human approve / reject / redirect.
* **The ablation surprised me:** I predicted removing code execution would cause hallucinated numbers. It did not — groundedness held at 1.00. What it removed was 100% of derived analytical content. Answers stayed accurate and got shallow.

### 🥗 [NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG) — multilingual RAG

Retrieval-augmented diet assistant that auto-detects your language and answers in it, across English, Hindi and Telugu. Corresponding author on the paper (NutriRAG-ML), accepted at CML 2026, Springer — in press.

* **Safety is tested, not prompted-and-hoped:** refuses foods conflicting with a stated allergy or condition even when they appear in retrieved context — verified by the eval suite rather than assumed from the prompt.
* **No self-grading:** the eval suite's LLM-judge deliberately runs on a different provider than generation.
* **Retrieval:** `all-mpnet-base-v2` embeddings with cross-encoder reranking before generation — not raw vector similarity straight into the prompt.

### 📉 [Credit Risk Detection](https://github.com/RishabhCodezZz/Credit-Risk-Detection) — a leakage audit

Most public notebooks on this dataset report an inflated score because each customer appears ~8 times and a naive row split puts the same customer on both sides. This one measures that inflation, then eliminates it.

* **The proof:** the leaky random split reports macro-F1 0.8171; the honest customer-grouped split gets 0.6974 — demonstrated rather than merely avoided.
* **Discipline:** split before any statistic is computed, causal `shift(1)` rolling features, 10 model variants ranked on out-of-fold score only, holdout touched **exactly once**.
* **Two hypotheses that failed are kept in the notebook on purpose** — customer-level averaging and per-class threshold tuning, both rejected by their own noise floor.
* **Final:** macro-F1 0.7046 · ROC-AUC 0.8715 — a greedy-weighted ensemble that beat every individual model.

### 🎭 [CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection) — multi-modal deepfake detection

Audio-visual detection with four heads (video, audio, sync, fusion), trained on FakeAVCeleb and evaluated zero-shot on DFDC and Celeb-DF v2.

* **A threshold fixed in advance** (`SYNC_MIN_AUC = 0.70`) so the sync head's failure (AUC 0.507) could not be quietly reported as a working signal — with the root cause diagnosed: ~97% of the corpus's fakes are Wav2Lip, whose objective *is* correct lip-sync.
* **Self-Blended Images pretraining failed and was cut**, with all four attempts and the partial fix documented instead of deleted.
* **Rigor:** identity-disjoint splitting enforced by assertion · bootstrap 95% CIs and explicit *n* on every number · 12-configuration ablation grid.

---

## 🌍 Open source

**[Docling](https://github.com/docling-project/docling)** — root-caused and fixed a hyperlink-extraction regression that dropped URLs across ODT paragraphs, headings and list items. Shipped through 3 rounds of maintainer review, 44 tests passing, zero regressions.

---

## 💻 Tech Stack

**Languages & Core**

<p align="left">
  <img src="https://img.shields.io/badge/Python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54" alt="Python" />
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
  <img src="https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="SQL" />
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white" alt="Git" />
</p>

**Machine Learning & Data Science**

<p align="left">
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="scikit-learn" />
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas" />
  <img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white" alt="OpenCV" />
  <img src="https://img.shields.io/badge/XGBoost-337AB7?style=for-the-badge&logoColor=white" alt="XGBoost" />
  <img src="https://img.shields.io/badge/LightGBM-9ACD32?style=for-the-badge&logoColor=white" alt="LightGBM" />
  <img src="https://img.shields.io/badge/CatBoost-FFCC00?style=for-the-badge&logoColor=black" alt="CatBoost" />
  <img src="https://img.shields.io/badge/Optuna-2B6CB0?style=for-the-badge&logoColor=white" alt="Optuna" />
  <img src="https://img.shields.io/badge/SHAP-1F77B4?style=for-the-badge&logoColor=white" alt="SHAP" />
</p>

**LLM, RAG & Agents**

<p align="left">
  <img src="https://img.shields.io/badge/Google%20ADK-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Google ADK" />
  <img src="https://img.shields.io/badge/Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white" alt="Gemini" />
  <img src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black" alt="Hugging Face" />
  <img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white" alt="Ollama" />
  <img src="https://img.shields.io/badge/ChromaDB-FF6F61?style=for-the-badge&logoColor=white" alt="ChromaDB" />
  <img src="https://img.shields.io/badge/Deepgram-13EF93?style=for-the-badge&logoColor=black" alt="Deepgram" />
</p>

**Backend & Infrastructure**

<p align="left">
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white" alt="Flask" />
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/WebSockets-010101?style=for-the-badge&logo=socketdotio&logoColor=white" alt="WebSockets" />
  <img src="https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" alt="Pytest" />
  <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="GitHub Actions" />
  <img src="https://img.shields.io/badge/Kaggle-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white" alt="Kaggle" />
</p>

**AI-Assisted Development**

<p align="left">
  <img src="https://img.shields.io/badge/Claude%20Code-D97757?style=for-the-badge&logo=claude&logoColor=white" alt="Claude Code" />
  <img src="https://img.shields.io/badge/Cursor-000000?style=for-the-badge&logo=cursor&logoColor=white" alt="Cursor" />
</p>

<sub>Daily driver for building and reviewing — in Arbiter, three rounds of automated AI code review surfaced six real defects I had missed, including a NaN calibrator that would have produced a silent <code>allow</code>. Every finding verified and fixed by hand; the tooling proposes, the tests decide.</sub>

