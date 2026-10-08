+++
title = "Watermark Bot"
description = "Puts your signature diagonally on the media you send it."
weight = 70

[extra]
emoji = "📸"
repo = "WatermarkBots"
username = "overprint_bot"
clonable = true
+++

## What it does

You set a signature once, then send the bot a photo, a video, a GIF, a video
message or a document, and the bot sends it back with the signature written
diagonally across it, from the bottom left corner to the top right one.

The signature is your own text: a name, a username, the name of a channel. You
can pick one of eight script fonts, and under every signed media you find four
buttons to redo it lighter, darker, smaller or larger until you like it.

The bot does not go through the standard bot API, so it also accepts files
well above 50 MB: long videos are fine, they just take longer.

The bot speaks English and Italian. It picks the language of your Telegram
app the first time you write to it; you can change it at any time with
`/language`.

## Before you start

- Use it **in private chat only**: in groups it only answers `/ping`, so do
  not add it.
- It needs no permissions and does not have to be promoted anywhere.
- Without a signature the bot does nothing: if you send a media before
  setting anything up, it replies asking you to set the signature.

## Setup

1. Open the bot and send it `/start`.
2. Tap **✍ Set signature** and type the text you want as your signature.
   Or do it all at once with `/signature Mario`.
3. If the default font does not convince you, tap **🔠 Set font** and pick
   another one of the eight available.
4. Send a media. The bot replies with a waiting message and then with the
   signed media.
5. Use the buttons under the result to adjust shade and size.

Signature and font stay saved: you set them once and they apply to every
following media, until you change them.

## Commands

| Command | What it does | Who | Where |
|---|---|---|---|
| `/start` | Welcome message with the setup buttons | everyone | Private |
| `/help` | Short description of the bot and a link to this guide | everyone | Private |
| `/signature Mario` | Sets the signature in one go, without the buttons | everyone | Private |
| `/firma Mario` | Same as `/signature` | everyone | Private |
| `/language` | Switches the bot between English and Italian | everyone | Private |
| `/clone` | Explains how to create your own copy of the bot: you create the bot on @BotFather and forward it the message with the token | everyone | Private |
| `/ping` | Replies `PONG`, only useful to check the bot is alive | everyone | anywhere |

If you send `/signature` with nothing after it, the bot asks you to send it
again followed by the signature.

## Buttons and automations

**✍ Set signature** asks a question: the next message you write becomes your
signature, spaces and emoji included.

**🔠 Set font** shows the eight available fonts. Pick one and it applies right
away to the following media.

**🌐 Language** opens the language picker, the same as `/language`.

Under every signed media there are four buttons, and each one redoes the
render starting from the original media:

- **🔅** lighter, the signature shows less.
- **🔆** darker, the signature shows more.
- **➖** smaller.
- **➕** larger.

You can press them as many times as you like, even one after the other. Past
a certain point the bot stops changing, because below or above some values the
signature would vanish or cover everything.

Every render goes through a queue. The waiting message tells you how many
media are ahead of yours: a long video can take several minutes. Photos and
videos have separate queues, so a photo does not get stuck behind a movie.

## Frequently asked questions

### I sent a video and the bot seems stuck

It is not: it is working. The waiting message says it plainly: do not send the
same media again thinking the bot is stuck. Every copy you send lands at the
end of the same queue and makes the wait longer for you and everyone else.
Just wait.

### Can I send big files?

Yes. The 50 MB limit of the standard API does not apply here. The bigger the
file, the longer it takes.

### What does it accept?

Photos, videos, GIFs, video messages and documents. An image sent as a file
comes back as a file, not as a photo.

### Does the signature always come out the same?

On photos yes: with the same settings two passes on the same file give the
same result. On videos the angle changes a little at every render, so two
copies of the same video never come out identical.

### Can I change my signature?

Whenever you want, with `/signature` or with the button. It applies from the
next media; the ones already signed stay as they are.

### Does anyone see my media?

Yes, in part, and it is better to say so. Every media that reaches the public
bot is automatically forwarded to a private review channel that I read,
together with the name of the sender, the signature and the font used. It
helps me understand what goes through the bot and act on abuse. It does not
happen on clones: your own clone forwards nothing anywhere. If you are not
fine with that, clone the bot or do not send it anything you would not send
to me.
