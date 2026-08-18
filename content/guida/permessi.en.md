+++
title = "Telegram permissions"
description = "Which permissions to give the bot in a group or channel, and what breaks when they are missing."
weight = 2
+++

Telegram never warns a bot that a permission is missing before it tries to act:
the bot finds out when it fails. That is why almost every problem ("it does not
ban", "it does not delete", "it does not pin") is a missing permission.

## How to promote a bot

In the group: **Group info**, **Administrators**, **Add admin**, pick the bot
and tick the permissions. Channels work the same way.

Changing the permissions of an already promoted bot takes effect immediately.
You do not have to remove and re-add it.

## Which permissions each bot needs

| Permission | Needed for | Bots |
|---|---|---|
| Delete messages | Timed media deletion, service messages, wiping a blocklisted user's messages | Cazzinator, Master Control Program, Blocklist, AnonyMedia |
| Ban users | Banning and muting | Blocklist, Master Control Program, CAM Manager |
| Invite users via link | Generating invite links | CAM Manager, Networks |
| Pin messages | Pinning the published list | Networks |
| Add new admins | Setting custom admin titles | Master Control Program (only for `/addtitle`) |
| None, but promoted | Seeing the member list in a group that hides it | Tagga |
| None | The bot works as a normal member, when the member list is visible to everyone | Tagga |

## Privacy mode

By default a bot only reads commands and direct replies, not every message.
The bots that need to read everything already have privacy mode off on my side.

On a clone, you set it yourself in @BotFather: `/mybots`, pick the bot,
**Bot Settings**, **Group Privacy**, **Turn off**. Then remove and re-add the
bot to the group, because Telegram only applies the change on re-join.

## Forum groups (topics)

In forum groups several bots must be configured **inside the right topic**: the
command registers the group plus topic pair, not just the group. This applies
to the staff chat of Blocklist and AnonyMedia and to Better Limitati's operator
chats. Wrong topic means the bot writes in the wrong place: run the command
again from the correct one.

## Hidden member list

A group can hide its member list (in the group settings, under who is allowed
to see the members). Telegram then shows that list to admins only, bots
included.

So a bot that has to mention or count members, like Tagga, sees the admins
alone in that group and mentions just them. The fix is to promote the bot to
admin with every permission box left unticked: it needs the role, not the
powers.

## Telegram limits that are not the bot's fault

- A bot can delete other people's messages only within **48 hours**.
- Mentions are throttled: Tagga can tag at most **5 people per message**.
- A bot cannot see members who never wrote, and cannot list a group's full
  membership.
- Bans in a group the bot just joined take a few minutes: they run in a queue.
