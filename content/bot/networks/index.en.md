+++
title = "Networks Bot"
description = "Runs exchange lists and spam lists: group bookings, list publishing and scheduled posts."
weight = 90

[extra]
emoji = "🌐"
repo = "NetworksBots"
clonable = true
+++

## What it does

This bot is for people who run a list: spam lists, exchange lists, networks of
groups and channels that trade visibility with each other. If you do not run a
list and you are not trying to get into somebody else's, you almost certainly
do not need it.

The mechanism is always the same. Whoever runs the list opens the bookings in
a dedicated chat, the owners of the groups and channels write the booking
command there and pick which chats they want on the list, then the list owner
closes the bookings and the bot publishes the full list in every booked chat,
with the text and the buttons they configured. From there the bot can repeat
the post on a schedule, pin it, delete it and open the next round.

The bot also has a second personality, forwarding mode, which has nothing to
do with lists: it takes messages from a source chat and repeats them in every
destination chat. You turn it on from the settings and it is described further
down.

There is no public bot you can just add and go: every list lives in its own
clone, with its own admins, chats and settings. If the list is yours, creating
one is the first step.

## Before you start

There are three roles and it pays to keep them apart.

- **User**: anybody. Adds their own group or channel, books it, writes to the
  staff.
- **Manager**: runs the day to day work, meaning chats, bookings, scheduled
  posts and bans.
- **Superuser**: a manager who can also create other managers and move the
  bot's service chats.

The bot works in three different places: your private chat with it, the staff
chat (if the list owner set one up) and the booking chat, where the booking
commands are typed.

In your group or channel the bot has to be an administrator. The permissions
it needs:

- **Delete messages**, to remove the old post before putting up the new one;
- **Pin messages**, to pin the list when the schedule says so;
- **Invite users via link**, to generate the link to your chat that goes on
  the list.

When you promote it or change its permissions, the bot sends the managers a
summary and tells you whether the permissions are enough or which ones are
missing. See also [Telegram permissions](@/guida/permessi.md).

## Setup

### If you want to join somebody else's list

1. Add the list's bot to your group or channel and promote it administrator
   with the permissions above.
2. Wait. The list managers get a notification and have to tap **Add to list**:
   until they do, your chat cannot be booked.
3. When bookings are open, go to the list's booking chat and type the booking
   command, usually `#prenota`.
4. The bot opens the list of chats where you are an administrator. Tap the
   ones you want on the list and press **✅ Confirm ✅**.
5. If you change your mind before the round closes, `#sprenota` takes a chat
   back out.

If the list works with join requests, your chat shows up as booked "with
approval": whoever arrives through the link has to be accepted by hand.

### If you run a list of your own

1. Ask for your clone, which starts with you as superuser. See
   [Create your own clone](@/guida/clone.md).
2. Create the booking chat (a group where people will type `#prenota`), put
   the bot in it and run `/setreschat` right there.
3. If you want a staff chat, where the messages people write to the bot in
   private land, create that too and run `/setstaff` inside it. That is also
   the only place the ban commands work.
4. Add your managers with `/addmanager`, and any other superusers with
   `/addsuperuser`.
5. Send `/start` to the bot in private and open **⚙️ Settings**. Here you
   prepare the list template message, the pinned buttons at the top and at the
   bottom, the sublists, the list format and, if you want, a booking tag other
   than `prenota`.
6. As people add the bot to their own chats, the managers get the
   notification and tap **Add to list** to authorise them.
7. When the time comes, type `/aperte` in the booking chat. At the end of the
   round, `/chiuse`.
8. To publish, use **📨 Schedule Post** from the menu: you forward the message
   to publish and the bot walks you through when, how often, where, whether to
   pin it and whether to open or close the bookings along with the post.

You can run more than one list: **➕ Add list** in the main menu creates
another one, each with its own booking chat, its own tag and its own settings.

## Commands

The booking command is not fixed. `prenota` is only the starting value: each
list can use its own, chosen by the owner in **⚙️ Settings**,
**#️⃣ Configure #reserve tag**. If a list uses `normale`, the commands become
`#normale`, `#sprenotanormale`, `/apertenormale`, `/chiusenormale`. Below they
are written with the starting value.

The command names stay Italian in every language, because they are the ones
the bot listens for.

### For everybody

| Command | What it does | Who | Where |
|---|---|---|---|
| `/start` | Introduces the bot. If there is a staff chat, this is where you write to the managers | everyone | private |
| `#prenota` | Opens the list of your chats and lets you book the ones you want | everyone | booking chat |
| `#sprenota` | Takes one of your chats back out of the running list | everyone | booking chat |
| `/clone` | Asks for an independent copy of the bot | everyone | private |
| `/language` | Changes language | everyone | anywhere |
| `/paysupport` | Contact for payment problems | everyone | anywhere |
| `/ping` | Checks that the bot is alive | everyone | anywhere |

