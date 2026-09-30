# The TeaTools hub

TeaTools is a **plugin host**. It owns the resources that only one thing can have at a time — VRChat's OSC connection, the chatbox, your microphone — and hands them to modules so they never fight over them. This page walks the Home screen tab by tab.

The Home screen has four tabs: **General**, **Modules**, **Developers**, and **About**.

## General

Hub-wide settings, shared by every module.

### Appearance

- **Theme** — light or dark. Modules inherit it automatically, so the whole app stays coherent.
- **Accent** — one accent color for the entire app, including third-party modules.

### Audio capture

This is the single microphone every listening module uses (TeaTalk today; more later). Setting it here means you configure your mic **once**, not in each module.

- **Microphone** — the capture device shared by all modules.
- **Microphone level** — shows the live input level. TeaTalk's built-in speech detection is automatic; there is no sensitivity or silence-gap adjustment.

### Ambient listening

Separate from your own microphone: this transcribes **other players'** speech from VRChat's audio, for modules that react to the room. It's independent of your mic capture above.

- **Enable ambient listening** — off by default. Requires VRChat to be running, and turns off cleanly without restarting the hub.
- **Whisper model** — the model used to transcribe what other people say. Independent of your own speech-to-text model in TeaTalk. Turns on together with ambient listening.

> No module in this alpha uses ambient listening yet — it's the hub capability that future modules build on.

### OSC connection

- **OSC ports** — the ports TeaTools uses to talk to VRChat, shown for reference. The **send** port is fixed by VRChat's protocol. The **receive** port is assigned automatically at startup — TeaTools deliberately leaves the classic receive port (9001) free so face-tracking apps and other OSC software can keep it, and VRChat finds TeaTools' actual port through OSCQuery. The row shows the real bound port with how it was chosen — e.g. `51234 (auto)`, or `— (inbound disabled)` if no port could be bound. A separate live indicator in the same OSC section shows whether TeaTools currently sees VRChat.

## Modules

Your installed modules, each as a card with an on/off toggle.

- **Modules ship disabled.** Toggle one on and the choice is saved (`modules.json`) and applied live — the module loads immediately, no restart. Toggle it off and it unloads immediately.
- **Open a module** by clicking its row (or its entry in the left rail) — that's where the module's own controls live.
- Each module runs **isolated** from the hub and from other modules, so if one fails it doesn't take TeaTools down with it.

**TeaTalk** is the hub's flagship first module, and it ships with TeaTools. Like every module it starts switched off until you turn it on here. Additional modules — ambient chatbox status, haptics, and more — arrive through the module catalog after alpha.

## Developers

A read-only surface for people who want to build their own modules against the hub. It lays out the module contract — what TeaTools owns (the OSC connection, VRChat discovery, chatbox arbitration, and module lifecycle) versus what a module author controls (their own UI, OSC handlers, and manifest) — plus the primitive kit and SDK a module is built from, and how licensing works for authors.

Nothing here needs configuring; it's a preview of what module authoring will look like. If that's you, developer/module-author docs aren't part of this public docs set yet — ask on the **[TeaTools Discord](https://discord.gg/GUdBNfXfbe)**.

## About

- **Crash reports** — a consent toggle for sending crash/diagnostic data. It's opt-in; the same choice you make at first run lives here so you can change it any time. No account or identifier is attached, but diagnostic uploads (crash reports and problem reports) may include file paths from your PC in logs and error messages.

## Under the hood

- **Single instance** — a system-wide lock (`Global\TeaTools.Hub`) means only one TeaTools runs at a time; launching again focuses the existing window.
- **System tray** — TeaTools puts an icon in the tray; right-click it for actions and to quit. **Closing the window quits TeaTools** — that's the default, so the window's close button (✕) really does shut the app down rather than leaving it running out of sight. If you'd rather it keep running in the background, turn on **Minimize to system tray** under General → System: with that on, closing the window hides it to the tray and you quit from the tray icon instead.
- **Logs** — `%APPDATA%\TeaTools\logs`, one dated file per day (`teatools20260821.log`).

See [troubleshooting](troubleshooting.md) when something isn't behaving.
