# TeaTalk

**TeaTalk turns your speech into VRChat chatbox text** — either translated into another language, or transcribed as-is. It's the module TeaTools ships with, and it works for free with no account and no API key.

These pages are for **using** TeaTalk. If you want to build your own module against the TeaTools hub, developer/module-author docs aren't part of this public docs set yet — ask on the **[TeaTools Discord](https://discord.gg/GUdBNfXfbe)**.

## Start here

| If you want to… | Read |
|---|---|
| Get talking in your chatbox in 5 minutes | [Getting started](getting-started.md) |
| Understand translate vs. transcribe, engines, and mute options | [User guide](guide.md) |
| Look up what a specific setting does | [Settings reference](settings-reference.md) |
| Fix something that isn't working | [Troubleshooting](troubleshooting.md) |

## What TeaTalk is (and isn't)

- **It is** a module that reads your microphone and writes to the VRChat chatbox.
- **It uses** the hub's shared microphone/transcription — it doesn't own your mic. Capture device and voice-detection sensitivity are set once for the whole app under **Home → General → Audio capture**, not inside TeaTalk.
- **It is free by default.** The out-of-the-box path (local Whisper speech-to-text + Microsoft Edge translation) costs nothing and needs no key. API keys are optional power-user upgrades, tucked in Settings.

## What you need

- Windows
- VRChat running, with **OSC enabled** (see [Getting started](getting-started.md))
- A microphone

That's the whole list for the free path.
