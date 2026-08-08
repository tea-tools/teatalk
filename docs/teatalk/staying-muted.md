# Staying muted: talking through TeaTalk without your voice going out

For people who stay muted in VRChat and speak *only* through the chatbox. This
guide explains how TeaTalk relates to your VRChat microphone, and how to set
things up so you can talk into a mic for transcription while being certain your
voice never transmits in-world.

## First, the thing that matters most

**TeaTalk never sends your voice to VRChat.** It listens to your microphone,
turns your speech into text on your machine, and sends that **text** to the
chatbox. There is no path in TeaTalk that routes your audio *into* VRChat — so
TeaTalk itself cannot make your voice transmit.

Whether your voice actually goes out in-world is controlled entirely by
**VRChat's own microphone** (your mute toggle, push-to-talk, or open-mic
setting) — not by TeaTalk.

That's the whole picture. Everything below is about making VRChat's side
certain.

## Typing always works — even while muted

As of the current build, a message you **type** into TeaTalk is always sent,
regardless of your VRChat mute state. Typing is a deliberate choice, not live
audio, so muting your mic never blocks it. If all you do is type, you're already
done — stay muted in VRChat and type away.

The rest of this guide is for people who want to **speak** into a mic and have
TeaTalk transcribe it, while staying muted.

## The mute-behavior setting

In **TeaTalk → Settings**, under mute behavior, you choose how TeaTalk reacts to
your VRChat mute state:

| Setting | What it does to *spoken* transcription |
|---|---|
| **Pause transcribing** *(default)* | Stops transcribing while your VRChat mic is muted. Resumes when you unmute. |
| **Ignore mute** | Keeps transcribing no matter your VRChat mute state. |

If you want to **speak while muted and see the text in chatbox**, choose
**Ignore mute**. On the default "Pause transcribing," transcription stops while you're
muted — which is why it can feel like "my mic has to be on."

> "Ignore mute" only changes whether TeaTalk keeps *transcribing*. It never
> makes your voice transmit — that's still VRChat's mute doing its job.

## How certain do you want to be?

There are two ways to talk-for-transcription while muted. They differ in one
thing: what happens if VRChat gets unmuted by accident.

### Simple: one mic, stay muted in VRChat

1. Set TeaTalk's mute behavior to **Ignore mute**.
2. Keep yourself **muted in VRChat** (mute toggle on, or don't press
   push-to-talk).
3. Speak. TeaTalk hears your mic directly and sends the text to chatbox; VRChat,
   being muted, transmits nothing.

This works today with no extra setup. The catch: it relies on VRChat *staying*
muted. If you fat-finger the mute key, tap push-to-talk, or a world un-mutes
you, your voice can go out for as long as VRChat is unmuted. There's no safety
net — it's only as reliable as your mute stays put.

### Ironclad: give VRChat a separate, silent input

If you want **certainty** that your voice can never transmit — no matter what
happens to VRChat's mute — don't let VRChat listen to your real microphone at
all. Point VRChat at a different, silent input, and point TeaTalk at your real
mic. This is the approach the wider VRChat mute community uses.

You need a **virtual audio input** — a software "microphone" that carries no
sound. [VB-Audio Virtual Cable](https://vb-audio.com/Cable/) is the common free
one (it installs a "CABLE Output" recording device).

Set it up once:

1. **Install** a virtual audio cable (e.g. VB-Audio Virtual Cable). Reboot if it
   asks.
2. In **VRChat → Settings → Audio**, set your **microphone** to the virtual
   input (e.g. "CABLE Output"). Nothing is ever fed into it, so VRChat hears
   pure silence — your real voice physically cannot reach VRChat.
3. In TeaTools, set the **microphone** under **Home → General → Audio capture**
   to your **real microphone** (TeaTools has its own device picker, separate
   from VRChat's).
4. Set TeaTalk's mute behavior to **Ignore mute**.

Now you can speak freely: TeaTalk transcribes your real mic to the chatbox, and
VRChat — listening to a silent virtual input — has nothing to transmit. Your
VRChat mute state stops mattering at all, because there's no live audio behind
it.

> This is the only setup that is **certain**. In the simple approach, software
> is trusting VRChat to stay muted; here, VRChat simply isn't connected to your
> voice.

## Why isn't there a single "never transmit" button?

Because VRChat doesn't expose one. VRChat has no command that lets an outside app
*force* you muted — the mute is a toggle a person presses, and an app can at most
press it back. That means any purely-software "keep me muted" feature is a race:
it can re-mute you after an accidental unmute, but a fraction of a second of
audio can slip out before it catches. The separate-input setup above avoids the
race entirely, which is why it's the honest answer for anyone who needs a
guarantee.

## Quick reference

- **Just typing, staying muted?** Works as-is. Nothing to set up.
- **Speaking, and "good enough" certainty?** Ignore mute + stay muted in VRChat.
- **Speaking, and you need it airtight?** Virtual input for VRChat, real mic for
  TeaTalk, Ignore mute. Your voice never reaches VRChat, period.
