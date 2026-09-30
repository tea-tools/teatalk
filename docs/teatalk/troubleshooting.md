# TeaTalk troubleshooting

## Nothing reaches my VRChat chatbox

Work down this list:

1. **Is OSC on in VRChat?** Action Menu → **Options → OSC → Enable**. This is the most common cause. If OSC was off when you started, turn it on and restart VRChat.
2. **Is TeaTalk enabled and listening?** It ships disabled — enable it on **Home**, open it, and click **Start listening**. STT does not start until you press that button.
3. **Is "Send to chatbox" on?** In Settings, if it's off, TeaTalk recognizes and translates but sends nothing to VRChat.
4. **Are you muted in VRChat?** With the default **Pause transcribing**, being muted holds spoken lines (typed messages still send). Unmute, or switch to **Ignore mute** — see [mute behavior](guide.md#mute-behavior).
5. **Is your mute state unclear to TeaTools after TeaTools has connected to VRChat at least once this session?** With **Pause transcribing**, that unconfirmed state holds spoken lines too. You'll see the persistent **“Mute state unknown — paused to be safe”** warning with a **Check OSC** action. TeaTalk automatically rechecks a temporarily unavailable state while VRChat remains discoverable; if the warning lingers, check that OSC is still on (step 1).

## My words never get recognized (transcript stays empty)

- **First run:** the local Whisper model (~148 MB with the default **Base** size) downloads before the first recognition. TeaTalk reports the download as it goes and says when the model is ready, so give it a moment on your very first listen and make sure you're online for it. If it fails, TeaTalk tells you what to check and stops listening — fix that, then press **Start listening** to run the download again.
- **Wrong microphone:** capture device is set under **Home → General → Audio capture**, not in TeaTalk. Check the right mic is selected there.
- <a id="voice-detection"></a>**Voice detection:** TeaTalk uses its built-in neural speech detection automatically. If it says built-in speech detection could not start, apply the latest TeaTools update or reinstall TeaTools, then try Start listening again. If the microphone meter barely moves when you speak, check the microphone and its input volume.

## The translation is wrong or low quality

- The free engines (Google, Edge) are good but not perfect. For higher quality, switch to **OpenRouter** with your own key — see [engines](guide.md#engines).
- **Names/terms getting mangled?** Add them to the [glossary](guide.md#glossary).
- **Translations drift across sentences?** Raise **Conversation memory** (OpenRouter only).

## OpenRouter says it failed

- **Check your key and model.** A bad key or an unavailable model id causes failures. The model box's suggestions are safe choices; blank uses the default (`openai/gpt-4o-mini`).
- **You'll usually still get your line:** with "fall back to free translation" on (the default), TeaTalk retries once through Google and tells you it did. If you turned that off, the line is dropped instead.

## My typed lines work but my voice doesn't

That points at speech-to-text or the microphone, not the chatbox path (typing skips STT). Re-check the microphone under **Home → General → Audio capture** and the first-run model download above.

## Recognition is slow, or VRChat stutters while I talk

Local Whisper uses your GPU where TeaTools can select a usable one, which keeps recognition off the cores VRChat needs. Selection is automatic and has been confirmed to engage on real hardware. The `STT backend:` line written to the log at startup names the backend and device in use and, where it fell back to the CPU, the reason. Check that line first: GPU acceleration still depends on your hardware and drivers, and CPU recognition competes with VRChat for cores.

If it picked wrong, override it in `appsettings.local.json` next to `TeaTools.App.exe` (restart afterwards):

```json
{
  "Stt": {
    "Backend": "vulkan",
    "GpuDevice": 0,
    "WhisperThreads": 8
  }
}
```

- `Backend` — `auto` (default), `cpu`, or `vulkan`.
- `GpuDevice` — which GPU to use when you have more than one.
- `WhisperThreads` — how many CPU cores recognition may use. TeaTools derives a bounded share so it doesn't fight VRChat for the CPU; set this only if your machine disagrees.

Leave any key out to let TeaTools decide it.

## A line got cut off with "…"

VRChat's chatbox holds 144 characters. When your original plus the translation don't both fit, TeaTalk trims the **original** with an ellipsis and always keeps the translation whole. Switch the [chatbox format](guide.md#chatbox-format) to **Translation only** if you'd rather not show the original at all.

## Still stuck?

Ask in the **[TeaTools Discord](https://discord.gg/GUdBNfXfbe)** — describe your engine choice, languages, and what you expected versus what appeared in the chatbox.

## Keys and privacy

- API keys are stored **encrypted** on Windows (DPAPI, tied to your Windows account) — or as plain text when Windows can't encrypt them, which an ordinary PC can hit after a password reset on a local account or on a temporary profile. Either way the file stays on your PC.
- In **Translate** mode, URLs and @mentions are stripped out of your text before it's sent to a translation service.
- **Local Whisper** and **Transcribe** mode keep your speech on your machine; cloud engines (Google/Edge/OpenRouter/OpenAI Whisper) send text or audio to those services by nature.