Both `#prenota` and `/prenota` work, but only inside that list's booking chat.

### For managers

| Command | What it does | Who | Where |
|---|---|---|---|
| `/aperte [members] [gruppi\|canali]` | Opens the bookings. The number is the minimum member count required, the keyword limits the round to groups only or channels only | manager | booking chat |
| `/chiuse` | Closes the bookings | manager | booking chat |
| `/addchat` | Registers a chat by forwarding a message from it | manager | private, staff chat |
| `/delchat` | Removes a chat from the bot | manager | private, staff chat |
| `/add <chat_id> [name]` | Puts an already registered chat on the list by hand | manager | private, staff chat |
| `/del <chat_id>` | Takes a chat off the list by hand | manager | private, staff chat |
| `/adddefault [chat_id]` | The chat joins the list by default on every round | manager | anywhere |
| `/deldefault [chat_id]` | Removes that default | manager | anywhere |
| `/addcontroller [chat_id]` | The chat receives the posts but never shows up in the published list | manager | anywhere |
| `/delcontroller [chat_id]` | The chat goes back to appearing on the list like the others | manager | anywhere |
| `/setrequest [chat_id]` | The chat goes on the list with a join request link | manager | anywhere |
| `/unsetrequest [chat_id]` | Back to a direct link for that chat | manager | anywhere |
| `/newlink <chat_id> <link>` | Forces a fixed link for a chat instead of the generated one | manager | private, staff chat |
| `/dellink <chat_id>` | Back to the link the bot generates | manager | private, staff chat |
| `/check [chat_id]` | Checks the bot permissions across the chats | manager | private, staff chat |
| `/escilo <chat_id>` | Makes the bot leave the listed chats | manager | anywhere |
| `/generate` | Rebuilds the list text from the template | manager | private, staff chat |
| `/staff` | Lists the current chat's administrators, split by role | manager | group |
| `/admins` | Shows the administrators the bot has cached | manager | private, staff chat |
| `/reload_admins` | Re-reads the admins of every chat from Telegram | manager | private, staff chat |
| `/counts` | Counts the members of every chat | manager | private, staff chat |
| `/addban` | Blocks a user, also by replying to their message in the staff chat | manager | private, staff chat |
| `/delban` | Unblocks a user | manager | private, staff chat |
| `/listbans` | Lists the blocked users | manager | private, staff chat |
| `/check_staff_banned` | Checks whether any blocked user is still around | manager | private, staff chat |

The ban commands only exist once the owner has set up a staff chat.
`/reload_admins` and `/counts` are slow: the bot warns you it takes minutes.

### For superusers

| Command | What it does | Who | Where |
|---|---|---|---|
| `/addmanager <user>` | Adds a manager | superuser | anywhere |
| `/delmanager <user>` | Removes a manager | superuser | anywhere |
| `/listmanagers` | Lists the managers | superuser | anywhere |
| `/addsuperuser <user>` | Promotes somebody to superuser | superuser | anywhere |
| `/delsuperuser <user>` | Back to plain manager | superuser | anywhere |
| `/listsuperusers` | Lists the superusers | superuser | anywhere |
| `/setreschat` | Makes the chat you type it in the booking chat | superuser | in the chosen chat |
| `/unsetreschat` | Drops the booking chat of the current list | superuser | anywhere |
| `/setstaff` | Makes the chat you type it in the staff chat | superuser | in the chosen chat |
| `/unsetstaff` | Drops the staff chat | superuser | anywhere |

After `/setstaff` and `/setreschat` the bot restarts itself to apply the
change: a few seconds and it answers again.

## Buttons and automatic behaviour

The `/start` menu for managers holds these entries:

| Button | What it does |
|---|---|
| **📨 Schedule Post** | You forward a message and the bot walks you through when, how often, in which chats, whether to pin it, whether to open or close the bookings along with it |
| **🗒 List Scheduled Posts** | The queued posts, with text editing, per chat links and deletion |
| **⚙️ Settings** | Template, buttons, sublists, list format, booking tag |
| **➕ Add Channel** and **➖ Remove Channel** | Register or drop a chat by forwarding a message from it |
| **🗒 List chats** | The chats registered on the bot |
| **➕ Add list** and **➖ Remove list** | Run several lists in parallel on the same bot |
| **🌐 Language** | Changes language |
| **📔 Guide** | Opens the bot guide |
| **Support ❤️** | Donation with Telegram Stars or PayPal |
| **❌ Close** | Closes the menu |

Inside the settings: **💌 Configure template message** is the list text,
**⬆️ Configure top pinned buttons** and **⬇️ Configure bottom pinned buttons**
add buttons above and below, **🔗 Configure "dummy" link** is the link the
separators use, **📑 Configure sublists** splits the list into sections,
**📋 Configure list format** decides the columns and the behaviour in groups
with topics, **#️⃣ Configure #reserve tag** changes the booking command. When the bot runs a
single list and has no slave bots, **🤖 Configure master bot** shows up too.

