<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  AI/ML engineering, backend systems, and evaluation
</p>

<p align="center">
  I build AI applications and test them: streaming APIs, retrieval, agents, and the evals around them.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rishabhk11/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:rishabhsanu11@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://leetcode.com/rishabhk_11"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
</p>

Final-year B.Tech CSE (AI & ML) student at B.V. Raju Institute of Technology, Hyderabad, graduating May 2027. Looking for SDE and AI/ML internships now, and full-time roles from mid-2027.

- Merged a fix into [Docling](https://github.com/docling-project/docling/pull/3949); a Feast fix is under review.
- Presented a paper at CML 2026 (Springer proceedings, in press). <!-- TODO: add the paper title -->
- Former VIP Campus Partner at Perplexity AI. <!-- TODO: confirm the exact title you want to use -->

## Featured projects

### [Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent) · [Live demo](https://meraki-ai-voice-agent.onrender.com)

A real-time voice agent: Deepgram speech-to-text, an Ollama LLM and Murf text-to-speech over one WebSocket. You can talk over it and it stops and listens.

- First audio dropped from 4.0 s to a 1.28 s median (10 runs, 0.86 to 2.48 s, one machine), by cutting replies at the first clause and synthesising chunks in parallel while the model keeps writing.
- Interruption cancels one `asyncio` task per turn. Code review caught two barge-in bugs and a session-key leak, and each now has a regression test.
- 242 tests in CI. The demo needs your own free-tier API keys, and the hosted instance sleeps when idle, so the first load can take up to a minute.

<!-- TODO: add a 20-30 second screen recording of Meraki here, e.g. ![Meraki demo](path-to-gif) -->

### [Arbiter](https://github.com/RishabhCodezZz/Arbiter)

A fraud decision system. Instead of a score, it picks allow, step-up or block per transaction by the expected rupee cost of each action.

- On 92,427 held-out test-month transactions (IEEE-CIS, split by time), the estimated benefit is ₹1.678 crore over a no-system baseline (95% CI ₹1.51 to ₹1.85 crore). This is an offline estimate that depends on the cost assumptions, not realised savings, and dataset amounts were converted from USD to INR.
- XGBoost + LightGBM ensemble, calibrated with Platt scaling (isotonic was tried and rejected for collapsing scores).
- XGBoost scored 3.65x the PR-AUC of `gpt-oss:20b` at about 60x lower latency, so the LLM only writes the explanation and removing it leaves every decision unchanged. Refusing to use future data cost only 0.0066 PR-AUC.
- Audit log is replayable and tamper-checked, and the engine fails closed if a model file is missing. 105 tests. Solo build.

### [ARGUS](https://github.com/RishabhCodezZz/ARGUS)

An 11-agent financial due-diligence system on Google ADK and Gemini. Every number in an answer is traced back to a source.

![ARGUS demo](https://github.com/RishabhCodezZz/ARGUS/raw/HEAD/demo.gif)

- Financial metrics come from executed pandas code, not model arithmetic. Contradiction detection and the release gate make no LLM calls.
- A mechanical claim-matcher scores every stated figure. Below the confidence bar, the run pauses for a human.
- Evaluated on 8 scenarios with 4 deterministic metrics, plus an ablation with the raw output committed. Removing code execution kept groundedness at 1.00 but removed all derived analysis, so answers stayed accurate and got shallower.
- The test data is two fictional companies, so these scores show the pipeline works, not how it performs on real filings. 156 tests.

## More projects

| Project | What it is | What I found |
|:---|:---|:---|
| [CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection) | Audio-visual deepfake detection, aimed at generalising to unseen datasets. | Mean zero-shot AUC went from about 0.61 to 0.855 on DFDC and Celeb-DF after switching to a CLIP backbone pretrained on FaceForensics++. Single seed, bootstrap CIs, identity-disjoint splits, 47 tests in CI. |
| [GateKeep](https://github.com/RishabhCodezZz/GateKeep) | Tests whether a small fine-tuned model can make the judgment calls inside a RAG pipeline (route, grade, grounded, sufficient) instead of an LLM. | The 421M-parameter model beat Gemma 31B on 3 of 4 gates at roughly 10x lower latency, and a pipeline using it made 1.5 LLM calls per question instead of 10.9 with no significant difference in correctness. A no-gates baseline still scored higher, so the gates did not pay off here. |
| [NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG) | A multilingual RAG diet assistant (English, Hindi, Telugu) with allergy and condition safety checks. | On a 48-case suite: recall@5 0.32, hallucination rate 9.0%, no safety violations. The retrieval numbers are modest and the corpus is small. |

<details>
<summary>Notes on CrossFuse and GateKeep</summary>


**CrossFuse.** My earlier EfficientNet-B4 model scored 0.95 AUC in-domain but about 0.61 on unseen datasets, because about 97% of its training fakes were Wav2Lip lip-sync videos while DFDC and Celeb-DF contain full-face swaps. The ablation points to the FaceForensics++ pretraining as the main factor, but it uses one seed and one arm differs in learning rate, so I treat that as a hypothesis. Negative results are kept in the repo: self-blended-image pretraining, a lip-sync head that stayed at chance, and a multi-GPU setup that ran about 3x slower.

**GateKeep.** Built on LangGraph and evaluated on 343 questions from held-out chapters, with the success criteria written before the runs. The latency figures come from different hardware (Kaggle T4 for the small model, a network API for Gemma), so the speed ratio is indicative. The first round had five methodology mistakes, including training rows duplicated into the calibration slice. I found them, fixed them and re-ran, and both rounds are in the repo.

</details>

## Open source

**[Docling](https://github.com/docling-project/docling)** · [PR #3949](https://github.com/docling-project/docling/pull/3949) · merged. Fixed hyperlinks missing from ODT paragraphs, headings and list items, with edge-case tests, across three review revisions.

**[Feast](https://github.com/feast-dev/feast)** · [PR #6772](https://github.com/feast-dev/feast/pull/6772) · under review. Fix for remote-mode table provisioning after `feast apply`, adding two feature-server endpoints and an end-to-end lifecycle test.

## Skills

**Strongest:** Python, asyncio, FastAPI, WebSockets, pytest, GitHub Actions, scikit-learn, XGBoost, LightGBM, PyTorch  
**Also used:** JavaScript and React, Flask, Hugging Face, LangGraph, Google ADK, ChromaDB, Optuna, SHAP, Render  
**Services:** Gemini, Ollama Cloud, Deepgram, Murf
