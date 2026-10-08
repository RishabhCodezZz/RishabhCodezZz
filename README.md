<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  AI/ML engineering · Backend systems · Evaluation
</p>

<p align="center">
  I build AI applications, from retrieval and agent workflows to streaming APIs, and test how they behave.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:rishabhsanu11@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://leetcode.com/rishabhk_11"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
</p>

I'm a final-year B.Tech CSE (AI & ML) student at B.V. Raju Institute of Technology, Hyderabad, graduating in May 2027. I'm looking for SDE and AI/ML internships, and full-time roles from mid-2027.

- Open-source contributions: a merged fix in [Docling](https://github.com/docling-project/docling/pull/3949) and a [Feast fix](https://github.com/feast-dev/feast/pull/6772) under review.
- Presented a paper at CML 2026; Springer proceedings are in press.
- Former VIP Campus Partner at Perplexity AI.

## Featured projects

### [ARGUS](https://github.com/RishabhCodezZz/ARGUS)

An 11-agent financial due-diligence system built with Google ADK and Gemini. It traces numerical claims back to their sources and pauses for human review when confidence is too low.

![ARGUS demo](https://github.com/RishabhCodezZz/ARGUS/raw/HEAD/demo.gif)

- Computes financial metrics by executing pandas code. Contradiction detection and the release gate run without LLM calls.
- Checks each stated figure against its source with a mechanical claim-matcher.
- Evaluated on 8 scenarios using 4 deterministic metrics, with ablation outputs committed. Removing code execution preserved groundedness but removed derived analysis.
- 156 tests. Evaluation uses two fictional companies; performance on real filings remains untested.

### [GateKeep](https://github.com/RishabhCodezZz/GateKeep)

A document-question-answering project I built to learn how Laya can handle decisions inside a RAG pipeline. I fine-tuned four gates and connected them through LangGraph: routing the question, checking passage relevance, checking grounding, and checking whether the answer addresses the question.

- Built the pipeline from PDF parsing and FAISS retrieval through reranking, answer generation, query rewriting and bounded retries.
- Implemented interchangeable backends for a TF-IDF baseline, LLM judges, zero-shot Laya, fine-tuned Laya and a confidence-based Laya-to-Gemma cascade.
- On 343 held-out questions, the Laya-gated pipeline scored 92.1% correctness versus 91.5% for LLM gates, using about 1.5 total LLM calls per question versus 10.9. Laya handled every gate locally in that variant; Gemma still wrote the answers.
- Added a local web demo that searches the book and scikit-learn documentation together, shows supporting passages, and traces which checks Laya and Gemma performed.
- Reworked the router labels and calibration after the first experiments, then reran the evaluation. The repository keeps both rounds and the [full results and limitations](https://github.com/RishabhCodezZz/GateKeep/blob/HEAD/docs/RESULTS.md).

### [Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent) · [Live demo](https://meraki-ai-voice-agent.onrender.com)

A real-time voice agent connecting Deepgram speech-to-text, an Ollama LLM and Murf text-to-speech over one WebSocket. You can interrupt it while it speaks.

- Reduced time to first audio from 4.0 s to a 1.28 s median by synthesising clauses in parallel while the model continues writing. Measured over 10 runs on one machine, ranging from 0.86 to 2.48 s.
- Uses one cancellable `asyncio` task per turn. Added regression tests for two interruption bugs and a session-key leak found during review.
- 242 tests in CI. The hosted demo needs your own free-tier API keys and can take up to a minute to wake after being idle.

## More projects

### [Arbiter](https://github.com/RishabhCodezZz/Arbiter)

A fraud decision system that chooses allow, step-up or block by the expected rupee cost of each action.

- Combines XGBoost and LightGBM with Platt calibration. On 92,427 transactions from a held-out test month in IEEE-CIS, the estimated benefit over a no-system baseline was ₹1.678 crore (95% CI: ₹1.51–1.85 crore). This is an offline estimate under stated cost assumptions, with dataset amounts converted from USD to INR.
- XGBoost achieved 3.65× the PR-AUC of `gpt-oss:20b` at about 60× lower latency. The LLM writes explanations; the decision engine runs independently.
- Uses time-based splits, a replayable and tamper-checked audit log, and fails closed if a model file is missing. 105 tests. Solo build.

| Project | What I built | Evaluation |
|:---|:---|:---|
| [CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection) | Audio-visual deepfake detection tested on unseen datasets. | Mean zero-shot AUC improved from about 0.61 to 0.855 on DFDC and Celeb-DF using a CLIP backbone pretrained on FaceForensics++. Single seed, bootstrap intervals, identity-disjoint splits and 47 tests in CI. |
| [NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG) | A multilingual RAG diet assistant supporting English, Hindi and Telugu, with allergy and condition checks. | A 48-case evaluation recorded recall@5 of 0.32, a 9.0% hallucination rate and no observed safety violations. |

<details>
<summary>More on the CrossFuse experiments</summary>

My earlier EfficientNet-B4 model scored 0.95 AUC in-domain and about 0.61 on unseen datasets. About 97% of its training fakes were Wav2Lip lip-sync videos, while DFDC and Celeb-DF contain full-face swaps. The ablation points to FaceForensics++ pretraining as the main factor behind the improvement, though it uses one seed and one arm differs in learning rate. The repository also records the approaches that did not help: self-blended-image pretraining, a lip-sync head that stayed at chance, and a multi-GPU setup that ran about 3× slower.

</details>

## Open source

- [Docling · PR #3949](https://github.com/docling-project/docling/pull/3949), merged: fixed missing hyperlinks in ODT paragraphs, headings and list items, with edge-case tests across three review revisions.
- [Feast · PR #6772](https://github.com/feast-dev/feast/pull/6772), under review: fixes remote-mode table provisioning after `feast apply`, adding two feature-server endpoints and an end-to-end lifecycle test.

## Skills

- Python, asyncio, FastAPI, WebSockets, pytest and GitHub Actions.
- PyTorch, scikit-learn, XGBoost, LightGBM, Hugging Face, LangGraph and Google ADK.
- Also used JavaScript, React, Flask, ChromaDB, Optuna, SHAP and Render.
- Model and voice services: Gemini, Ollama Cloud, Deepgram and Murf.
