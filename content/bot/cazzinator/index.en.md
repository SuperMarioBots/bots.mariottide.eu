+++
title = "Cazzinator"
description = "Deletes the media in a group after a delay you choose."
weight = 20

[extra]
emoji = "🍆"
repo = "ToolBoxyBots"
username = "Cazzinator_bot"
clonable = true
+++

## What it does

Put `#dick` in the caption of a photo or a video and the bot deletes it after
a while. The default is two hours, but you can ask for your own delay, for
example `#dick30m`, and an admin can change the default for the whole group.

It keeps media heavy chats clean without anybody deleting things by hand. If
you want everything to go without typing a command each time, `/alldick 3h`
queues every media that lands in the group.

The same bot also carries `/unsplash`: it grabs a random photo and writes your
text over it, in the style of a motivational quote.

## Before you start

- Use it in **groups and supergroups**.
- The bot must be an **admin** with the **Delete messages** permission.
  Without it the bot ignores the delete commands entirely: no reply, no
  complaint. See [Telegram permissions](@/guida/permessi.md).
- Telegram only lets a bot delete other people's messages within **48 hours**,
  which is why delays above 24 hours make no sense and the bot caps them at 24
hours.
- The base command is configurable: here it is `dick`, in a clone it can be
  anything. In that case replace `dick` with your own word in every command
  below, `/setdick`, `/alldick` and `/noalldick` included.

## Configuration

1. Add the bot to the group and promote it to admin with **Delete messages**.
2. Send a photo with `#dick` in the caption. The bot replies with the moment
   the media will disappear.
3. If two hours is not right for your group, an admin sends `/setdick 30m`
   (or `1h30m`, up to 24 hours).
4. For a one off you can override the default by sticking the time onto the
   command: `#dick10m` in the caption, or `/dick10m` as a reply to the media.
5. To delete everything automatically, a group admin sends `/alldick 3h`. `/noalldick` turns
   it back off.

## Commands

The delete commands work with `/` and with `#`. `/unsplash` needs the slash.

### For everyone, in a group

| Command | What it does | Who | Where |
|---|---|---|---|
| `#dick` in the caption | The media is deleted after the group default, two hours unless somebody changed it. It can sit anywhere in the caption | everyone | Group |
| `#dick1h30m` in the caption | The same, with the delay you pick | everyone | Group |
| `/dick` replying to a media | Schedules the deletion of a media already sent | everyone | Group |
| `/dick1h30m` replying to a media | The same, with the delay you pick | everyone | Group |
| `/unsplash text` | Sends a random photo with your text, your name and your username on it | everyone | Group and private |
| `/unsplash` replying to a message | The same, but it takes the text and the name from the message you reply to | everyone | Group and private |

### For group admins

| Command | What it does | Who | Where |
|---|---|---|---|
| `/setdick 1h30m` | Sets the group default delay. The cap is 24 hours, anything above is trimmed | group admin | Group |
| `/alldick 3h` | Turns on automatic deletion of every media in the group and sets the delay. The time is always required | group admin | Group |
| `/noalldick` | Turns automatic deletion off | group admin | Group |

Write the delay with no spaces, in hours and minutes: `30m`, `2h`, `1h30m`.
Send it empty and the bot answers with the correct example.

### If you own a clone

| Command | What it does | Who | Where |
|---|---|---|---|
| `/modules` | Opens the list of the bot's features: tap one to turn it on or off. `/moduli` works too | the clone's owner | Private |

A clone starts with the features picked when it was created, but that is not
final: from `/modules` you can turn the others on, or turn off the ones you do
not need, at any time.

If the bot changes hands, open @BotFather, ask for the bot token with `/token`
and forward that message to the bot itself: from then on it is yours and the
previous owner no longer manages it. Right after that, use `/revoke` in
@BotFather, otherwise whoever had it before can still use the old token.

## Buttons and automatic behaviour

The bot has no buttons.

For every scheduled media it replies with "This message will be deleted" and
the moment it will happen. That notice disappears together with the media, so
nothing is left behind in the chat.

Send the command again on the same media and the old timer is dropped in
favour of the new one. That also covers **editing** the caption to add the
command after sending the media: the bot reads the edited caption.

With albums the bot handles every photo together: the command on one of them
takes all of them away.

With `/alldick` on, the bot queues every photo, video, GIF, sticker, video
note, story and document that arrives in the group, with nobody typing
anything.

## Frequently asked questions

### I wrote `#dick` and nothing happened

Almost always the **Delete messages** permission is missing. The bot stays
quiet when it does not have it, because it already knows the deletion would
fail. Check the word too: in a clone it can be something other than `dick`.

### What are the defaults?

Two hours for a single media, three hours for the automatic deletion of
`/alldick`. An admin changes the first one with `/setdick`.

### Can I set a week?

No. The cap is 24 hours and above it the bot trims the value. That is not an
arbitrary choice: Telegram does not let a bot delete other people's messages
older than 48 hours.

### Does it delete text messages too?

No. The reply form schedules whatever message you replied to, but the
automatic deletion of `/alldick` only looks at media: photos, videos, GIFs,
stickers, video notes, stories and documents.

### Who can turn automatic deletion on?

Group admins only, same as `/setdick`. Everyone else can still have their own
media deleted, by putting `#dick` in the caption or replying to the media with
`/dick`.

### Which photo does `/unsplash` use?

A random one from Unsplash, different every time. The text goes on top in
capitals, with the name of whoever asked, or of whoever wrote the message you
replied to, underneath.
