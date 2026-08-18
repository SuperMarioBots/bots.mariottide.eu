+++
title = "Ubot Manager"
description = "Takes messages from a channel of yours and posts them to every group in a Telegram folder, on the schedule you set."
weight = 100

[extra]
username = "Ubot_Manager_Bot"
emoji = "🪄"
repo = "ubot"
clonable = false
+++

## What it does

Ubot Manager posts for you. Pick a channel to take messages from, pick a
Telegram folder holding the groups you want to post in, say how often, and the
bot does the rest. On every run it picks a fresh message from the channel and
sends it to every group in the folder.

The difference from the other bots is that no bot works inside those groups:
your own account does. You connect it once with `/login` and from then on the
messages go out as if you had typed them. That is why it also works in groups
where bots cannot join or cannot write.

You can run several folders at once, each with its own source channel, its own
interval and its own settings.

## Before you start

It is used only in a private chat with the bot. Do not add it to any group and
do not promote it anywhere: the permissions it needs are the ones you already
have in your own groups.

You need:

- your Telegram account, connected to the bot with `/login`;
- a Telegram folder containing the destination groups;
- a channel (a broadcast channel, not a group) you are already a member of, to
  use as the message source.

After the login Telegram warns you about a new session called **Windows 10
Desktop**. That session is the bot. Do not terminate it: if you revoke it the
bot stops posting and you have to run `/login` again.

## Setup

1. Open the bot in a private chat and send `/start`.
2. Send `/login` and tap **Open secure login**. A small page opens where you
   enter your phone number and the code Telegram sends to your app.
3. In the Telegram app create the folder holding your destination groups:
   **Settings**, **Folders**, **Create new folder**, then add the groups.
4. Back on the bot, send `/spam` and tap **+ Add folder**. Pick the folder you
   just created.
5. Inside the folder tap **Source channel** and choose the channel to take
   messages from, or send its @username or invite link.
6. Tap **Set timer**, choose how often to post (every 2 hours, for example),
   whether to run forever or stop after a given number of runs, and optionally
   a fixed start time so the runs line up with the clock.

From then on the bot runs on its own. To see the result right away, tap
**Run spam now**.

## Commands

All of them in a private chat with the bot.

| Command | What it does | Who | Where |
|---|---|---|---|
| `/start` | Welcome message and first steps | everyone | private |
| `/login` | Connect your Telegram account to the bot | everyone | private |
| `/logout` | Disconnect the session and delete the stored access | everyone | private |
| `/spam` | Opens folders, source channels and timers | everyone | private |
| `/errors` | Shows the errors of the last runs, group by group | everyone | private |
| `/guide` | Step by step tutorial inside the bot | everyone | private |
| `/language` | Switch between Italian and English | everyone | private |
| `/paysupport` | Contact for payment problems | everyone | private |
| `/cancel` | Abort the operation in progress | everyone | private |
| `/help` | List of commands | everyone | private |

## Buttons and automatic behaviour

Almost everything happens through the `/spam` buttons. Inside a folder you
find:

| Button | What it does |
|---|---|
| **Run spam now** | Posts immediately, without waiting for the next run |
| **Send message manually** | You pick the exact message to send now |
| **Auto-delete** | Removes the previous message before sending a new one |
| **⏸️ Pause** and **Resume** | Stop and restart the timer without losing the schedule |
| **Delete last sent** | Removes the last batch of messages from every group |
| **📋 List chats** | Shows the groups in the folder |
| **Set timer** and **Delete timer** | Change or remove the schedule |
| **Source channel** | Picks the channel the messages come from |

In the main `/spam` menu, outside the folder card:

| Button | What it does |
|---|---|
| **🔄 Check folders** | Re-reads the folders from your Telegram account |
| **📊 Recent activity** | Summary of how the last runs went |

Three things happen without you asking: the bot posts at the interval you set,
picking a new message from the channel each time; it keeps the pinned message
in your chat with it updated with the result of every run; and it warns you if
your account session stops working.

The bot is free and nobody is authorised to sell it. If somebody is charging
you for it, report it on [@SuperMarioUbot](https://t.me/SuperMarioUbot). The
same channel carries the news and the
[video tutorial](https://t.me/SuperMarioUbot/15).

## Frequently asked questions

### Telegram flagged a "Windows 10 Desktop" session, is it safe?

Yes, that is the bot's connection to your account. Do not terminate it: if you
revoke it the bot stops working.

### I terminated the session by mistake, what now?

Send `/login` again and reconnect the account. Folders, source channels and
timers are all preserved.

### The bot stopped posting

Check the pinned message in your chat with the bot: it shows the result of
every run. The two usual causes are a source channel with no new messages, or
a revoked session. `/errors` tells you which groups rejected the last runs and
why.

### How do I change the source channel?

Send `/spam`, open the folder, tap **Source channel** and pick another one.

### Can I run more than one folder?

Yes. Each folder has its own source channel, timer and settings. Add as many
as you like.

### Does the bot cost anything?

No, it is free. Inside `/spam` there is a **Support ❤️** button with Telegram
Stars and PayPal, but it is a donation towards the running costs and it
unlocks nothing.

### What happens if I run /logout?

The session is deleted from the server and the bot stops posting. To start
again you need a new `/login`.
