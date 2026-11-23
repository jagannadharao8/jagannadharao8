# Verification follow-up — 23 November 2026

This follow-up continues the [28 October audit](verification-2026-10-28.md). It records new provenance work and a fresh check of the unavailable vision integration.

## Completed: dataset provenance

The CSV in the income-classification project was compared with adult.data and adult.test from the official UCI Adult archive. After explicit column-name and formatting normalization, every one of its 48,842 row instances matched, including duplicate multiplicity. Both versions contain 48,790 unique rows.

- Source: https://archive.ics.uci.edu/dataset/2/adult
- Citation: Becker, B. & Kohavi, R. (1996). Adult [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5XW20.
- Licence stated by UCI: CC BY 4.0, https://creativecommons.org/licenses/by/4.0/
- Normalized full-record SHA-256: 6a07b01226845a861c786d71e2733b3bd3eef20789276e32bd5e347d84aea053.
- [Attribution, adaptations and methods](https://github.com/jagannadharao8/Employee-Salary-Prediction/blob/main/DATASET_ATTRIBUTION.md).
- [Committed comparison record and raw-file hashes](https://github.com/jagannadharao8/Employee-Salary-Prediction/blob/main/docs/data-provenance-verification.json).
- [Passing provenance and Python syntax check](https://github.com/jagannadharao8/Employee-Salary-Prediction/actions/runs/45198173161).

The method establishes corpus identity; it does not recover the original intermediate download history. The project pools UCI's original train/test records, then performs its documented deduplication and split. The previous held-out metrics remain tied to that project split.

## Completed: dashboard wording

The dashboard identifies the historical 1994 US Census source and includes attribution. The score distribution is labelled as uncalibrated model scores rather than confidence. Labels and exported CSV naming refer to census records and income classification. The dataset, fitted model and evaluation artifacts retain their previous content.

[Published change](https://github.com/jagannadharao8/Employee-Salary-Prediction/pull/3).

## Current vision integration

A fresh owner-side check found the Space running on cpu-basic. Its health endpoint returned HTTP 200. An image-only request returned HTTP 200 with visionAvailable=false and matching Uncertain verdict/card labels. The response demonstrates a safe fallback; it does not establish working image interpretation.

[Live runtime and image request evidence](https://github.com/jagannadharao8/Fake-news-detection-using-GENAI-ML-DL-XAI/actions/runs/45198018162).

The vision wrapper now classifies provider failures into controlled categories, status codes and exception types while omitting raw provider details. Nineteen API/configuration regressions passed, including checks that private error markers are excluded from logs.

- [19-test verification](https://github.com/jagannadharao8/Fake-news-detection-using-GENAI-ML-DL-XAI/actions/runs/45198845539).
- [Published diagnostic change](https://github.com/jagannadharao8/Fake-news-detection-using-GENAI-ML-DL-XAI/pull/4).

Final deployed-source identity and provider-category verification are pending. No secret value or raw owner runtime log is included in this report.

## Scope and remaining work

The October research-agent, portfolio and résumé verification remains recorded in the original audit; it is not presented here as a fresh November end-to-end test. The current task focused on the unresolved dataset and vision items.

1. Identify and repair the current vision provider failure, then verify actual image interpretation.
2. Account bio and pinned repositories still require GitHub's account interface because the connected repository tools do not expose those editing controls.
