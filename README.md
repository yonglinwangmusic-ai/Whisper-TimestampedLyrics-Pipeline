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
## Why local deployment matters
Most transcription tools send your audio to a remote server. For music content pipelines — where licensing and data sovereignty matter — local inference is the only viable approach.
This pipeline uses faster-whisper, a CTranslate2-optimised reimplementation of Whisper that runs efficiently on CPU, making it accessible without GPU hardware.
## Quickstart
1. Prerequisites
- macOS (tested on macOS 13+) or Linux
- Python 3.11
- ffmpeg
Install ffmpeg on Mac:
、、、
brew install ffmpeg
、、、
2. Install dependencies
、、、
pip3 install faster-whisper
、、、
3. Run the pipeline
、、、
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
、、、
Replace your_audio_file.m4a with your audio path and set language to your target language code (e.g. zh, en, vi, id).
## Output format
The pipeline generates standard .lrc format:
、、、
[00:03.20]
[00:08.45]
[00:13.10]
、、、
Compatible with most music players, karaoke apps, and lyrics display systems.



