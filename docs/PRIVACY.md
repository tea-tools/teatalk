# Privacy — what leaves your PC

TeaTools handles your microphone and your words, so here's the honest account of what stays on your machine and what gets sent out. Short version: **on the free default path, only your translated text leaves your PC, and only to your translation provider.**

## Translation — your text goes to your translation provider

To translate, TeaTalk has to send your recognized text to a translation service. Which one depends on the engine you've picked:

| Engine | What is sent, and to whom |
|---|---|
| **Microsoft Edge — the free default** | Your text is sent to Microsoft's Edge translation service. Keyless, no account. |
| **Google Translate (free)** | Your text is sent to Google Translate. This is also the **automatic fallback**: if the Edge service fails, TeaTalk retries the same line through Google so your words still reach the chatbox. |
| **OpenRouter (bring your own key)** | Your text is sent to OpenRouter (and on to the model you chose). Only used if you opt in by entering your own OpenRouter API key. |

Before your text is sent to *any* translation service, TeaTalk **masks out URLs and @mentions** and restores them afterward — so links and handles you say aren't shipped to the translator.

**Transcribe mode sends nothing to a translator.** It shows your own recognized words as-is, with no translation step.

## Speech-to-text — stays local by default

- **Local Whisper (the default)** runs entirely on your machine. Your audio never leaves your PC. It downloads a model file once (~148 MB) and then works offline.
- **OpenAI Whisper** is an optional bring-your-own-key upgrade. If you choose it, your **audio** is sent to OpenAI for transcription. It's off unless you enter an OpenAI key and select it.

## Ambient listening — opt-in, off by default

The hub's "ambient listening" feature (transcribing other people's audio) is **off out of the box**. It only runs if you explicitly turn it on. No module in this alpha uses it, so there's no reason to enable it today.

Your own microphone also only captures after you press **Start listening** — nothing is transcribed until you do.

## Telemetry / crash reports — opt-in, off unless you turn it on

TeaTools does **not** send usage or behavioral telemetry. The only optional uploads are diagnostic ones — crash reports, and problem reports you send yourself — and they are **opt-in**: on first run you're asked once, and declining (or never being asked) means everything stays **local-only**. No account or identifier is attached to an upload, but diagnostic uploads (crash reports and problem reports) may include file paths from your PC in logs and error messages. You can change the choice any time on **Home → About**.

## Your API keys — encrypted on disk when Windows can

If you enter an OpenRouter or OpenAI key, it's stored **encrypted at rest using Windows DPAPI**, tied to your Windows user account, and masked in the UI. When Windows can't do that encryption, TeaTools saves the key as plain text rather than lose it — and that isn't limited to unusual setups, it can happen on an ordinary Windows PC. Either way the file never leaves your PC, and the key itself only ever goes to the provider you chose; a plain-text key just isn't protected from anything else on the machine that can read your files. In `%APPDATA%\TeaTools\logs`, TeaTools records which way a key ended up stored. There's one log file per day, named with its date — `teatools20260821.log`, for example — so open the newest and search it for `TeaTalk API key storage:`; the phrase sits mid-line after the timestamp, not at the start of the line. It says what happened to your key once per run, and never contains the key itself. Nothing in the app shows you — the log is the only place it's stated.

## In one line

Free default = local speech recognition + text sent only to Microsoft/Google to translate; audio stays on your PC; no telemetry; ambient listening off. Everything that sends more (cloud speech-to-text, OpenRouter) is an explicit opt-in you turn on yourself.
