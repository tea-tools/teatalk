# TeaTools troubleshooting (hub)

Hub-level problems. For issues specific to speech and the chatbox, see [TeaTalk troubleshooting](teatalk/troubleshooting.md).

## The app won't open / nothing happens when I run it

- **It may already be running.** TeaTools is single-instance and lives in the **system tray** — check there before launching again. A second launch just focuses the running copy.
- **Check the log.** TeaTools records startup in `%APPDATA%\TeaTools\logs` — one file per day, named with its date, like `teatools20260821.log`. If the window never appears, the tail of the newest one usually says why.

## Windows shows a warning when I run the installer

The beta installer is digitally signed. If Windows shows a warning, check that you downloaded `TeaTools-win-Setup.exe` from the [official release](https://github.com/tea-tools/teatalk/releases/tag/v0.1.0-beta.3). You can inspect its signature by right-clicking the file and opening **Properties → Digital Signatures**.

## My antivirus warns that TeaTools "wants webcam access"

Some antivirus tools may label microphone access as a webcam request. Check Windows privacy settings to see which device was accessed. If you are unsure about a warning, share its wording when reporting the problem.

## TeaTools doesn't see VRChat / OSC won't connect

1. **Enable OSC in VRChat:** Action Menu → **Options → OSC → Enable**. This is the most common cause.
2. **Start order:** if VRChat was already running with OSC off when you turned it on, restart VRChat so it re-advertises itself.
3. **Check the OSC connection row** under **Home → General → OSC connection** — it reflects whether TeaTools currently sees VRChat and on which ports.
4. **Reset VRChat's OSC config** if it's stale: close VRChat, delete its OSC config folder (`%LOCALAPPDATA%Low\VRChat\VRChat\OSC\`), reopen. VRChat rebuilds it.
5. **Other OSC apps are fine.** TeaTools doesn't take the classic OSC receive port (9001) at all anymore — it picks a free port automatically at startup and VRChat finds it through OSCQuery, so face-tracking apps (like VRCFaceTracking) and other OSC software can keep 9001. This doesn't crash or block anything. If receiving still fails entirely, TeaTools keeps running send-only and logs the reason in the day's log file.

## I need TeaTools on a fixed OSC receive port

By default the receive port is assigned automatically (see above). If a tool in your setup can only send to a fixed port, you can pin one: create (or edit) `appsettings.local.json` next to `TeaTools.App.exe` and set

```json
{
  "Osc": {
    "ListenPort": 9001
  }
}
```

TeaTools then binds exactly that port (falling back to a free one only if it's already taken — the Home → General OSC row shows `(fallback)` when that happened). There is no settings-UI field for this yet; the file is the supported override. Note a fixed 9001 brings back the old tug-of-war with face-tracking apps — only pin it if you need it.

## Text is hard to read through the frosted glass

Turn **Transparency effects** off: **Home → General → Appearance**, directly under Theme. The window, dialogs and tooltips stop asking Windows for the blur effect and render fully opaque — the same design, with nothing from your desktop showing through. It applies instantly, no restart, and it's on by default so nothing changes until you flip it.

This is the accessibility opt-out for the dark-theme contrast problem a bright window sitting behind TeaTools causes. **Known issue:** in the *light* theme some muted grey text is still lower-contrast than it should be even with the switch off — that's the ink colour itself, which no transparency setting can fix, and it's tracked separately.

## My module won't turn on

- Modules ship **disabled** — enable them on the **Modules** tab.
- If a module shows as failed, it's isolated by design — the hub keeps running. Check the day's log file for the reason.
- There's no public catalog of third-party modules to install yet in this beta — only the modules that ship with TeaTools are available to enable.

## My microphone isn't being heard

The mic is a **hub** setting, shared by all modules — not a per-module one. Set it under **Home → General → Audio capture**, and watch the level meter as you talk to confirm TeaTools hears the right device.

TeaTools also tells you when it's hearing nothing: after 30 seconds of listening with no speech detected, it writes a line to the day's log file. Search the newest one for **"No speech detected in 30s of listening"** — the phrase sits mid-line, after the timestamp, not at the start of the line. If you see it while you were talking, the wrong microphone is selected or the selected input is muted, unplugged, or a silent virtual device.

## Reset to a clean state

Everything TeaTools stores is under `%APPDATA%\TeaTools\`. With the app closed you can:

- Delete `modules.json` to forget which modules were enabled.
- Delete `data\` to clear saved module settings.
- Delete `models\` to remove downloaded speech models (they re-download on next use).

Removing these is non-destructive to the app itself — it rebuilds them.

## Where to find the log

`%APPDATA%\TeaTools\logs`. There's one file per day, named with its date — `teatools20260821.log`, for example — so the newest is the one to open. It's the first thing to check for almost anything, and the right thing to attach when reporting a problem.

## Still stuck?

Ask in the **[TeaTools Discord](https://discord.gg/GUdBNfXfbe)** — attach the newest log file from `%APPDATA%\TeaTools\logs` and describe what you expected versus what happened.
