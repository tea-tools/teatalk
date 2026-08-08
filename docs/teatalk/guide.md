# TeaTalk user guide

Everything TeaTalk does, and when to reach for each option. For a plain list of every setting, see the [settings reference](settings-reference.md).

## Modes

TeaTalk has two modes. You switch between them from the toggle on the main panel, live, mid-session.

### Translate (default)

Speech (or typed text) → translated → chatbox. Your original words and the translation can both be shown, in the order you choose (see [chatbox format](#chatbox-format)). This is the default mode when you open TeaTalk.

### Transcribe

Speech → the same words, as text → chatbox. **No translation engine is used at all** — your recognized speech goes straight to the chatbox. Reach for this when you just want your own voice as captions (accessibility, voice-typing, a loud room), not a translation.

> Only Translate mode does AI/cloud translation, so only Translate mode sends your text to a translation service. Transcribe keeps everything local to the speech engine you chose.

## Engines

TeaTalk separates **speech-to-text** (turning your voice into words) from **translation** (turning those words into another language). Each has a free default and optional paid upgrades.

### Speech-to-text engines

| Engine | Cost | Needs a key? | Notes |
|---|---|---|---|
| **Local Whisper** *(default)* | Free | No | Runs on your machine. Downloads a model once (~142 MB for the default **Base** size). No internet needed after that. |
| **OpenAI Whisper** | Paid (your OpenAI usage) | Yes — OpenAI key | Cloud transcription. A power-user option; the free local engine is enough for most people. |

For local Whisper you can pick a model size — **Tiny** (~75 MB, fastest, least accurate), **Base** (~142 MB, the default balance), or **Small** (~488 MB, most accurate, slower). Bigger = more accurate and more download.

### Translation engines

| Engine | Cost | Needs a key? | Glossary? |
|---|---|---|---|
| **Edge Translate** *(default)* | Free | No | No |
| **Google Translate** | Free | No | No |
| **OpenRouter LLM** | Paid (your OpenRouter usage) | Yes — OpenRouter key | Yes |

The two free engines cover the vast majority of language pairs at zero cost. **Edge Translate** (Microsoft's translator) is the default — keyless and zero-setup; if it ever hiccups, TeaTalk automatically falls back to Google for that line so your message still gets through. **OpenRouter** routes translation through a large language model of your choice for higher-quality, context-aware translation — it's the "bring your own key" upgrade.

#### Using OpenRouter

Choose **OpenRouter LLM** as the translation engine in Settings and a small config section appears:

- **API key** — your OpenRouter key. It's masked in the UI and stored encrypted on disk (Windows DPAPI).
- **Model** — defaults to `openai/gpt-4o-mini`. The model box suggests options fetched from OpenRouter (voice-capable models are marked "Recommended"), but you can type any model id. Leave it blank to fall back to the default.
- **Temperature** — defaults to `0.3`. Lower is more literal; higher is more creative.
- **Base URL** — defaults to OpenRouter's endpoint. Leave it blank unless you're pointing at a compatible proxy.
- **Fall back to free translation if my model fails** — on by default. If OpenRouter errors out, TeaTalk retries once through free Google Translate so your line still reaches the chatbox, and warns you it did. Turn this off if you'd rather the line be dropped than sent through the free engine.

## Chatbox format

When you're translating, you decide what shows in the chatbox:

- **Original, then translation** *(default)* — your words, then the translation, on two lines.
- **Translation, then original** — the translation, then your words.
- **Translation only** — just the translation.

The translation is always kept in full; if the combined text is too long for VRChat's chatbox (144 characters), the **original** line is the one trimmed with an ellipsis, never the translation.

You can also:

- **Show a typing indicator** (on by default) — VRChat shows the "typing…" bubble while TeaTalk is preparing a line.
- **Turn on Live captions** (off by default) — your words appear in the chatbox while you speak, and the finished line settles in the same bubble when you stop. Early text is a best guess and can change. Captions only ever go to the chatbox, so the toggle is unavailable while Send to chatbox is off — and changing it while listening briefly pauses transcription.
- **Turn the chatbox off** entirely — TeaTalk still recognizes and translates (you'll see it in the app), but nothing is sent to VRChat.

## Mute behavior

This controls whether TeaTalk keeps working while you're **muted in VRChat**. It's a privacy decision, so the default is the safe one.

| Setting | What happens while you're muted in VRChat |
|---|---|
| **Pause transcribing** *(default)* | Stops transcribing while your VRChat mic is muted. Resumes when you unmute. Muted means muted. |
| **Ignore mute** | TeaTalk keeps transcribing and sending regardless of your VRChat mute state. |

Whether a spoken line counts as muted is decided at the moment you **start** speaking: a line you began while unmuted still sends even if you mute before it finishes (so push-to-talk works naturally), and a line you began while muted is dropped even if you unmute mid-sentence.

Typed messages always send either way — muting your mic never blocks typing.

> **Stay muted and talk only through text?** See [Staying muted](staying-muted.md) — how to speak into a mic for transcription while making certain your voice never transmits in VRChat.

## Glossary

The glossary is a list of terms you don't want changed — names, handles, project words. Add them as chips in Settings. With **OpenRouter**, the model is instructed to keep them intact. With the free engines, TeaTalk protects them by masking them out of the text before translation and restoring them after.

> A caveat worth knowing: terms whose edges aren't plain letters or digits — like `.NET`, `C++`, or `@handle` — may not be caught by glossary protection. Ordinary words and names work reliably.

## Conversation memory

A slider from 0 to 10 (default 4). It lets the OpenRouter engine see the last few lines of your conversation as context, so translations stay consistent across sentences. 0 turns it off. It only affects the OpenRouter engine.

## What leaves your machine

Worth being clear about, since TeaTalk handles your voice:

- **Local Whisper** and **Transcribe mode** keep your speech on your machine.
- **Google/Edge/OpenRouter translation** and **OpenAI Whisper** send text (or audio, for OpenAI Whisper) to those services — that's how they work.
- Before Translate mode sends text to a translation service, TeaTalk **masks URLs and @mentions** out of it, so links and handles you say aren't shipped to the translator. (This applies to Translate mode; Transcribe mode sends nothing to a translator at all.)
