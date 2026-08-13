# TeaTalk

*Say it once. They read it in their language.*

**Real-time speech translation for VRChat.** You talk normally; the people around you read it in their language, right in the in-game chatbox — while you keep talking.

![Status: Alpha](https://img.shields.io/badge/status-alpha-orange)
![Platform: Windows x64](https://img.shields.io/badge/platform-Windows%20x64-blue)
![License: PolyForm Noncommercial 1.0.0](https://img.shields.io/badge/license-PolyForm%20Noncommercial%201.0.0-lightgrey)
![Latest release](https://img.shields.io/github/v/release/vaniteav/teatalk?include_prereleases)

`Free to use · No account · Windows`

---

## What it feels like

You join a world, someone says hi in a language you don't speak, and you just... answer. You speak normally into your mic. A beat later, your words land in the VRChat chatbox in their language — no menus, no stopping mid-sentence, no copy-pasting into another window. Flip to transcribe mode and it captions your own voice instead, clean and live.

It works the first time you open it. Nothing to sign up for, nothing to pay.

---

## Why you'll like it

- 🗣️ **Speak, don't type.** Your voice becomes chatbox text in another language while you keep talking — live, no menus, no stopping mid-sentence.
- 🆓 **Free out of the box.** Speech recognition runs on your PC (local Whisper); translation is built in (Microsoft Edge, with automatic fallback to Google). No account, no API key.
- 🔇 **Mute players are first-class here.** Switch on **Ignore mute** and TeaTalk turns your speech into chatbox text even while your VRChat mic is muted — so you're always in the conversation.
- 🧠 **Translation that follows the conversation.** Bring your own OpenRouter key and TeaTalk carries context between lines — pronouns, follow-ups, and names stay consistent instead of each sentence being translated cold. (The free path needs no key.)
- 🎨 **Actually designed.** A soft "Pastel Glass" interface, light and dark themes, and one consistent style across every module — an OSC tool that feels like it belongs in VRChat.
- 🔀 **Translate or transcribe.** Post your words in another language, or caption your own speech as-is. One click to switch.
- 💬 **Live captions (opt-in preview).** Watch your words appear in the chatbox as you speak, before the finished translation lands. Off by default — turn it on in **Chatbox** settings. It's a preview, so expect rough edges.
- 🌐 **Auto-detects your language.** Just talk — TeaTalk figures out what you're speaking. Prefer to pin one language? Pick it, and local recognition gets faster.
- 📝 **Reads the way you want.** Show the original first, the translation first, or translation only.

---

## Download

**[⬇️ Get the latest alpha build → github.com/vaniteav/teatalk/releases](https://github.com/vaniteav/teatalk/releases)**

1. Download and unzip anywhere (your Desktop is fine).
2. Run the app — nothing else to install.
3. In VRChat, enable OSC: **Action Menu (R) → Options → OSC → Enabled.** TeaTalk finds VRChat automatically once OSC is on.

> **First launch:** Windows may show a SmartScreen notice because the app isn't code-signed yet — click **More info → Run anyway.** (Alpha; signing comes later.)

**You'll need:** Windows (64-bit) · VRChat with OSC enabled · a microphone.

---

## How it works (and what's free)

The **default path is free and runs on your machine:**

- **Speech → text** happens **on your PC** with local Whisper. Your voice audio isn't sent to a server on this path.
- **Translation** uses free, keyless engines (Microsoft Edge, falling back to Google automatically if the Edge endpoint hiccups) — so a dropped call doesn't drop your line.

That's the whole free path. No account, no key, no catch.

### Optional power-user mode: bring your own OpenRouter key

Add your own [OpenRouter](https://openrouter.ai/) API key and translation stops working line-by-line and starts working like a conversation:

- **Conversation memory** — hands the model your recent back-and-forth (0–10 messages, 4 by default) so pronouns, follow-ups, and the running topic carry from one line to the next instead of each sentence being translated cold.
- **Your glossary** — pin names, jargon, and in-game terms so they come out the same way every time; no more your friend's handle getting "translated."
- **Links and @mentions survive** — URLs and @handles are set aside before translation and restored after, so they always come through intact.
- **Your model, your settings** — choose any OpenRouter model and tune how literal it is (deterministic by default).

Any API keys you add are **encrypted on your PC** (Windows DPAPI) and never leave it. You never need a key to use TeaTalk.

*Provider names (Whisper, Microsoft Edge, Google, OpenRouter, VRChat) describe what TeaTalk connects to — not endorsements or partnerships.*

---

## Docs

The same docs that ship inside the download, readable here first.

| If you want to… | Read |
|---|---|
| Install it, connect it to VRChat, get your first line into the chatbox | [Getting started](docs/getting-started.md) |
| Understand the Home screen — appearance, audio, ambient, OSC, modules, privacy | [The hub](docs/the-hub.md) |
| Fix the app not starting, OSC not connecting, or a mic that isn't heard | [Troubleshooting](docs/troubleshooting.md) |
| Know exactly what leaves your PC and what doesn't | [Privacy](docs/PRIVACY.md) |

**TeaTalk** — the translation module, in depth:
[start here](docs/teatalk/getting-started.md) · [full guide](docs/teatalk/guide.md) · [every setting](docs/teatalk/settings-reference.md) · [talking while muted](docs/teatalk/staying-muted.md) · [troubleshooting](docs/teatalk/troubleshooting.md)

Something unclear or plain wrong? Say so on [Discord](https://discord.gg/GUdBNfXfbe) — the docs are alpha too.

---

## Privacy, honestly

- On the **default path, your voice is turned into text on your own PC** and isn't shipped to a server. (If you opt into a cloud speech engine, audio does leave your PC — that's your choice.)
- **Translation** text goes to whichever engine you've picked (Edge/Google on the free path, or OpenRouter if you bring a key).
- **Respect-VRChat-mute is on by default:** while you're muted in-world, TeaTalk transcribes nothing.
- **Diagnostics are opt-in — nothing is sent unless you choose to.** If you use the in-app "Report a problem" button, it sends what you write, plus TeaTools' own logs and settings (never your API keys) and basic system info — your app version, your Windows version, and the time. No account or identifier is attached. We don't call it "anonymous," though: those logs can include file paths from your PC, and we'd rather be precise about your privacy than oversell it.

---

## This is an alpha 🌱

TeaTalk is early and built in the open. Expect rough edges, expect things to change, and expect the occasional bug — "early and honest" is the point, not "flawless." Version `v0.1.0-alpha.3`.

**Built in the open on [Discord](https://discord.gg/GUdBNfXfbe).** It's just getting started — so the feedback you leave now is the feedback that steers what ships. Come say hi.

If something breaks, there's a **"Report a problem"** button right in the app — it's the fastest way to help fix it.

---

## License

TeaTalk is part of **TeaTools** (TeaTalk is the translation module; the app is the hub). It's released under the **PolyForm Noncommercial 1.0.0** license — free to use, not open-source-for-commercial-use. See [`LICENSE`](LICENSE) for details.
