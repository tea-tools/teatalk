# TeaTalk troubleshooting

## Nothing reaches my VRChat chatbox

Work down this list:

1. **Is OSC on in VRChat?** Action Menu → **Options → OSC → Enable**. This is the most common cause. If OSC was off when you started, turn it on and restart VRChat.
2. **Is TeaTalk enabled and listening?** It ships disabled — enable it on **Home**, open it, and click **Start listening**. STT does not start until you press that button.
3. **Is "Send to chatbox" on?** In Settings, if it's off, TeaTalk recognizes and translates but sends nothing to VRChat.
4. **Are you muted in VRChat?** With the default **Pause transcribing**, being muted stops spoken transcription (typed messages still send). Unmute, or switch to **Ignore mute** — see [mute behavior](guide.md#mute-behavior).

## My words never get recognized (transcript stays empty)

- **First run:** the local speech model (~142 MB) downloads before the first recognition. Wait for it on the very first listen, and make sure you're online for that download.
- **Wrong microphone:** capture device is set under **Home → General → Audio capture**, not in TeaTalk. Check the right mic is selected there.
- <a id="voice-detection"></a>**Voice detection too strict:** on **Home → General → Audio capture**, watch the level meter as you talk. If the bar barely moves when you speak, your voice isn't crossing the detection threshold — lower the sensitivity. If it triggers on silence (a fan, music, roommates), raise it. Calibrate in a quiet room if one's available.

## The translation is wrong or low quality

- The free engines (Google, Edge) are good but not perfect. For higher quality, switch to **OpenRouter** with your own key — see [engines](guide.md#engines).
- **Names/terms getting mangled?** Add them to the [glossary](guide.md#glossary).
- **Translations drift across sentences?** Raise **Conversation memory** (OpenRouter only).

## OpenRouter says it failed

- **Check your key and model.** A bad key or an unavailable model id causes failures. The model box's suggestions are safe choices; blank uses the default (`openai/gpt-4o-mini`).
- **You'll usually still get your line:** with "fall back to free translation" on (the default), TeaTalk retries once through Google and tells you it did. If you turned that off, the line is dropped instead.

## My typed lines work but my voice doesn't

That points at speech-to-text or the microphone, not the chatbox path (typing skips STT). Re-check the microphone under **Home → General → Audio capture** and the first-run model download above.

## A line got cut off with "…"

VRChat's chatbox holds 144 characters. When your original plus the translation don't both fit, TeaTalk trims the **original** with an ellipsis and always keeps the translation whole. Switch the [chatbox format](guide.md#chatbox-format) to **Translation only** if you'd rather not show the original at all.

## Still stuck?

Ask in the **[TeaTools Discord](https://discord.gg/GUdBNfXfbe)** — describe your engine choice, languages, and what you expected versus what appeared in the chatbox.

## Keys and privacy

- API keys are stored **encrypted** on Windows (DPAPI, tied to your Windows account).
- In **Translate** mode, URLs and @mentions are stripped out of your text before it's sent to a translation service.
- **Local Whisper** and **Transcribe** mode keep your speech on your machine; cloud engines (Google/Edge/OpenRouter/OpenAI Whisper) send text or audio to those services by nature.
