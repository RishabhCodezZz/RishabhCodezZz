<h1 align="center">Rishabh</h1>

<p align="center">
  <b>Software Engineering · AI/ML · Backend Systems</b>
</p>

<p align="center">
  I build AI applications and the software behind them—from ML evaluation
  and retrieval to streaming APIs, automated tests, and deployment.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/">
    <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
  <a href="mailto:rishabhsanu11@gmail.com">
    <img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" />
  </a>
  <a href="https://leetcode.com/rishabhk_11">
    <img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" />
  </a>
</p>

Final-year **B.Tech CSE (AI & ML)** student at **B.V. Raju Institute of Technology, Hyderabad**, graduating **May 2027**.

**Open to SDE, AI/ML, and GenAI engineering internships, as well as applied ML research opportunities. Available for full-time roles from mid-2027.**

- Build projects spanning multi-agent systems, streaming voice, RAG, and predictive ML.
- Contributed a merged fix to **Docling** and a proposed remote-provisioning fix to **Feast**.
- Presented a paper at **CML 2026**; Springer proceedings **in press**.
- Former **VIP Campus Partner at Perplexity AI**.

## Featured projects

| Project | What I built | Selected evidence |
|:---|:---|:---|
| **[ARGUS](https://github.com/RishabhCodezZz/ARGUS)** | An 11-agent financial due-diligence system using Google ADK and Gemini; my thesis project. | **156 tests** and an **8-scenario evaluation** scored on four deterministic metrics, with committed ablation evidence. |
| **[Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent)** · [Demo ↗](https://meraki-ai-voice-agent.onrender.com) | A streaming voice agent with a WebSocket pipeline, interruptible responses, and session isolation. | Reduced measured time to first audio from **4.0 s to ~1.3–2.2 s**; **97 tests in CI**. |
| **[Arbiter](https://github.com/RishabhCodezZz/Arbiter)** | A fraud decision system that evaluates actions using financial costs and benefits. | Evaluated on **92,427 held-out transactions**; estimated **₹1.678 crore benefit** over a no-system baseline in an offline experiment.* |

*Arbiter’s financial result is an experimental estimate, not realized savings.
Dataset amounts were converted from USD to INR.
Reported 95% CI: ₹1.51–1.85 crore; the estimate depends on the experiment’s cost assumptions.*

<details>
<summary><b>Engineering decisions behind these projects</b></summary>

### ARGUS — evaluating accuracy and analytical depth

The evaluation contains **eight scenarios**, covering focused queries, retrieval,
broad analysis, contradictory evidence, missing-company recovery, and adversarial
input. Results are scored on **four deterministic metrics**.

Clean evaluation runs achieved **1.00 groundedness**. In an ablation experiment,
removing code execution preserved that score but eliminated the derived
analytical content—showing why factual accuracy alone does not measure
analytical usefulness.

Contradiction detection and the release gate use deterministic checks without
LLM calls. Raw ablation evidence is committed to the repository.

### Meraki — streaming, concurrency, and isolation

Clause-level chunking reduced measured time to first audio from **4.0 s to 3.2 s**.
A streaming TTS endpoint brought it to **~1.3–2.2 s**.

The initial sentence-level pipeline rarely overlapped generation and speech
because the agent was configured to give one-sentence replies.
Barge-in cancels a per-turn `asyncio.Task`.

The test suite includes a regression check for a fixed shared-state bug that
could expose one session’s API keys to another session.

### Arbiter — separating decisions from explanations

Built solo. On the same benchmark data, XGBoost achieved **3.65× the PR-AUC**
of `gpt-oss:20b` with approximately **60× lower latency**.

The LLM generates explanations; removing it leaves every decision unchanged.

A separate experiment measured a **0.0066 PR-AUC increase** when future
information was allowed into the pipeline, quantifying the effect of leakage.

</details>

## More projects

| Project | Focus | Selected finding |
|:---|:---|:---|
| **[CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection)** | Audio-visual deepfake detection and cross-dataset generalization. | Improved mean zero-shot AUC from approximately **0.61 to 0.855** across DFDC and Celeb-DF, with bootstrap confidence intervals. |
| **[NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG)** | A multilingual RAG diet assistant supporting English, Hindi, and Telugu. | **48 evaluation cases** covering retrieval, factuality, numeric accuracy, and safety; **no observed safety violations** in the suite. |
| **[Credit Risk](https://github.com/RishabhCodezZz/Credit-Risk-Detection)** | Three-class credit-score prediction with a customer-leakage audit. | Measured a **0.1197 macro-F1 gap** between a leaky row split and a customer-grouped split. |

<details>
<summary><b>Research and evaluation details</b></summary>

### CrossFuse — investigating generalization failures

Investigated a reference baseline that achieved **0.95 in-domain AUC** but
approximately **0.61 zero-shot AUC** on unseen datasets.

The investigation identified a training-data mismatch: approximately **97%**
of the training data consisted of Wav2Lip lip-sync fakes, while the target
datasets included full-face swaps.

Pretraining a CLIP ViT-L/14 backbone on FaceForensics++ with LayerNorm-only
tuning before modality fusion improved zero-shot AUC to **0.865 on DFDC**
and **0.845 on Celeb-DF**.

Evaluation includes bootstrap 95% confidence intervals and assertions enforcing
identity-disjoint splits.

### NutriBot — evaluating retrieval and response safety

Uses `all-mpnet-base-v2` retrieval with cross-encoder reranking.

The **48-case evaluation suite** measures recall@5/10, precision, MRR,
nDCG@10, hallucination rate, numeric accuracy, safety violations,
and LLM-judged faithfulness and relevance.

Safety checks include recommendations that conflict with stated allergies
or conditions, even when conflicting foods appear in retrieved context.
The LLM judge uses a different provider from the generation model.

### Credit Risk — measuring customer leakage

Each customer appears approximately eight times in the dataset, so a random
row split can place the same customer in both training and evaluation data.

Macro-F1 dropped from **0.8171 to 0.6974** when using a customer-grouped split.

The workflow uses causal `shift(1)` features, compares **10 variants using
out-of-fold scores**, and evaluates the final selection on the holdout once.
Two unsuccessful hypotheses are also documented in the notebook.

</details>

## Open-source contributions

**[Docling](https://github.com/docling-project/docling) ·
[PR #3949](https://github.com/docling-project/docling/pull/3949) · Merged**

Fixed a regression that dropped hyperlinks from ODT paragraphs, headings,
and list items. Added edge-case tests and addressed maintainer feedback
and coverage requirements across three revisions.

**[Feast](https://github.com/feast-dev/feast) ·
[PR #6772](https://github.com/feast-dev/feast/pull/6772) · Under review**

Implemented a proposed fix for remote-mode table provisioning after
`feast apply`. Added two feature-server endpoints and an end-to-end lifecycle
test to address downstream materialization failures.

## Technical skills

**Languages:** Python, JavaScript, SQL  
**Backend and applications:** FastAPI, asyncio, WebSockets, React, MySQL  
**Machine learning:** PyTorch, scikit-learn, XGBoost, LightGBM, CatBoost, pandas, NumPy, Optuna, SHAP, OpenCV  
**LLMs and retrieval:** Google ADK, Gemini, Ollama, Hugging Face, ChromaDB, Deepgram  
**Testing and deployment:** pytest, GitHub Actions, Git, GCP, Render  

## Contact

For internship opportunities and engineering collaborations:

[Email](mailto:rishabhsanu11@gmail.com) ·
[LinkedIn](https://www.linkedin.com/in/rishabhk11/)
