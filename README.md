# 🎵 Whisper-TimestampedLyrics-Pipeline
A lightweight, fully local pipeline for transcribing music audio into timestamped lyrics using OpenAI Whisper — no API keys, no data upload, no cost.
Built as a personal exploration of vibe coding: deploying an open-source ML model end-to-end without a traditional engineering background.
## What it does
Takes any audio file (.m4a, .mp3, .wav, etc.) as input
Transcribes speech/vocals using OpenAI's Whisper ASR model (run locally)
Outputs a .lrc file with line-level timestamps, ready for any LRC-compatible music player
All processing happens on your machine — audio never leaves your device
## Why local deployment matters
Most transcription tools send your audio to a remote server. For music content pipelines — where licensing and data sovereignty matter — local inference is the only viable approach.
This pipeline uses faster-whisper, a CTranslate2-optimised reimplementation of Whisper that runs efficiently on CPU, making it accessible without GPU hardware.
## Quickstart

### 1. Prerequisites

- macOS (tested on macOS Tahoe 26)
- Python 3.11
- ffmpeg

Install ffmpeg on Mac:
```bash
brew install ffmpeg
```

### 2. Install dependencies

```bash
pip3 install faster-whisper
```

### 3. Run the pipeline

```bash
python3 -c "
from faster_whisper import WhisperModel

model = WhisperModel('small', device='cpu')
segments, _ = model.transcribe(
    'your_audio_file.m4a',
    language='zh'        # change to your target language
)

with open('output.lrc', 'w', encoding='utf-8') as f:
    for segment in segments:
        minutes = int(segment.start // 60)
        seconds = segment.start % 60
        f.write(f'[{minutes:02d}:{seconds:05.2f}]{segment.text.strip()}\n')

print('Done — output saved to output.lrc')
"
```

Replace `your_audio_file.m4a` with your audio path and set `language` to your target language code (e.g. `zh`, `en`, `vi`, `id`).

---


## Output format
The pipeline generates standard .lrc format:
```
[00:03.20] lyrics
[00:08.45] lyrics
[00:13.10] lyrics
```
Compatible with most music players, karaoke apps, and lyrics display systems.

---
## Model options

| Model | Size | Speed | Accuracy | Best for |
|-------|------|-------|----------|----------|
| `tiny` | ~75MB | fastest | lowest | quick drafts |
| `small` | ~500MB | fast | good | general use ✅ |
| `medium` | ~1.5GB | moderate | better | production |
| `large-v3` | ~3GB | slow | best | high accuracy needs |

For multilingual music content, `small` offers the best speed/accuracy tradeoff.

---

## Supported languages

Whisper supports 99 languages natively, including:

- Chinese (`zh`)
- English (`en`)
- Vietnamese (`vi`)
- Indonesian (`id`)
- Thai (`th`)
- Japanese (`ja`)
- Korean (`ko`)
- Malay (`ms`)

No per-language fine-tuning required — zero-shot multilingual transcription out of the box.

---

## Use cases

- **Music platforms**: batch-generate localised lyrics for multilingual catalogues
- **Content operations**: automate lyrics ingestion pipelines at scale
- **Research**: analyse vocal patterns or lyrics across large audio datasets
- **Personal**: generate synced lyrics for your own music library

---

## Limitations

- Accuracy varies with audio quality, background music volume, and vocal clarity
- Not optimised for heavily produced tracks where vocals are mixed low
- `small` model may struggle with strong accents or dialect-heavy speech — use `medium` or `large-v3` for higher accuracy requirements

---

## Background

This project was built as part of an exploration into vibe coding — using AI-assisted iteration to deploy an ML pipeline end-to-end without a formal engineering background. The goal was to close the loop independently: from problem identification, to tool selection, to local deployment and output validation.

The underlying use case comes from real-world music content operations: at scale, manual lyrics localisation is a significant bottleneck. Automating it with a locally-deployed ASR model eliminates per-song cost, removes external data dependencies, and enables throughput that manual workflows cannot match.

---

## Tech stack

- [faster-whisper](https://github.com/SYSTRAN/faster-whisper) — optimised Whisper inference
- [OpenAI Whisper](https://github.com/openai/whisper) — underlying ASR model
- Python 3.11
- ffmpeg

---

## License

MIT — do whatever you want with it.

---

*Contributions, issues, and forks welcome.*



