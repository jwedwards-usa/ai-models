# AI Models

**GitHub Pages:** https://jwedwards-usa.github.io/ai-models/

A small distribution repository for AI model artifacts that are useful in offline workflows.

## OpenAI Whisper `small.en`

This repository includes a manually triggered GitHub Actions workflow that:

1. Resolves OpenAI Whisper's current official `small.en` model URL from the upstream `openai/whisper` repository.
2. Uses the SHA-256 fingerprint embedded in that URL as the model version.
3. Checks whether that exact model version has already been published here.
4. Downloads and verifies the checkpoint only when a new model fingerprint is available.
5. Packages the verified `small.en.pt` weights, checksum, and manifest in an easy-to-find ZIP file.
6. Publishes the ZIP as the latest GitHub Release asset.

The stable download URL is:

`https://github.com/jwedwards-usa/ai-models/releases/latest/download/openai-whisper-small-en-offline-model.zip`

> The ZIP contains model weights, not the Whisper runtime. For fully offline transcription, install/cache a Whisper-compatible runtime and its dependencies (for example Python, `openai-whisper`, PyTorch, and FFmpeg) before disconnecting from the network.

## Run the model update manually

Open **Actions → Update Whisper small.en offline model → Run workflow**.

The updater is intentionally `workflow_dispatch` only. Re-running it is safe: if the upstream `small.en` model fingerprint matches a release already published in this repository, the workflow exits without downloading or publishing the checkpoint again.

## GitHub Pages

Visit the published site at **https://jwedwards-usa.github.io/ai-models/**.

The static site lives in [`docs/`](docs/) and is deployed by a separate Pages workflow. It includes:

- Search-friendly HTML metadata and canonical URLs.
- Schema.org `Dataset` / `DataDownload` structured data.
- `robots.txt` and `sitemap.xml`.
- `llms.txt` and `llms-full.txt` for LLM-oriented discovery.
- `model.json` with machine-readable download and usage metadata.

If Pages has not been enabled for this repository before, set **Settings → Pages → Build and deployment → Source → GitHub Actions** once.

## Upstream

Whisper is maintained by OpenAI at `openai/whisper`. The `small.en` model is the English-only Small Whisper checkpoint (approximately 244M parameters).

This repository does not modify the model weights; it verifies and repackages the upstream artifact for convenient offline caching and discovery.
