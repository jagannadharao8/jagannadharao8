# Vision restoration work — 23 November 2026

This continues the [dataset and provider follow-up](verification-2026-11-23.md).

## Published source changes

The misinformation assistant now supports VISION_PROVIDER=auto, groq or gemini. Automatic selection tries the existing Groq credential with qwen/qwen3.8-27b before Gemini, so a Gemini outage does not by itself stop every vision request. It uses configured credentials; no key value is embedded in the source.

Both image-only and text/image entry points use this selection. Images are resized for bounded provider input. The application validates labels and finite, nonnegative probability values, rejects malformed responses and retains a safe unavailable/Uncertain path if providers fail. Successful results record the actual provider and model.

The interface shows completed versus unavailable image assessment and the selected service. Mismatch flags use the actual response label, and provider metadata is rendered as text.

[Published implementation](https://github.com/jagannadharao8/Fake-news-detection-using-GENAI-ML-DL-XAI/pull/6).

## Verification

Twenty-seven API/configuration/SDK tests passed. They cover both public prediction paths, provider selection and fallback, invalid-response rejection, status handling, real-SDK request payloads using mock transports, retry limits and private-error redaction. The vision UI tests passed for no-image, unavailable, assessed mismatch and safe metadata rendering.

[Passing CI and UI checks](https://github.com/jagannadharao8/Fake-news-detection-using-GENAI-ML-DL-XAI/actions/runs/45208092078).

Live verification of the matching deployment, image-only input and matching/mismatching text-image inputs is pending. Offline/mock-provider tests alone do not demonstrate production provider access.

## Account settings

The [exact bio, website, location and pin order](github-account-update-plan.md) are prepared. TinyFish is installed and enabled, but its browser controls are not yet exposed in this chat. Account-level changes have not been applied or verified.
