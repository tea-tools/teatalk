# TeaTalk settings reference

Every TeaTalk setting, its default, and what it does. Settings live on the TeaTalk **Settings** panel unless noted. Changes apply automatically a moment after you make them.

For guidance on *when* to use these, see the [user guide](guide.md).

## Language

| Setting | Default | Effect |
|---|---|---|
| Spoken language | Detect language (auto-detect) | The language you talk in. Fresh installs default to **Detect language**, which auto-detects your speech. Picking a specific language instead pins local speech-to-text to it, which is a little faster (it skips the detection step). A saved concrete pick from before this default changed is kept as-is. |
| Chatbox language | Japanese (`ja`) | The language translations are written in. |

> The language **pickers** live on the main panel, not in Settings — the main panel is the single place to change languages, and your choice there is remembered. Swapping languages on the main panel (the swap button) is a temporary flip for the current session and isn't saved; picking a language from a picker is saved. The swap button is unavailable while the spoken language is set to Detect language — there's no concrete language to move to the chatbox side.

## Translation

| Setting | Default | Effect |
|---|---|---|
| Translation engine | Edge Translate | Edge Translate (Microsoft, free), Google Translate (free), or OpenRouter LLM (needs key). If Edge fails, TeaTalk auto-falls back to Google. |
| OpenRouter API key | *(empty)* | Your OpenRouter key. Masked; normally stored encrypted (Windows DPAPI) — see [Notes on storage](#notes-on-storage) for when it isn't. Only used by the OpenRouter engine. |
| OpenRouter model | `openai/gpt-4o-mini` | The model OpenRouter uses. Free-text; suggestions are offered. Blank falls back to the default. |
| OpenRouter temperature | `0.3` | 0–2. Lower = more literal, higher = more creative. |
| OpenRouter base URL | OpenRouter endpoint | Leave blank unless using a compatible proxy. Blank or invalid falls back to the default. |
| Fall back to free translation if my model fails | On | On OpenRouter failure, retry once via free Google Translate and warn you. Off = drop the line instead. |

## Chatbox

| Setting | Default | Effect |
|---|---|---|
| Chatbox format | Original, then translation | How translated output is arranged: Original, then translation; Translation, then original; or Translation only. |
| Send to chatbox | On | Off = TeaTalk still recognizes/translates in-app but sends nothing to VRChat. |
| Typing indicator | On | Show VRChat's "typing…" bubble while preparing a line. |
| Live captions | On | Show your words in the chatbox while you speak; the finished line settles when you stop. Early text is a best guess and can change. Unavailable while Send to chatbox is off. Changing it while listening briefly pauses transcription (the speech pipeline restarts). |

## Speech-to-text

| Setting | Default | Effect |
|---|---|---|
| Speech engine | Local Whisper | Local Whisper (free, offline), OpenAI Whisper (cloud, needs key), or OpenAI Live Transcribe (cloud, needs key, lower latency, costs more per minute). |
| Model *(in the **Whisper** card)* | Base (~148 MB) | Tiny (~78 MB), Base (~148 MB), or Small (~488 MB). Bigger = more accurate, larger download. The row appears only while **Whisper** is the selected engine. |
| OpenAI Whisper API key | *(empty)* | Your OpenAI key. Masked; normally stored encrypted (Windows DPAPI) — see [Notes on storage](#notes-on-storage) for when it isn't. Only used by the OpenAI Whisper engine. |
| OpenAI Live Transcribe API key *(in the "OpenAI platform key" block at the foot of Advanced)* | *(empty)* | A separate OpenAI key, used only by the OpenAI Live Transcribe engine — billed at $0.017 per minute of audio actually sent, higher than OpenAI Whisper's per-minute rates, for lower latency. Masked; stored the same way as the key above. Visible regardless of which speech engine is currently selected, so you can set it up before switching. |

> **TeaTools selects the local Whisper backend automatically** — a discrete Vulkan GPU where one is available, an integrated GPU where that is the only option, and the CPU engine where no usable Vulkan GPU is present. There is no setting for this.
>
> **The startup log names the backend in use.** TeaTools writes a single `STT backend:` line identifying the backend and device it selected, and states the reason whenever it requested the GPU and fell back to the CPU. GPU acceleration has been confirmed on real hardware, but still depends on your hardware and drivers — check that line to confirm what your machine is using.

### Advanced overrides (no UI — `appsettings.local.json`)

Only for rigs where the automatic choice is wrong. Create `appsettings.local.json` next to `TeaTools.App.exe`; leave a key out entirely to let TeaTools decide. Restart the app after editing.

| Key | Default | Effect |
|---|---|---|
| `Stt:Backend` | *(unset — auto)* | `auto`, `cpu`, or `vulkan`. `cpu` forces the CPU engine; `vulkan` requires a usable GPU and falls back to CPU (with a warning in the log) if there isn't one. |
| `Stt:GpuDevice` | *(unset — auto)* | Device number to use when more than one GPU is present. Out of range or unusable falls back to CPU and says so in the log. |
| `Stt:WhisperThreads` | *(unset — derived)* | How many CPU cores recognition may use. TeaTools derives a bounded share so it doesn't compete with VRChat; set this only if your machine disagrees. Applies to the CPU work on either backend. |

## Mute behavior

| Setting | Default | Effect |
|---|---|---|
| Mute behavior | Pause transcribing | Pause transcribing (stop transcribing while your VRChat mic is muted) or Ignore mute (keep transcribing regardless). See the [guide](guide.md#mute-behavior). |

## Glossary & context

| Setting | Default | Effect |
|---|---|---|
| Glossary | *(empty)* | Terms to keep unchanged through translation. Add/remove as chips. |
| Conversation memory | 4 | 0–10. How many recent lines of context the OpenRouter engine sees. 0 = off. OpenRouter only. |

## Elsewhere (not in TeaTalk Settings)

These affect TeaTalk but are owned by the hub because they're shared across modules:

| Setting | Where | Effect |
|---|---|---|
| Capture device | Home → General → Audio capture | Which microphone the whole app listens to. |
| Voice detection sensitivity | Home → General → Audio capture | The threshold that separates speech from room noise. |
| Transparency effects | Home → General → Appearance | On by default. Turn it off if text is hard to read through the frosted-glass look — the window, dialogs and tooltips go fully opaque, same design with nothing showing through. Applies instantly, no restart. This is the accessibility opt-out for the dark-theme contrast problem a bright window behind TeaTools causes. **Known issue:** in the *light* theme some muted grey text is still lower-contrast than it should be even with this off; that's an ink-colour fix, tracked separately. |

## Notes on storage

- TeaTalk's configuration is saved in its own plugin storage.
- API keys are encrypted at rest using **Windows DPAPI** (tied to your Windows user account). When Windows can't do that encryption, TeaTools saves the key as plain text rather than lose it. That isn't only an unusual-setup thing — an ordinary PC can hit it after a password reset on a local account, on a temporary or roaming Windows profile, or if Windows' own key store is damaged. Either way the file never leaves your PC; a plain-text key just isn't protected from anything else on the machine that can read your files.
- A key you saved before TeaTools started encrypting keys stays plain text until the next time it's saved successfully.
- In `%APPDATA%\TeaTools\logs`, TeaTools records which way a key ended up stored. There's one log file per day, named with its date — `teatools20260821.log`, for example — so open the newest and search it for `TeaTalk API key storage:`; the phrase sits mid-line after the timestamp, not at the start of the line. It says what happened to your key once per run, and never contains the key itself. Nothing in the app shows you — the log is the only place it's stated.
