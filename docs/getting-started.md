# Getting started with TeaTools

TeaTools is a Windows app that sits between your microphone and VRChat and gives your modules a clean, shared line to VRChat over OSC. This page gets the hub installed, connected, and running one module.

## Install & run

TeaTools ships as a self-contained Windows build — you don't need to install .NET separately.

1. Unzip the TeaTools folder anywhere.
2. Run `TeaTools.App.exe`.
3. The app opens its window and also places an icon in your **system tray** — right-click it for quick actions and to quit. Closing the window leaves it running in the tray.

TeaTools is **single-instance**: launching it again just focuses the copy that's already running, so you can't accidentally run two.

## Turn on OSC in VRChat

TeaTools works by owning VRChat's OSC connection, so OSC has to be on in VRChat:

- In VRChat: Action Menu → **Options → OSC → Enable**.

You do this once; VRChat remembers it. TeaTools finds VRChat automatically (via OSCQuery) — you'll see the connection state in the **OSC** section under Home → General. TeaTools sends to and listens on the standard VRChat OSC ports, shown alongside it.

## Enable a module

The hub does nothing user-visible on its own — features come from **modules**, and they all ship **disabled** so nothing runs uninvited.

1. Open the **Modules** tab on the Home screen.
2. You'll see the installed modules as cards. TeaTools ships with **TeaTalk** (speech → chatbox).
3. Toggle a module on. The choice is saved and applied immediately — no restart.
4. The module appears in the left rail; click it to open its panel.

From here, set up the one you enabled — see the [TeaTalk docs](teatalk/README.md) for the module that ships with TeaTools.

## Set your microphone (once, shared by every module)

Any module that listens to your voice uses **one** shared microphone, configured on the hub — not per module.

- Go to **Home → General → Audio capture** and pick your microphone and sensitivity. Full details in [the hub reference](the-hub.md#audio-capture).

## Where TeaTools keeps its files

Everything lives under `%APPDATA%\TeaTools\`:

| Path | What's there |
|---|---|
| `logs\teatools.log` | The app log — the first place to look when something's wrong |
| `modules.json` | Which modules you've enabled |
| `plugins\` | Installed catalog modules |
| `data\` | Per-module saved settings |
| `models\` | Downloaded speech models |

## Next

- **[The hub reference](the-hub.md)** — the Home screen tab by tab: appearance, audio, ambient listening, OSC, modules, and privacy/telemetry.
- **[Troubleshooting](troubleshooting.md)** — the app won't start, OSC won't connect, where to find logs.
