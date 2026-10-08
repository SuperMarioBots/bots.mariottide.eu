+++
title = "Master Control Program"
description = "Advanced group administration: automatic bans on suspicious profiles, antispam, mass mute and timed deletion."
weight = 40

[extra]
emoji = "🛡️"
repo = "MasterControlProgramBots"
username = "MasterControlProgramBot"
clonable = true
+++

## What it does

Master Control Program is the administration bot for large groups, the ones
where spam profiles come in waves and nobody wants to check them one by one.
Its strong point are specialbans: you describe what an unwanted profile looks
like (name, bio, language, age, personal channel) and the bot bans on its own
anyone who matches, as soon as they join or as soon as they write.

Around that sit the chores of every group: deleting service messages,
stripping the "forwarded from" header from messages reposted from channels,
limiting how many links a day a person can send, muting newcomers until an
admin unlocks them, banning people who keep joining and leaving, deleting
media after a few hours, finding inactive members.

Every setting is managed with `/msettings`, a button panel that shows how the
group is configured right now. The written commands remain valid and do
exactly the same things: use whichever is more comfortable.

The bot speaks English and Italian. It follows the language of your Telegram
app (Italian for any language other than these two); you can change it at
any time with `/language` or the **🌐 Language** button in the panel.
Messages the bot writes in the group by itself use the language of the person
they are about.

## Before you start

The bot is used in groups (it also works in supergroups with topics). In
private only the information commands answer.

It must be added to the group and promoted to admin. The Telegram permissions
it needs:

- **Delete messages**: for service messages, messages from banned people,
  timed deletion of media and the antispam limit.
- **Ban users**: for specialbans, bans of people who leave, mass mutes.
- **Pin messages**: only if you want it to unpin by itself the posts
  forwarded from the linked channel.
- **Add admins**: only if you use `/addtitle` to give admins custom titles.

If you want the log channel, the bot must be an admin there too.
Details in [Telegram permissions](@/guida/permessi.en.md).

## Setup

1. Add the bot to the group and promote it to admin with the permissions
   above.
2. Write `/msettings` in the group: the panel with every setting opens.
3. Turn on what you need by tapping the buttons. Entries with a value
   (Automute, Leave ban, Spam limit, timed deletion hours) cycle through the
   possible values at every tap.
4. Open **Specialbans** and add the first rules. The panel guides you by
   category: Name, Bio, Language, User age, Personal channel.
5. If you want to keep track of what the bot does, create a channel, add the
   bot as admin, then write `/canalelog` in the group and forward to the
   channel the message the bot gives you. Confirm with **Yes**.
6. Exclude from the automations the people who must stay out of them (service
   bots, editors who forward from channels) with the exclusion commands.

## Commands

### Information

| Command | What it does | Who | Where |
|---|---|---|---|
| `/start` | Welcome message | everyone | private |
| `/help` | Points to the guide and suggests cloning | everyone | private and group |
| `/language` | Switches the bot between English and Italian | everyone | private and group |
| `/clone` | Instructions to create your own clone | everyone | private and group |
| `/ping` | Replies PONG, useful to see if the bot is alive | everyone | private and group |
| `/info` | ID, language and datacenter of a person (in reply, with `@username` or with the ID) | everyone | private and group |
| `/dc` | Only the datacenter, derived from the profile photo | everyone | private and group |
| `/search_id @user` | History of that person's names and usernames | everyone | private |
| `/test` | How many members the group has | everyone | private and group |
| `/stats` | How many clones and how many chats the bot manages | everyone | private and group |

### Settings panel

| Command | What it does | Who | Where |
|---|---|---|---|
| `/msettings` | Opens the button panel with every chat setting | group admin | group |
| `/mimpostazioni` | The same panel, with the Italian name | group admin | group |

### Automatic moderation