Without anybody typing anything, the bot:

- warns the managers when somebody adds or removes it from a chat, with the
  **Add to list**, **Check**, **Administrators** and **Remove the bot**
  buttons;
- checks the permissions on every role change and says what is missing;
- publishes the scheduled posts at the set times, pins them if you asked for
  it and deletes the previous post;
- opens and closes the bookings along with the post, if the schedule says so;
- forwards to the staff whatever users write to it in private, and carries the
  staff replies back to the user;
- puts chats that keep rejecting the posts on hold for a week instead of
  retrying forever;
- rate limits anybody repeating `#prenota` too fast, with a "Too fast! Wait
  ... and try again".

## Forwarding mode

**📡 Switch to forwarder mode** changes the bot's job. The whole list and
booking side disappears and what is left is a forwarder: you define one or
more source chats and one or more destination chats, and every message that
shows up in a source is repeated in the destinations. **📋 Switch to scheduler
mode** takes you back.

The menu for this mode is all toggles, which flip when you tap them:

| Toggle | What it changes |
|---|---|
| **Forward new messages** | The master switch for forwarding |
| **Copy messages** or **Forward messages** | With copy the origin is hidden, with forward it is visible |
| **Forward messages with inline buttons** | Passes or drops messages carrying buttons |
| **Forward messages containing links** | Passes or drops messages containing links |
| **Notify managers of chat moves** | Tells the managers about every add, removal or role change |
| **Approval mode for new destinations** | A fresh destination only receives once a manager approves it |
| **Replay last message when bot joins** | As soon as it joins a new chat, it posts the latest message there |
| **Allow replies to forwarded posts** | Whoever replies to a post in a destination is put in touch with whoever wrote it |
| **Repost latest message** or **Repost random message** | What the repeat timer publishes |

The other entries are **➕ Add channel**, **➖ Remove channel**, **🗒 List
chats**, **⏰ Repeat** (how many seconds between reposts, zero to turn it off)
and **⟳ Refresh message cache**.

| Command | What it does | Who | Where |
|---|---|---|---|
| `/addchat [chat_id [topic_id]]` | Marks a chat as a source | manager | anywhere |
| `/delchat [chat_id [topic_id]]` | Drops the source chat | manager | anywhere |
| `/listchats` | Lists sources and destinations | manager | anywhere |
| `/approve [chat_id [topic_id]]` | Approves a waiting destination | manager | anywhere |
| `/setexpiration <days> [chat_id [topic_id]]` | Gives the source an expiry date. A negative number brings it forward | manager | anywhere, the source included |
| `/unsetexpiration [chat_id [topic_id]]` | Removes the expiry | manager | anywhere, the source included |
| `/enabletopic <chat_id> <topic_id>` | Turns a topic into a destination | manager | anywhere |
| `/disabletopic <chat_id> <topic_id>` | Turns that topic off | manager | anywhere |
| `/enablesourcetopic <chat_id> <topic_id>` | Turns a topic into a source | manager | anywhere |
| `/disablesourcetopic <chat_id> <topic_id>` | Turns that source topic off | manager | anywhere |
| `/forward` | Replying to a message in the source, sends it to every destination right away | manager | source chat |

## Frequently asked questions

### I typed #prenota and the bot said nothing

The command only works inside that list's booking chat, and only while the
bookings are open. If they are closed the bot answers that it cannot take the
booking because bookings for this list are not currently open.

### The bot says I am not an admin of any booked chat

It means none of the chats where you are an administrator has been authorised
by the list managers, or none of them meets the requirements of the round in
progress: minimum member count, groups only or channels only. Add the bot to
your chat and wait for a manager to tap **Add to list**.

### I cannot find #prenota, this list uses another word

Every list can change the tag. Look at the message that opened the bookings:
the right command is written there.

### I removed a chat by mistake, can I put it back?

Yes, while the bookings are still open. Type the booking command again and
select the chat.

### The post never arrived in my group

In order: the bot is still an administrator, it still has **Delete messages**
and **Pin messages**, and your chat really is on the list this round. A
manager can run `/check` to see the permissions chat by chat. If your chat has
been rejecting posts for days, the bot puts it on hold for a week.

### What does "with approval" next to my chat mean?

That your chat goes on the list with a join request link: whoever comes
through the link does not walk straight in, they have to be accepted. A list
manager decides it with `/setrequest`.

### What is the staff chat for?

It is where the messages users write to the bot in private end up. Managers
answer by replying to the message and the reply travels back to the user. It
is also the only place where the ban commands work.

### Do I have to create a clone?

If you run a list of your own, yes: chats, managers and settings all live in
the clone, and no public bot can host somebody else's list. If you only want to
join someone else's list, they already have the clone: you just add the bot
they point you to.

### Why did the bot restart after /setstaff?

Because those settings change the way it works. The bot tells you and comes
back within seconds.
