+++
title = "AnonyMedia"
description = "Send photos and videos to your groups without anyone knowing who sent them."
weight = 60

[extra]
emoji = "🕵🏻"
repo = "AnonyMediaBots"
username = "AnonyMediaBot"
clonable = true
+++

## What it does

AnonyMedia posts photos, videos, GIFs, documents and video messages to groups
on your behalf. People in the group see a post from the bot, not your name:
the media stays anonymous for everyone except the staff, who always know who
sent what.

You use it in a private chat with the bot. You write to it, pick the group
from the list and send the media. If you are whitelisted the post goes out
right away, otherwise it goes through the staff first, who approve or discard
it with buttons.

Every published media carries the button
**😏 Send media anonymously 😏**, so whoever sees it in the group can do the
same with one tap.

The bot speaks English and Italian. It follows the language of your Telegram
app (Italian for any language other than these two); you can change it at
any time with `/language`.

## Before you start

To use it as a member you need little: being in a group where the bot already
is. The list of groups it offers you is built on that, so if you have not
written in a long time the group may not show up: send a message in the group
and try again.

To enable it on one of your groups you need two chats:

- The **public chat**, the group where the media will appear. The bot must be
  in it and able to write. Channels cannot be linked: Telegram does not
  deliver to bots the commands written in them.
- The **staff chat**, a separate group where the media to review arrive. You
  need it even if you plan to approve everything: it is where whitelist and
  moderation are run from.

It is worth giving the bot the **Delete messages** permission in the public
chat too: without it, `/delete` leaves the command behind and the automatic
deletion after two hours does not always succeed. Details are in
[Telegram permissions](@/guida/permessi.en.md).

## Setup

1. Create the staff group and add the bot to it.
2. In the staff group send `/register`. The bot replies with a `/confirm`
   command followed by a code, valid for 15 minutes.
3. Copy that command and have it sent **in the public group** by someone who
   is an admin there. The bot checks that the sender really is an admin there.
4. The bot confirms in both chats: from then on the two are linked.
5. If the staff group is a forum, send `/register` inside the topic where you
   want to receive the media: review requests will arrive there.
6. Whitelist the people you trust with `/whitelist`, so their media go out
   without passing through moderation.

To redo the link (for example after changing staff group) just repeat
`/register` and `/confirm`: the latest registration replaces the previous one.

## Commands

### For senders

| Command | What it does | Who | Where |
|---|---|---|---|
| `/start` | Shows the groups you can post to and starts the upload | everyone | private chat |
| `/help` | Explains how to use it | everyone | anywhere |
| `/delete` | In reply to a published media, deletes it. Works only if you sent that media | the sender of that media | in the group |
| `/language` | Switches the bot between English and Italian | everyone | anywhere |
| `/clone` | Explains how to create your own copy of the bot | everyone | private chat |
| `/ping` | Replies `PONG`, only useful to check the bot is alive | everyone | anywhere |

### For the staff

| Command | What it does | Who | Where |
|---|---|---|---|
| `/register` | Generates the code to use with `/confirm` to link a group | staff | in the staff group |
| `/confirm CODE` | Completes the link | group admin | in the public group |
| `/whitelist @someone` | Whitelists one or more people: their media go out unchecked. Numeric IDs work too | staff | in the staff group |
| `/delwhitelist @someone` | Removes from the whitelist | staff | in the staff group |
| `/inwhitelist @someone` | Tells whether a person is whitelisted | staff | in the staff group |
| `/whitelists` | Lists everyone on the whitelist | staff | in the staff group |
| `/tagwhitelist` | Mentions the whitelisted people still in the group, five per message | staff | in the staff group |
| `/help` | Summary of the staff commands | staff | in the staff group |

## Buttons and automations

When a media to review arrives, the staff get it with five buttons:

- **✅ Accept** publishes the media in the group.
- **❌ Reject** discards it and publishes nothing.
- **🍆 Dick (2h)** publishes the media and deletes it by itself after two
  hours. The group sees the notice "This message will be deleted in 2 hours",
  and the copy left in the staff chat disappears too.
- **🚫 Ban** discards the media and stops that person from sending more to
  that group through the bot. It does not touch their group membership.
- **✅ Whitelist + Accept** publishes the media and whitelists the sender, so
  next time it skips the review.

Once handled, the message in the staff chat loses its buttons and shows who
decided what.

The review card and the buttons under the published media use the language
of the person who sent the media.

If you write `#dick` (or `/dick`) in the caption, the media deletes itself
after two hours even when approved normally.

You do not have to start from `/start`: you can send the media to the bot and
pick the group afterwards. In forum groups the bot also asks which section to
post in. After every upload the buttons **📤 Send another** and
**📤 Same group** appear, to repeat without choosing again.

On published media the bot applies a watermark with the chat's username, or
with its name if it has no username. It is on by default and there is no
command to turn it off.

## Deep link: send people straight to your group

If you put a button or a link with this address, whoever taps it opens the bot
already set to your group and skips picking from the list:

```
https://t.me/AnonyMediaBot?start=CHAT_ID
```

Replace `CHAT_ID` with the group's numeric ID, the one starting with `-100`.
It is the same link the bot puts under every published media. The check stays:
if whoever taps the link is not in the group or was banned by the bot, nothing
gets posted.

## Frequently asked questions

### Does the staff know who I am?

Yes. Anonymity applies towards the group, not towards the moderators: in the
staff chat your media arrives tied to your account, and the bot warns that
abuse gets you banned. If you are whitelisted the media does not go through
the staff chat, but it is still recorded.

### The bot says I am not in any group.

Only the groups where both you and the bot are show up. If you have not
written in a long time, send a message in the group and tap **🔄 Reload**.

### I sent a video and nothing came out.

Above 20 MB the bot cannot process the file and the request is discarded.
Send a lighter file, or compress the video first.

### Can I delete a media already published?

Yes, but only yours: reply to that media in the group with `/delete`. The bot
checks that it came from you and deletes it. On other people's media the
command does nothing.

### "You are sending too much media. Wait a minute and try again."

There is a limit of three uploads per minute each. Wait sixty seconds and
start again.

### The `/confirm` code no longer works.

It lasts fifteen minutes. Generate a new code with `/register` in the staff
group, keeping in mind that the bot makes you wait half a minute between one
code and the next.

### Can I use it on a channel?

No. Telegram does not deliver to bots the commands written inside a channel,
so `/confirm` from there never arrives and the channel cannot be linked. Both
the public chat and the staff chat must be groups.