| Command | What it does | Who | Where |
|---|---|---|---|
| `/delservice` | Deletes service messages (joins, leaves, photo changes) | group admin | group |
| `/undelservice` | Stops deleting them | group admin | group |
| `/disinoltra` | Reposts messages forwarded from channels without the header, and says who sent them | group admin | group |
| `/undisinoltra` | Turns the unforwarding off | group admin | group |
| `/silent` | The bot stops announcing in chat what it does | group admin | group |
| `/unsilent` | Goes back to announcing it | group admin | group |
| `/sfissadiscussione` | Unpins by itself the posts forwarded from the linked channel | group admin | group |
| `/unsfissadiscussione` | Stops unpinning them | group admin | group |
| `/uscitiban 2` | Bans whoever leaves the group the given number of times (no number means 1) | group admin | group |
| `/unuscitiban` | Turns off the leave ban and resets the count | group admin | group |
| `/automute` | Mutes newcomers until an admin unlocks them | group admin | group |
| `/automutemedia` | Newcomers can write text but not send media | group admin | group |
| `/unautomute` | Turns off the mute on join | group admin | group |
| `/setspamlimit 10` | Daily limit of forwards and Telegram links (invites and `@username` of groups or channels) per person, past which the message is deleted | group admin | group |
| `/unsetspamlimit` | Removes the limit and resets the counts | group admin | group |
| `/specialbans` | Lists the specialban rules active in the group | group admin | group |
| `/specialban bioparziale onlyfans` | Adds a specialban rule | group admin | group |
| `/unspecialban bioparziale onlyfans` | Removes that rule | group admin | group |
| `/setspecialbanreplymessage` | In reply to a media, saves it: the bot will send it after every specialban | group admin | group |
| `/unsetspecialbanreplymessage` | Removes the saved media | group admin | group |
| `/setuscitibanreplymessage` | The same, for the leave bans | group admin | group |
| `/unsetuscitibanreplymessage` | Removes the saved media | group admin | group |

### Exclusions

Every automation can be turned off for a single person. The command works in
reply to one of their messages, with `@username` or with the numeric ID.

| Command | What it does | Who | Where |
|---|---|---|---|
| `/specialbanescludi @user` | That person will never be banned by the specialban rules | group admin | group |
| `/unspecialbanescludi @user` | Removes the exclusion | group admin | group |
| `/disinoltraescludi @user` | Their forwards from channels stay as they are | group admin | group |
| `/undisinoltraescludi @user` | Removes the exclusion | group admin | group |
| `/spamlimitescludi @user` | The daily limit does not apply to them | group admin | group |
| `/unspamlimitescludi @user` | Removes the exclusion | group admin | group |
| `/uscitibanescludi @user` | They can join and leave as much as they like without being banned | group admin | group |
| `/unuscitibanescludi @user` | Removes the exclusion | group admin | group |

### Manual moderation

| Command | What it does | Who | Where |
|---|---|---|---|
| `/listmuted` | Lists every member with active restrictions | group admin | group |
| `/kmute` | Kicks every muted member out of the group | group admin | group |
| `/allmute` | Mutes every member who is not an admin or a bot | group admin | group |
| `/allunmute` | Gives the voice back to every muted member who is not an admin | group admin | group |
| `/minattivi 30` | Looks for people who have not written for that many days (no number, 20) and offers to kick or ban them | group admin | group |
| `/addtitle @user Moderator` | Gives an admin a custom title | group admin | group |
| `/deltitle @user` | Removes admin rights, title included | group admin | group |

### Timed deletion

| Command | What it does | Who | Where |
|---|---|---|---|
| `/setdickcmd evening night` | Defines the words that mark a media for deletion. With no words, turns the feature off | group admin | group |
| `/setdickhours 2.5` | After how many hours to delete (2.5 means two and a half hours) | group admin | group |

Whoever sends a media writes `#evening` in the caption, or replies to their own
media with `/evening`. To change the time for that media only, write
`#evening1h` or `#evening30m`.

### Unsplash

| Command | What it does | Who | Where |
|---|---|---|---|
| `/enableunsplash` | Enables `/unsplash` in the group | group admin | group |
| `/disableunsplash` | Disables it | group admin | group |
| `/unsplash phrase to use` | Turns the phrase into a quote-style image. In reply to a message it uses that message's text | everyone | private, and in groups where it is enabled |

### Log

| Command | What it does | Who | Where |
|---|---|---|---|
| `/canalelog` | Explains how to link the log channel and gives you the message to forward | group admin | group |
| `/setlogchannel` | It is the message to forward to the channel: it starts the confirmation request | group admin | in the log channel |

## Specialban rules

A rule tells the bot what a profile to ban looks like. Add them with
`/specialban <type> <value>`, or from the panel, which asks the same things
as questions. Rules apply only in the group where you write them.

