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
