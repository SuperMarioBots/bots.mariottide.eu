+++
title = "CAM Manager"
description = "Time-limited access to a channel: invite links with a duration, automatic removal when they expire."
weight = 80

[extra]
emoji = "🎟"
repo = "CAMManagerBot"
username = "CAM_Manager_Bot"
clonable = false
+++

## What it does

CAM Manager handles time-limited access to a channel. You issue an invite link
with a duration (seven days, a month, whatever you pick), you send it to the
person, they join the channel, and when the time is up the bot removes them on
its own. If you want to give them more time, one tap extends it.

Each link is good for one person and burns on first use, so it does not get
passed around. The countdown starts when the person actually joins the
channel, not when you generate the link.

The bot keeps the list of active subscribers with each expiry date, plus the
history of everyone who left, expired or was revoked. It handles several
channels at once: you pick them one by one in the menu.

## Before you start

You drive the bot from a private chat. In the channel it has to be an
administrator, with two exact Telegram permissions:

- **Invite users via link**, to create the invite links;
- **Ban users**, to remove people whose access expired.

If it loses either one, the channel pauses itself and stops issuing invites
and removing expired members until you give the permission back. See
[Telegram permissions](@/guida/permessi.md).

You have to be an administrator of the channel too: the bot only lists
channels where you show up as an admin.

## Setup

1. Open the bot in a private chat and send `/start`.
2. In your channel, promote the bot to administrator with **Invite users via
   link** and **Ban users**.
3. Go back to the bot. If the channel is missing, tap **🔄 Refresh my
   channels**.
4. Open **📋 Channels** and pick the channel (with a single channel the bot
   goes straight in).
5. Open **⚙️ Settings** and set the **⏱ Duration presets**, the cuts you will
   use most often, written in days separated by commas. The default is
   `7, 30, 90`. Each value goes from 1 to 365.
6. Still in settings, choose the **🔔 Pre-expiry warning**: 24h (the default),
   72h or off.
7. Tap **➕ Invite link**, choose a duration and send the link to the person.

## Commands

There are very few commands because nearly everything happens through
buttons.

| Command | What it does | Who | Where |
|---|---|---|---|
| `/start` | Opens the management menu, or accepts the invite if you arrive from a link | everyone | private |
| `/menu` | Reopens the menu if you closed it | channel admins | private |
| `/help` | Summary of the menu entries | everyone | private |
| `/language` | Switch between Italian and English | everyone | private |
| `/cancel` | Aborts the duration you are typing | everyone | private |
| `/ping` | Checks that the bot is alive | everyone | private |

Whoever receives an invite has nothing to learn: they open the link, tap
**Start**, and the bot sends them the link to join the channel.

## Buttons and automatic behaviour

The main menu lists the channels you manage. Inside a channel there are five
entries.

| Button | What it does |
|---|---|
| **➕ Invite link** | Issues an invite with one of the preset durations, or **✏️ Custom** to type a free one such as `7d`, `12h`, `30m` |
| **👥 Subscribers** | The active list with each expiry date, plus a **History** tab with everyone who left, expired or was revoked |
| **⚙️ Settings** | Duration presets, pre-expiry warning and channel state |
| **⏸ Pause** and **▶️ Unpause** | Stop or resume invites and expiries for that channel |
| **🔄 Refresh admins** | Re-reads from Telegram who the channel administrators are |

In the subscriber list every person carries **➕ Extend** (by a preset cut or
by a duration you type) and **🚫 Revoke**, which asks for confirmation and
then removes the person from the channel straight away. From the history tab
there is **🔁 Reinstate**, which lets somebody back in with a fresh duration.

With nobody touching anything, the bot does this:

- starts the countdown when the person actually joins the channel;
- sends a warning before the expiry, if you turned on the 24 or 72 hour
  window;
- removes expired members within a minute of their expiry and closes their
  row;
- records the people who leave on their own;
- pauses the channel if you take away either of the two permissions, and
  writes to tell you. When you give them back it resumes and works off the
  removals it could not perform;
- sends you a daily summary of expiries, departures and warnings sent.

## What the subscriber receives

All of it in a private chat, in the person's own language.

| When | What arrives |
|---|---|
| On joining | "Welcome! Your access is active until ..." |
| Before the expiry | "Heads-up: your access expires on ... Ask the channel admin for an extension if you want to stay" |
| At the expiry | "Your access has expired. Thanks for subscribing!" |
| If you revoke it | "Your access has been revoked by the channel admin" |

If the person blocked the bot these messages never arrive, but the expiry and
the removal happen all the same.

## Frequently asked questions

### The channel is not in the menu

Check that you promoted the bot to administrator in the channel and that you
are an administrator too, then tap **🔄 Refresh my channels**. If you have
just changed the channel admins, use **🔄 Refresh admins** inside the channel.

### The bot says the channel is paused

Either you paused it with **⏸ Pause**, or the bot lost one of the two
permissions. Give them back and the pause clears itself.

### How long does the link I generate last?

The link you send to the person is single use and expires after **24 hours**:
if nobody opens it by then, issue the invite again. The real join link, the one
the bot sends after they tap **Start**,
expires after one hour and works for one person only. If it expires, issue the
invite again.

### When does the countdown start?

When the person joins the channel, not when you generate the link.

### Can I extend an access that already expired?

Yes: open **👥 Subscribers**, go to **History**, find the person and use
**🔁 Reinstate** with a new duration. They get a fresh invite.

### Can the same person hold two accesses to one channel?

No. If they already have an open access to that channel, the bot tells them
they are already subscribed. To give them more time use **➕ Extend**.

### How do I write a custom duration?

A number followed by `d`, `h` or `m`: `7d` seven days, `12h` twelve hours,
`30m` thirty minutes. Presets instead are written in days only, separated by
commas.

### If I remove the bot from the channel, what happens to the subscribers?

They stay in: with no permissions the bot cannot remove anybody. The expiries
queue up and are worked off when you promote the bot again.