| Type | What it bans | Example |
|---|---|---|
| `nome` | The first name, or first and last name together, is exactly that text (case does not matter) | `/specialban nome Anna` |
| `nomeparziale` | The name contains that text as a whole word, case-insensitive: `escort` does not catch `escortgirl` | `/specialban nomeparziale escort` |
| `nomealfabeto` | The name contains characters of an alphabet: ARABIC, CYRILLIC, GREEK, HEBREW, LATIN | `/specialban nomealfabeto CYRILLIC` |
| `nomewildcard` | The name matches a pattern with the asterisk as wildcard | `/specialban nomewildcard *bitcoin*` |
| `lang` | The person uses Telegram in that language (two-letter code) | `/specialban lang ru` |
| `bio` | The bio is exactly that text (case does not matter) | `/specialban bio looking for friends` |
| `bioparziale` | The bio contains that text as a whole word | `/specialban bioparziale onlyfans` |
| `bioalfabeto` | The bio contains characters of that alphabet | `/specialban bioalfabeto ARABIC` |
| `biotemplate` | The bio falls in a ready-made category: LINK (any link), TELEGRAMLINK (Telegram link), CAM (cam profiles) | `/specialban biotemplate CAM` |
| `biowildcard` | The bio matches a pattern with the asterisk as wildcard | `/specialban biowildcard *t.me/*` |
| `age` | The age stated in the profile is below that number of years | `/specialban age 18` |
| `channel` | The person has a personal channel linked to the profile. Takes no value | `/specialban channel` |

Rules on name and language apply right away. The ones that look at the bio,
the age and the personal channel need to read the full profile, which
Telegram allows at a limited rate: a few seconds of delay is normal. The `age`
rule only works if the person has set their birthday in the profile.

To remove a rule use the same type and the same value
(`/unspecialban bioparziale onlyfans`), or the bin icon next to the rule in the
panel.

## Buttons and automations

When someone joins the group, the bot checks them against the specialban
rules. If a rule matches, it bans them, deletes every message it has already
seen them write, sends the media you saved with `/setspecialbanreplymessage`
and writes what happened in the log channel. The check also runs on normal
messages, so it also catches people who were already inside before the rule
existed, or who change name and bio after joining.

The `/msettings` panel is all buttons: the green tick or the cross shows
whether a setting is on, entries with a number cycle through the available
values at every tap, and the **Timed delete** and **Specialbans** sections
open in a submenu. Specialban rules are added there by answering questions,
and deleted with the bin icon.

`/minattivi` replies with the list of inactive members and two buttons,
**Kick all** and **Ban all**. The list arrives in private, so the chat with the
bot must already be open: if the bot cannot write to you, it gives you a
button to open it. If the list is too long for one message, the bot sends a
link to the full text.

In the log channel, the bot adds by itself the datacenter of whoever joined to
the join messages, and highlights those outside Europe.

The rest works without commands: service messages disappear, forwards from
channels are reposted clean, whoever exceeds the daily limit gets the message
deleted with a notice, newcomers are muted, marked media disappear when time
runs out.

## Frequently asked questions

### Commands or panel?

The panel, because it shows you how the group is set up now. Commands are for
when you already know what you want, or when you need to set something the
panel does not ask, like a long regular expression or an admin title.

### I added a rule but the spam profiles are still inside

Rules do not clean the group by themselves. They apply to whoever joins and
whoever writes: profiles already inside that stay silent are not touched.

### The bot does not ban

Check the **Ban users** permission. If the permission is there, look whether
the person is among the exclusions (`/specialbanescludi` shields them from
every rule) or is an admin: admins are never touched by the automations.

### Why does it not delete old messages?

Telegram lets a bot delete other people's messages only within 48 hours. That
applies to the timed deletion of media and to the cleanup after a ban.

### The log channel stays empty

The bot must be an admin in the channel, with permission to post, and the link
must be confirmed with the **Yes** button that arrives in the group after
forwarding the `/setlogchannel` message.

### `/unsplash` does not work in the group

It has to be enabled once per group with `/enableunsplash`. In private with
the bot it always works.

### Is cloning worth it?

Yes. A clone dedicated to your group does not share Telegram's rate limits
with every other chat, so bans and deletions arrive sooner.
