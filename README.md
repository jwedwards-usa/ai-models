# ai-models

https://jwedwards-usa.github.io/ai-models/

Whisper `small.en` model files for local use.

## FILES

- `ggml-small.en.zip` — preferred whisper.cpp download
- `ggml-small.en.zip.sha256` — ZIP checksum
- `ggml-small.en.bin` — raw whisper.cpp model
- `ggml-small.en.bin.sha256` — model checksum
- `ggml-small.en.manifest.json` — conversion provenance
- `openai-whisper-small-en-offline-model.zip` — verified `small.en.pt` package

Stable URLs:

```text
https://github.com/jwedwards-usa/ai-models/releases/latest/download/ggml-small.en.zip
https://github.com/jwedwards-usa/ai-models/releases/latest/download/ggml-small.en.bin
https://github.com/jwedwards-usa/ai-models/releases/latest/download/openai-whisper-small-en-offline-model.zip
```

## USAGE

```sh
unzip ggml-small.en.zip
whisper-cli -m ggml-small.en.bin -f audio.wav
```

Runtime binaries are not included.

## UPDATE

Run **Actions → Update Whisper small.en → Run workflow**.

The workflow is manual-only. It verifies the OpenAI checkpoint, converts it when needed, publishes release assets, and refreshes:

```text
openai-whisper-small-en-ggml-<model-sha-prefix>
```

Existing releases are reused.

## CHATGPT

https://jwedwards-usa.github.io/ai-models/chatgpt-prompt.txt

## SOURCE

- https://github.com/openai/whisper
- https://github.com/ggml-org/whisper.cpp
