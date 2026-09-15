# AI Models

**GitHub Pages:** https://jwedwards-usa.github.io/ai-models/

**Direct whisper.cpp model:** https://github.com/jwedwards-usa/ai-models/releases/latest/download/ggml-small.en.bin

**Direct PyTorch model ZIP:** https://github.com/jwedwards-usa/ai-models/releases/latest/download/openai-whisper-small-en-offline-model.zip

A small distribution repository for verified AI model artifacts that are useful in offline workflows.

## OpenAI Whisper `small.en`

This repository provides the same verified OpenAI Whisper `small.en` weights in two useful forms:

- `small.en.pt` inside `openai-whisper-small-en-offline-model.zip` for the Python/OpenAI Whisper runtime.
- `ggml-small.en.bin` for the official `whisper.cpp` runtime and `whisper-cli`.

The manually triggered GitHub Actions workflow:

1. Resolves OpenAI Whisper's current official `small.en` model URL from the upstream `openai/whisper` repository.
2. Uses the SHA-256 fingerprint embedded in that URL as the model version.
3. Checks whether that exact model version has already been published here before downloading the large upstream checkpoint.
4. Downloads and verifies `small.en.pt` only when a new model fingerprint is available.
5. For a new model, packages the verified checkpoint into the stable PyTorch ZIP.
6. Converts the verified checkpoint with the official `ggml-org/whisper.cpp` `models/convert-pt-to-ggml.py` converter and records the exact `whisper.cpp` commit used.
7. Publishes `ggml-small.en.bin`, its SHA-256, and conversion manifest as GitHub Release assets.
8. Uploads the GGML model as a GitHub Actions artifact so GitHub API/connector clients can retrieve it even when ordinary release-asset transport is unavailable.

For an older release that already has the verified PyTorch ZIP but does not yet have GGML assets, the workflow performs a one-time backfill from that existing ZIP instead of downloading the upstream checkpoint again.

## Stable download URLs

### whisper.cpp / `whisper-cli`

Model:

`https://github.com/jwedwards-usa/ai-models/releases/latest/download/ggml-small.en.bin`

Checksum:

`https://github.com/jwedwards-usa/ai-models/releases/latest/download/ggml-small.en.bin.sha256`

Conversion provenance:

`https://github.com/jwedwards-usa/ai-models/releases/latest/download/ggml-small.en.manifest.json`

Example after the model and `whisper-cli` are available locally:

```bash
whisper-cli -m ggml-small.en.bin -f audio.wav
```

### Python / OpenAI Whisper

ZIP:

`https://github.com/jwedwards-usa/ai-models/releases/latest/download/openai-whisper-small-en-offline-model.zip`

ZIP checksum:

`https://github.com/jwedwards-usa/ai-models/releases/latest/download/openai-whisper-small-en-offline-model.zip.sha256`

> These assets contain model data, not a transcription runtime. For fully offline transcription, install/cache a compatible runtime and its dependencies before disconnecting from the network.

## Connector-friendly GitHub Actions artifact

Every successful manual workflow run uploads an Actions artifact named:

`openai-whisper-small-en-ggml-<first-12-characters-of-model-sha256>`

The artifact contains:

- `ggml-small.en.bin`
- `ggml-small.en.bin.sha256`
- `ggml-small.en.manifest.json`

It is retained for 90 days. If the model version has not changed, the workflow does **not** download `small.en.pt` again; it reuses the already-published GGML release asset to refresh this connector-friendly artifact.

## Run the model update manually

Open **Actions → Update Whisper small.en offline model → Run workflow**.

The updater is intentionally `workflow_dispatch` only. It never runs on pushes or on a schedule.

## GitHub Pages and LLM discovery

Visit **https://jwedwards-usa.github.io/ai-models/**.

The static site in [`docs/`](docs/) includes:

- Search-friendly HTML metadata and canonical URLs.
- A dedicated whisper.cpp / GGML discovery page.
- Schema.org structured data and stable direct-download URLs.
- `robots.txt` and `sitemap.xml`.
- `llms.txt` and `llms-full.txt` for LLM-oriented discovery.
- `model.json` with machine-readable PyTorch and GGML retrieval metadata.

## Upstream and provenance

The trained model originates from OpenAI's `openai/whisper` repository. The English-only `small.en` model has approximately 244 million parameters.

The GGML file is produced from the verified OpenAI checkpoint by the official converter in `ggml-org/whisper.cpp`. The conversion manifest records both the source model SHA-256 and the exact `whisper.cpp` commit used. This repository does not retrain or alter the learned model parameters; it verifies, packages, and converts their representation for convenient offline use.
