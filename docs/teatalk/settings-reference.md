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
| OpenRouter API key | *(empty)* | Your OpenRouter key. Masked; stored encrypted (Windows DPAPI). Only used by the OpenRouter engine. |
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
| Live captions | Off | Show your words in the chatbox while you speak; the finished line settles when you stop. Early text is a best guess and can change. Unavailable while Send to chatbox is off. Changing it while listening briefly pauses transcription (the speech pipeline restarts). |

## Speech-to-text

| Setting | Default | Effect |
|---|---|---|
| Speech engine | Local Whisper | Local Whisper (free, offline) or OpenAI Whisper (cloud, needs key). |
| Whisper model size | Base (~142 MB) | Tiny (~75 MB), Base (~142 MB), or Small (~488 MB). Bigger = more accurate, larger download. Local engine only. |
| OpenAI API key | *(empty)* | Your OpenAI key. Masked; stored encrypted (Windows DPAPI). Only used by the OpenAI Whisper engine. |

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

## Notes on storage

- TeaTalk's configuration is saved in its own plugin storage.
- API keys are encrypted at rest using **Windows DPAPI** (tied to your Windows user account). On non-Windows systems, or if encryption is unavailable, keys fall back to being stored as plain text — relevant only if you're running outside a normal Windows setup.
