+++
title = "Tagga Bot"
description = "Mentions every member of a group, starting from a single message."
weight = 10

[extra]
emoji = "📢"
repo = "ToolBoxyBots"
username = "Tagga_Bot"
clonable = true
+++

## What it does

Start a message with `@all` and the bot replies mentioning every member of the
group, five at a time. Five is the most Telegram allows in one message, so on
a large group the bot sends a long run of messages, roughly one every three
seconds.

In most groups the bot works as a regular member: it only has to be in the
group and read the message that starts the tag. If the group hides its member
list, though, Telegram shows that list only to admins, so the bot ends up
mentioning admins alone. There you have to promote it, even with every
permission left off.

Everything else is settings: who is allowed to start a tag, how the mentions
look (name, emoji or invisible), whether the bot replies to your message or
copies its text, and which word triggers the tag instead of `all`.

## Before you start

- Use it in **groups and supergroups**: tags only run there. In a private chat
  the bot replies to its guide and to `/clone`.
- Add the bot to the group. If the member list is visible to everyone, a
  **regular member** is enough.
- If the group **hides its member list**, promote the bot to **admin**, or
  Telegram will only show it the admins and the tag will mention just them.
  It needs no permissions: promote it and leave every box unticked. See
  [Telegram permissions](@/guida/permessi.md).
- It works in forum groups too: every topic has its own running tag,
  independent from the others.
- The bot never mentions other bots or deleted accounts.

## Configuration

1. Add the bot to the group. If the group settings hide the member list,
   promote it to admin without ticking any permission.
2. Write a message that **starts** with `@all`, for example
   `@all meeting at 9pm`. `#all` and `/all` work as well.
3. The bot confirms with "Command accepted successfully" and starts tagging.
4. If only admins should be allowed to use it, send `/onlyadmins`.
5. Pick how the mentions look: `/nametagtype` (the default),
   `/emojitagtype` or `/emptytagtype`.
6. If you would rather have the bot copy your text than reply to your message,
   send `/copymessage`.
7. If `all` is not the word you want, change it with
   `/set_tag_command announce`: from then on the tag starts with `@announce`.

## Commands

The message has to **start** with the trigger word: `@all everyone` works,
`everyone @all` does not.

### For everyone, in a group

| Command | What it does | Who | Where |
|---|---|---|---|
| `@all message` | Starts tagging every member, five per message. `#all` and `/all` work too | everyone, or admins only if you sent `/onlyadmins` | Group |
| `/stopall` | Stops a running tag. `@stopall` and `#stopall` work too | whoever started the tag, or a group admin | Group |
| `/lottery` | Draws one random member of the group and announces them | everyone | Group |

### For group admins

| Command | What it does | Who | Where |
|---|---|---|---|
| `/onlyadmins` | The bot accepts tags from admins only | group admin | Group |
| `/noonlyadmins` | The bot accepts tags from anybody | group admin | Group |
| `/copymessage` | The bot copies the text of your message instead of replying to it, and adds a link back to the original | group admin | Group |
| `/nocopymessage` | The bot goes back to replying to the message | group admin | Group |
| `/nametagtype` | Mentions show the person's first name. This is the default | group admin | Group |
| `/emojitagtype` | Mentions show a random face emoji instead of the name | group admin | Group |
| `/emptytagtype` | Mentions are invisible: the notification still arrives, but the message looks empty | group admin | Group |
| `/set_tag_command announcement` | Changes the word that starts a tag in that group | group admin | Group |
| `/unset_tag_command` | Restores the default word | group admin | Group |

These settings apply to the whole group, even if you send them inside a
topic.

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

The bot has no buttons: everything runs on commands.

When it joins a group it registers its own command menu, so the commands show
up in the `/` list without you doing anything.

One tag at a time per topic. If somebody starts another one while the first is
still running, the bot answers that a tag is already in progress and deletes
that warning a few seconds later.

When the bot replies to the message that started the tag and that message gets
deleted, the bot stops and says the original is gone.

The waiting message ("the bot will start tagging as soon as possible")
disappears on its own once the first batch of mentions goes out.

## Frequently asked questions

### Why only five people per message?

That is a Telegram limit, not a bot limit: one message cannot carry more than
five mentions. A group of a thousand people takes two hundred messages, with a
pause between them so Telegram does not throttle the bot.

### Do I have to make it an admin?

Only if the group hides its member list. Telegram then keeps the members
hidden from non-admins, so the bot mentions the admins alone. Promoting it
with no permission ticked fixes it. In every other group it is not needed.

### The tag skipped some people

If it mentioned the admins only, the group hides its member list and the bot
is not an admin: promote it. The bot also never mentions other bots or deleted
accounts. If real people are missing, the tag almost certainly stopped early:
check that the original message is still there and that nobody sent
`/stopall`.

### How do I stop a tag started by mistake?

`/stopall`. Whoever started the tag can use it, and so can any group admin.

### Can I trigger the tag with my own word?

Yes, a group admin sends `/set_tag_command` followed by the word they want. It
applies to that group only, and from then on the old word stops working.
`/unset_tag_command` brings the default back.

### What is the difference between the three mention styles?

`/nametagtype` shows names and is the readable one. `/emojitagtype` replaces
names with face emoji and keeps the message short. `/emptytagtype` uses an
invisible character: the notification still arrives, but the message looks
empty.

### It is slow on my group

The public bot serves thousands of chats and Telegram limits are shared across
all of them. A bot dedicated to your group starts sooner and finishes sooner.
