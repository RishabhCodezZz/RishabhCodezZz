<h1 align="center">Rishabh Kumar Yadav</h1>

<p align="center">
  Software engineering, AI/ML, and backend systems
</p>

<p align="center">
  I build AI applications and the software around them, from evals and retrieval to streaming APIs and deployment.
  I report what I measured, including results that came out worse than I expected.
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

Final-year B.Tech CSE (AI & ML) student at B.V. Raju Institute of Technology, Hyderabad, graduating May 2027. Looking for SDE and AI/ML internships now, and full-time roles from mid-2027.

- Merged a fix into Docling and proposed a remote-provisioning fix for Feast, now under review.
- Presented a paper at CML 2026 (Springer proceedings, in press).
- Former VIP Campus Partner at Perplexity AI.

## Featured projects

| Project | What it is | Evidence |
|:---|:---|:---|
| [ARGUS](https://github.com/RishabhCodezZz/ARGUS) | An 11-agent financial due-diligence system on Google ADK and Gemini. | 156 tests. An 8-scenario eval scored on 4 deterministic metrics, with ablation evidence committed to the repo. |
| [Meraki](https://github.com/RishabhCodezZz/Meraki-AI-Voice-Agent) · [Demo](https://meraki-ai-voice-agent.onrender.com) | A streaming voice agent: Deepgram, Ollama, and Murf over one WebSocket, with interruptible replies. | First audio went from 4.0 s to a 1.28 s median over 10 runs (0.86 to 2.48 s, one machine, measured on different days). 242 tests in CI. The demo needs your own API keys. |
| [Arbiter](https://github.com/RishabhCodezZz/Arbiter) | A fraud decision system that picks actions by their cost and benefit in rupees. | On 92,427 held-out transactions, an estimated ₹1.678 crore benefit over a no-system baseline (95% CI ₹1.51 to ₹1.85 crore). |

Arbiter's figure is an offline estimate that depends on the experiment's cost assumptions, not realized savings. Dataset amounts were converted from USD to INR.

<details>
<summary>How these were built and tested</summary>

### ARGUS

The eval has eight scenarios: focused queries, retrieval, broad analysis, contradictory evidence, missing-company recovery, and adversarial input. Clean runs reach 1.00 groundedness. In the ablation, removing code execution kept that score but removed the derived analysis, so answers stayed accurate and got shallower. Contradiction detection and the release gate make no LLM calls.

### Meraki

Latency came down one change at a time. Cutting the first chunk at a clause instead of a sentence took first audio from 4.0 s to 3.2 s, and Murf's streaming endpoint took it to about 1.4 s. The persona gives one-sentence replies, so a sentence-only rule meant generation and speech never overlapped.

I then changed the default model. `nemotron-3-nano` took 18 to 30 s to its first token, while `gemma4:31b` took about 0.5 s on the same API.

Barge-in cancels one `asyncio.Task` per turn. Code review found two bugs: playback waited for three queued chunks, and barge-in did nothing once generation had finished. Both now have tests, as does an earlier bug where a shared global could hand one session's API keys to another.

### Arbiter

Built solo. XGBoost scored 3.65x the PR-AUC of `gpt-oss:20b` on the same data with about 60x lower latency, so the LLM only writes the explanation. Removing it leaves every decision unchanged. Letting future information into the pipeline raised PR-AUC by only 0.0066, which is what refusing leakage costs.

</details>

## More projects

| Project | Focus | Result |
|:---|:---|:---|
| [CrossFuse](https://github.com/RishabhCodezZz/DeepFake-Detection) | Audio-visual deepfake detection and cross-dataset generalization. | Mean zero-shot AUC went from about 0.61 to 0.855 across DFDC and Celeb-DF. Single seed, bootstrap confidence intervals, 47 tests in CI. |
| [NutriBot](https://github.com/RishabhCodezZz/NutriBot-RAG) | A multilingual RAG diet assistant for English, Hindi, and Telugu. | 48 eval cases covering retrieval, factuality, numeric accuracy, and safety. No safety violations observed in that suite. |
| [Credit Risk](https://github.com/RishabhCodezZz/Credit-Risk-Detection) | Three-class credit-score prediction with a customer-leakage audit. | A random row split scored 0.8171 macro-F1 and a customer-grouped split scored 0.6974, a gap of 0.1197. |

<details>
<summary>Research and evaluation details</summary>

### CrossFuse

My earlier EfficientNet-B4 model scored 0.95 AUC in-domain but about 0.61 zero-shot on unseen datasets. Roughly 97% of its training fakes were Wav2Lip lip-sync videos, while DFDC and Celeb-DF contain full-face swaps.

The updated pipeline uses a CLIP ViT-L/14 backbone pretrained on FaceForensics++ with LayerNorm-only tuning. Zero-shot AUC is 0.865 on DFDC and 0.845 on Celeb-DF. The ablation points to pretraining as the main factor, but it uses one seed and one arm differs in learning rate, so I treat that as a hypothesis.

Splits are identity-disjoint, enforced by assertions. I also kept three negative results: self-blended-image pretraining, a lip-sync head that stayed at chance, and a multi-GPU setup that ran about 3x slower.

### NutriBot

Retrieval uses `all-mpnet-base-v2` with cross-encoder reranking. The 48-case suite measures recall@5/10, precision, MRR, nDCG@10, hallucination rate, numeric accuracy, safety violations, and LLM-judged faithfulness and relevance. The safety checks include foods that conflict with a stated allergy even when they appear in the retrieved context. The judge runs on a different provider from the generator. The result covers only those 48 cases.

### Credit Risk

Each customer appears about eight times, so a random row split can put the same customer in both training and evaluation data. The workflow uses causal `shift(1)` features, compares 10 variants on out-of-fold scores, and touches the holdout once. Two failed hypotheses are kept in the notebook.

</details>

## Open source

[Docling](https://github.com/docling-project/docling) · [PR #3949](https://github.com/docling-project/docling/pull/3949) · merged

Fixed hyperlinks missing from ODT paragraphs, headings, and list items. Added edge-case tests and addressed review feedback and coverage requirements across three revisions.

[Feast](https://github.com/feast-dev/feast) · [PR #6772](https://github.com/feast-dev/feast/pull/6772) · under review

Proposed a fix for remote-mode table provisioning after `feast apply`. Added two feature-server endpoints and an end-to-end lifecycle test to stop the materialization failures.

## Technical skills

Languages: Python, JavaScript, SQL  
Backend and applications: FastAPI, asyncio, WebSockets, React, MySQL  
Machine learning: PyTorch, scikit-learn, XGBoost, LightGBM, CatBoost, pandas, NumPy, Optuna, SHAP, OpenCV  
LLMs and retrieval: Google ADK, Gemini, Ollama, Hugging Face, ChromaDB  
Speech: Deepgram, Murf  
Testing and deployment: pytest, GitHub Actions, Git, GCP, Render
