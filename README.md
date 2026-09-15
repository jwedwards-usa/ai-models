# ai-models

Whisper `small.en` model files for local use.

## FILES

- `ggml-small.en.bin` — whisper.cpp / `whisper-cli`
- `ggml-small.en.bin.sha256` — GGML checksum
- `ggml-small.en.manifest.json` — conversion provenance
- `openai-whisper-small-en-offline-model.zip` — verified `small.en.pt` package
- `openai-whisper-small-en-offline-model.zip.sha256` — ZIP checksum

Stable URLs:

```text
https://github.com/jwedwards-usa/ai-models/releases/latest/download/ggml-small.en.bin
https://github.com/jwedwards-usa/ai-models/releases/latest/download/openai-whisper-small-en-offline-model.zip
```

## USAGE

```sh
whisper-cli -m ggml-small.en.bin -f audio.wav
```

Runtime binaries are not included.

## UPDATE

Run **Actions → Update Whisper small.en offline model → Run workflow**.

The workflow is manual-only. It verifies the OpenAI checkpoint SHA-256, converts it with the official whisper.cpp converter, publishes release assets, and uploads an Actions artifact named:

```text
openai-whisper-small-en-ggml-<model-sha-prefix>
```

Existing releases are reused; unchanged checkpoints are not downloaded or converted again.

## CHATGPT

Sample local-transcription prompt:

https://jwedwards-usa.github.io/ai-models/chatgpt-prompt.txt

Project page:

https://jwedwards-usa.github.io/ai-models/

## SOURCE

- https://github.com/openai/whisper
- https://github.com/ggml-org/whisper.cpp
