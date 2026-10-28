# Project verification — 28 October 2026

Scope: the five connected repositories owned by jagannadharao8: research assistant, misinformation assistant, income classifier, portfolio and profile. The deleted photo-studio project was excluded.

## Research assistant

| Check | Result |
| --- | --- |
| Normal question in the deployed Streamlit interface | Passed |
| Markdown, Word and PDF downloads | Passed; DOCX and PDF text extraction checked |
| Clear session | Chat and last report cleared |
| Web retrieval | Answer, web mode and citation rendered |
| Document A | Correct synthetic fact returned using TF-IDF; numeric citation formatting correction prepared |
| Two-document isolation after citation correction | Final hosted verification pending |
| Provider errors | Sanitised failures; empty/truncated answers are not treated as successful cached reports |
| Shared cache | Replaced in the UI with a bounded session-private cache keyed by query, document digest, recent conversation and model |
| Code execution | Disabled in the legacy subprocess helper; not offered by the interface |

The default hosted retrieval method is TF-IDF lexical ranking. FAISS/MiniLM semantic retrieval is explicitly available with RETRIEVAL_BACKEND=faiss for a host with adequate memory and model-download access. Lexical ranking can miss paraphrases. The interface labels the actual method.

GPT-OSS calls reserve reasoning/completion capacity, use low reasoning effort and permit one bounded retry on token exhaustion. Clear numeric citation brackets are normalised before checking identifiers. Source support is a model-assisted heuristic, not calibrated confidence or proof of truth. The optional knowledge graph remains experimental.

Evidence:
- [Real application-query provider checks](https://github.com/jagannadharao8/ai-research-agent/actions/runs/40712070700).
- [25-test lexical/semantic-path regression suite](https://github.com/jagannadharao8/ai-research-agent/actions/runs/40715079641).
- [Hosted answer, download, web and first-document check](https://github.com/jagannadharao8/jagannadharao8.github.io/actions/runs/40716652423). Its overall result failed at citation format; the individual completed checks above are recorded in its logs.

## Misinformation evidence assistant

| Check | Result |
| --- | --- |
| Health endpoint | HTTP 200 |
| Empty input | HTTP 400 |
| URL fetching | HTTP 400; paste text instead |
| Malformed PDF | HTTP 400 |
| Valid synthetic PDF | HTTP 200 with matching Uncertain verdict and evidence card |
| Unsupported synthetic text claim | HTTP 200; matching Uncertain label and no confidence percentage |
| Shared public history | HTTP 410; new submissions are not persisted by this API |
| Image-only and text-plus-image inputs | HTTP 200 with conservative uncertainty; actual cloud vision unavailable |
| Vision configuration | Explicit GEMINI_API_KEY selection and configurable GEMINI_MODEL; provider access still needs owner repair |
| Continuous deployment | Runtime-only upload preserves valid Docker Space metadata, existing model artifacts and private settings |

API verdicts and evidence cards share one policy. Local text-classifier probabilities cannot establish real-world truth. The system abstains when evidence is missing, weak, conflicting or unavailable. Text attribution explains the local classifier rather than the top-level evidence verdict.

[Deployed PDF/image input checks](https://github.com/jagannadharao8/jagannadharao8.github.io/actions/runs/40716918643) show safe image fallback; they do not demonstrate successful image interpretation.
[17-test API/configuration suite](https://github.com/jagannadharao8/Fake-news-detection-using-GENAI-ML-DL-XAI/actions/runs/40716493350).

The remaining cloud-vision blocker is provider credential/account access. Rebooting or changing repository code cannot grant provider permission. Configure access privately in the existing Space settings, then repeat the image tests.

## Income classifier

The application classifies census income above or at most $50K. It does not estimate a numerical salary.

| Evidence | Verified value |
| --- | --- |
| Selected model | XGBoost |
| Training-only cross-validation ROC-AUC | 0.9228 |
| Held-out ROC-AUC | 0.9207 |
| Held-out accuracy | 85.29% |
| Train/test rows | 39,032 / 9,758 |
| Higher-income precision / recall / F1 | 0.6680 / 0.7667 / 0.7140 |
| Saved model | Reloaded and reproduced held-out ROC-AUC |
| SHAP | Generated for the selected tree model |
| Persistent artifacts | model.joblib, evaluation.json, heldout.csv, model.sha256 and plots committed |

[Reproducible evaluation and model reload](https://github.com/jagannadharao8/Employee-Salary-Prediction/actions/runs/40697955712).
The model SHA-256 is 6be6615b00a9420a010855b02e397b02ee0d689a4a9460835f9615801306145b.

Preprocessing and SMOTE sit inside training folds; test labels are not used to choose the model. Dashboard agreement on displayed rows includes training records and is labelled separately. SMOTE can interpolate one-hot indicators. Dataset origin/licensing provenance still needs independent documentation. These results apply to this split and do not justify using the demo for hiring or compensation decisions.

The old presentation outline was replaced with the current protocol, metrics and limitations. Historical slides, screenshots, certificates and notebooks are retained as learning records rather than current benchmark evidence. No new public income-classifier deployment was created.

## Portfolio, résumé and profile

- Refreshed portfolio and one-page résumé PDF are published on GitHub Pages.
- Desktop heading, mobile navigation, 390/768/1440-pixel overflow checks and JavaScript-error checks passed in the relevant QA runs.
- The résumé PDF has selectable text and includes the held-out income result.
- Removed unsupported percentage gains and corrected virtual-programme attribution. Education and internship history remain user-supplied.
- GitHub profile README presents three selected projects with scoped evidence.
- GitHub account bio, pinned repositories and sidebar settings were not changed: those account-editing controls are absent from the connected tools.

[Portfolio and résumé rendering checks](https://github.com/jagannadharao8/jagannadharao8.github.io/actions/runs/40713366781).

## Source inspection

Automated checks covered 100 source/configuration text files across the four code repositories, plus review of the profile README. Python syntax checks passed. No matches were found for the common embedded Groq, Hugging Face, Google or GitHub credential patterns included in the scan. Updated runtime changes were also checked in project CI. Secret values were not printed.

## Remaining actions

1. Finish the hosted two-document check after numeric citation normalisation; record its outcome here.
2. Repair Gemini provider credential/account access in the existing Space, then verify actual image interpretation.
3. Update account bio/pins manually if desired; the profile README is already published.
4. Keep interview claims tied to the current source, evaluation protocol and verified runtime behavior.
