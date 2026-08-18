+++
title = "Better Limitati"
description = "An anonymous help desk: whoever writes to the bot talks to the whole staff, without knowing who answers."
weight = 50

[extra]
emoji = "⚔️"
repo = "BetterLimitatiBots"
clonable = false
+++

## What it does

Better Limitati puts a bot between people and your staff. A user writes to the
bot in private, the message lands in the operator chat (a group, or a single
topic of a forum group), an operator answers by replying to that message, and
the answer goes back to the user in private. The user only ever sees the bot:
no operator name, no group to join, no way back to your staff.

An operator's reply is also mirrored into every other operator chat, showing who
answered whom. If your staff is spread over several groups or topics, nobody
answers the same question twice. Edits and reactions travel both ways: if the
user fixes a message, the copy in the operator chat is updated too, and the
other way around.

Two typical uses: group verifications (the user's video note or voice message
lands in the staff group, with no contact exchanged) and a way in for people
Telegram has limited, who cannot write privately to anyone who has not saved
their number. They can still write to the bot.

This bot has no automatic clone button: you get it on request. If you need one,
write to me from [Support and contacts](@/guida/supporto.md) and I will set up
your own instance, with your groups and your operators.

## Before you start

You need somewhere to receive messages: a staff group is fine. If the group has
topics, you can register a single topic and keep the help desk apart from the
rest of the chatter.

Add the bot to the group. It does not have to be an administrator, because
operators reply to the bot's own messages and those replies always reach it. If
you plan to use `/onlyadmins`, keep the bot in the group before running the
command: that is where it reads the list of group administrators.

In forum groups the topic you write from matters: the command registers the
group and the topic together. Write from the wrong topic and messages land in
the wrong place.

## Setup

1. Ask me for the bot from [Support and contacts](@/guida/supporto.md). It comes
   ready, with you as its first administrator.
2. Add the bot to your staff group.
3. Send `/addchat` in the group, or inside the topic you want to use. From then
   on user messages arrive there.
4. Add the rest of your staff with `/addadmin` (replying to one of their
   messages, or with their `@username`). Whoever becomes an administrator also
   gets copies of the messages in private.
5. Check with `/listchats` that only the chats you want are registered.
6. Customise the welcome with `/setstart` and the confirmation users get after
   writing with `/setreply`.
7. If only your leads should answer, send `/onlyadmins` in the operator chat.

## Commands

### For people writing to the bot

| Command | What it does | Who | Where |
|---|---|---|---|
| `/start` | Starts the bot and shows the welcome message | everyone | private |
| `/help` | Shows the default welcome message, even if you changed it with `/setstart` | everyone | private |
| `/ping` | Replies `PONG`, only useful to check the bot is alive | everyone | anywhere |
| `/language` | Pick the bot language from a list of buttons | everyone | private |

### For bot admins

| Command | What it does | Who | Where |
|---|---|---|---|
| `/addchat` | Registers the chat (or topic) you write from as an operator chat | bot admin | group, topic or private |
| `/delchat` | Removes that chat from the operator chats | bot admin | group, topic or private |
| `/listchats` | Lists the registered operator chats | bot admin | anywhere |
| `/addadmin @user` | Adds a bot administrator and registers their private chat as an operator chat | bot admin | anywhere |
| `/deladmin @user` | Removes an administrator and their private chat | bot admin | anywhere |
| `/listadmins` | Lists the administrators | bot admin | anywhere |
| `/addban @user` | Stops someone from writing to the bot | bot admin | anywhere |
| `/delban @user` | Lifts the ban | bot admin | anywhere |
| `/listbans` | Lists banned people | bot admin | anywhere |
| `/onlyadmins` | In that operator chat, only group administrators can answer | bot admin | in the operator chat |
| `/noonlyadmins` | Lets anyone answer again | bot admin | in the operator chat |
| `/original` | Replying to a received message, brings back the original with its sender | bot admin | in the operator chat |
| `/setstart Hi there!` | Sets the welcome message. Telegram formatting is not kept: for bold, type the HTML tags, for example `<b>hi</b>` | bot admin | anywhere |
| `/unsetstart` | Back to the default welcome | bot admin | anywhere |
| `/setreply We will answer soon` | Sets the confirmation users get after writing | bot admin | anywhere |
| `/unsetreply` | Back to the default confirmation, the one that disappears on its own | bot admin | anywhere |
| `/hidestart` | User `/start` messages do not reach the operator chats | bot admin | anywhere |
| `/unhidestart` | Shows them again | bot admin | anywhere |
| `/hidehelp` | User `/help` messages do not reach the operator chats | bot admin | anywhere |
| `/unhidehelp` | Shows them again | bot admin | anywhere |
| `/setbuttons` | Puts a keyboard of buttons under the user's chat | bot admin | anywhere |
| `/unsetbuttons` | Removes the keyboard | bot admin | anywhere |

Bot administrators who send `/start` or `/help` in private get this list instead
of the welcome message.

### The /setbuttons syntax

Buttons go in the same message as the command: every new line is a keyboard row,
columns are separated by `||`. For example:

```
/setbuttons Support||Report
How it works
```

gives two buttons side by side (Support and Report) and a wide one below (How it
works). Tapping a button is the same as typing that text, so the message reaches
the operators like any other. `/unsetbuttons` takes the keyboard away.

## Buttons and automatic behaviour

Most of the work happens with no commands at all. Every private message reaching
the bot is copied to all operator chats, with the sender's name and ID on top.
Photos, voice messages, video notes, documents and polls arrive as they are;
forwarded messages stay forwards, so you can see where they came from.

To answer, reply to the message in the operator chat and write: the answer goes
to the user in private, attached to the right message. A confirmation appears in
the operator chat and deletes itself after a few seconds, to keep things clean.
The other operator chats get a copy of the answer instead, showing which
operator answered which user.

Reply chains are kept as well: if the user quotes a staff answer, operators see
it quoted, and the other way around. Edits and reactions propagate both ways.
If the user has blocked the bot, the operator finds out right away, because the
bot says so in the chat.

## Frequently asked questions

### Can the user find out who the operators are?

No. They only see the bot. Staff names and groups stay on the operator side, and
answers reach the user from the bot.

### How does it work in groups with topics?

Open the topic you want and send `/addchat` from there. Group and topic are
registered together, so messages land in that topic and nowhere else. You can
register several topics of the same group.

### Can I have more than one operator group?

Yes, as many chats as you like. Every message reaches all of them, and every
answer is mirrored into the ones where it was not written.

### Who can answer users?

By default anyone in the operator chat. With `/onlyadmins` only the group
administrators (and the bot administrators) can answer in that chat.

### Someone is being abusive

`/addban`, replying to one of their messages or with their `@username`. From
then on nothing they write reaches anyone. `/delban` puts things back.

### Why do I get the messages in private too?

Because `/addadmin` also registers the new administrator's private chat. If you
do not want that, send `/delchat` in your private chat with the bot: you stay an
administrator, but stop receiving copies.

### How do I get it?

On request, there is no automatic clone button. Write to me from
[Support and contacts](@/guida/supporto.md).
