<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  <b>AI/ML Engineering · Agentic Systems · Applied Machine Learning</b>
</p>

<p align="center">
  I build AI systems with measurable evaluations, reliable backends,
  and clear engineering trade-offs.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/">LinkedIn</a>
  ·
  <a href="mailto:rishabhsanu11@gmail.com">Email</a>
  ·
  <a href="https://leetcode.com/rishabhk_11">LeetCode</a>
</p>

Final-year **B.Tech CSE (AI & ML)** student at **B.V. Raju Institute of Technology, Hyderabad**, graduating **May 2027**.

**Seeking AI/ML engineering internships · Available for full-time roles from mid-2027.**

My projects span multi-agent systems, streaming voice applications, RAG, and predictive ML. I focus on evaluating model behavior, preventing data leakage, and understanding where systems fail.

## Featured projects

| Project | What I built | Selected result |
|:---|:---|:---|
| **[ARGUS](https://github.com/RishabhCodezZz/ARGUS)** | An 11-agent financial due-diligence system built with Google ADK and Gemini; my thesis project. | **1.00 groundedness on clean evaluation runs**, with ablation evidence and **156 tests**. |
| **[Arbiter](https://github.com/RishabhCodezZz/Arbiter)** | A fraud decision system that evaluates actions using financial costs and benefits. | **₹1.678 crore estimated benefit** versus a no-system baseline on **92,427 held-out transactions**; 95% CI: ₹1.51–1.85 crore. |
| **[Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent)** · [Demo ↗](https://meraki-ai-voice-agent.onrender.com) | A streaming voice agent connecting speech recognition, an LLM, and speech synthesis over WebSockets. | Reduced measured time to first audio from **4.0 s to ~1.3–2.2 s**; **97 tests in CI**. |

<details>
<summary><b>Engineering decisions and experiments</b></summary>

### ARGUS — evaluating analytical depth

An ablation experiment challenged my initial hypothesis: removing code execution did **not** reduce measured groundedness, which stayed at 1.00. Instead, all derived analytical content disappeared in that experiment.

The result distinguished factual accuracy from analytical usefulness. Contradiction detection and the release gate use deterministic checks without LLM calls.

**Stack:** Python, Google ADK, Gemini, pandas.

### Arbiter — connecting predictions to decisions

Built solo, with an offline evaluation that measures the financial consequences of fraud decisions.

On the same benchmark data, XGBoost achieved **3.65× the PR-AUC** of `gpt-oss:20b` with approximately **60× lower latency**. The LLM generates explanations; removing it leaves decisions unchanged.

A separate leakage experiment measured a **0.0066 PR-AUC increase** from allowing future information, quantifying the effect of that evaluation flaw.

**Stack:** Python, XGBoost, Ollama.

### Meraki — reducing streaming latency

Clause-level chunking reduced measured time to first audio from **4.0 s to 3.2 s**. Switching to a streaming TTS endpoint brought it to **~1.3–2.2 s**.

The initial sentence-level pipeline rarely overlapped generation and speech because the agent was configured to give one-sentence replies. Barge-in uses cancellation of a per-turn `asyncio.Task`.

Regression tests also cover API-key isolation between users after fixing a shared-state bug.

**Stack:** Python, asyncio, WebSockets, Deepgram.

</details>

## More projects

| Project | Focus | Selected finding |
|:---|:---|:---|
| **[CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection)** | Audio-visual deepfake detection and cross-dataset generalization. | Improved mean zero-shot AUC from approximately **0.61 to 0.855** across DFDC and Celeb-DF, with bootstrap confidence intervals. |
| **[NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG)** | A RAG diet assistant supporting English, Hindi, and Telugu. | Measured **1.6% hallucinations** and **no observed safety violations** within the evaluation suite. |
| **[Credit Risk](https://github.com/RishabhCodezZz/Credit-Risk-Detection)** | Three-class credit-score prediction with a customer-leakage audit. | Macro-F1 fell from **0.8171 to 0.6974** when replacing a row split with a customer-grouped split. |

<details>
<summary><b>Research and evaluation details</b></summary>

### CrossFuse

Investigated a baseline that achieved **0.95 in-domain AUC** but approximately **0.61 zero-shot AUC** on unseen datasets.

The investigation identified a training-data mismatch: approximately 97% of its training data consisted of Wav2Lip lip-sync fakes, while the target datasets included full-face swaps.

Pretraining a CLIP ViT-L/14 backbone on FaceForensics++ with LayerNorm-only tuning before modality fusion improved zero-shot AUC to **0.865 on DFDC** and **0.845 on Celeb-DF**. Evaluation includes bootstrap 95% confidence intervals and assertions enforcing identity-disjoint splits.

### NutriBot

Combines `all-mpnet-base-v2` retrieval with cross-encoder reranking.

The evaluation checks whether the assistant rejects recommendations that conflict with stated allergies or conditions, including when conflicting foods appear in retrieved context. The LLM judge uses a different provider from the generation model.

### Credit Risk

Customers appear approximately eight times each in the dataset, allowing a row-level split to place the same customer in both training and evaluation data.

The project measures this leakage effect, uses causal `shift(1)` features, and compares **10 variants using out-of-fold scores** before a single final holdout evaluation. The notebook also documents two unsuccessful hypotheses.

</details>

## Open-source contributions

- **[Docling](https://github.com/docling-project/docling) — [PR #3949](https://github.com/docling-project/docling/pull/3949), merged.** Fixed a regression that dropped hyperlinks from ODT paragraphs, headings, and list items. Added edge-case tests and addressed maintainer feedback and coverage requirements.

- **[Feast](https://github.com/feast-dev/feast) — [PR #6772](https://github.com/feast-dev/feast/pull/6772), under review.** Implemented remote table provisioning to address materialization failures after `feast apply`, with feature-server endpoints and an end-to-end lifecycle test.

## Technical skills

**Languages:** Python, SQL, JavaScript  
**Machine learning:** PyTorch, scikit-learn, XGBoost, LightGBM, CatBoost, pandas, NumPy, Optuna, SHAP, OpenCV  
**LLMs and retrieval:** Google ADK, Gemini, Ollama, Hugging Face, ChromaDB  
**Applications:** FastAPI, asyncio, WebSockets, Deepgram, React  
**Engineering and deployment:** pytest, GitHub Actions, Git, MySQL, GCP, Render

## Get in touch

Interested in internships involving **applied ML, agentic systems, RAG, or AI backend engineering**.

[Email me](mailto:rishabhsanu11@gmail.com) · [Connect on LinkedIn](https://www.linkedin.com/in/rishabhk11/)
