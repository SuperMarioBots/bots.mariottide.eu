+++
title = "Blocklist"
description = "A shared blacklist: ban someone once and they are gone from all your groups."
weight = 30

[extra]
emoji = "🚷"
repo = "BlocklistBots"
clonable = true
+++

## What it does

Blocklist keeps a blacklist of users that applies to every group where the
bot is an admin. When someone on your staff puts a person in the blocklist,
the bot bans them everywhere: in the groups you have now and in the ones you
will add tomorrow. You do not have to repeat the ban group by group.

Every ban can carry proofs (the messages that triggered the report, forwarded
to the bot) and a category, for example spam, scam or fraud. Proofs stay
archived and can be read again at any time with `/prove`.

There is no public Blocklist to use as it is: the bot is used cloned, because
the blacklist, categories, groups and staff are yours and you share them with
nobody.

The bot speaks English and Italian. It follows the language of your Telegram
app (Italian for any language other than these two); you can change it at
any time with `/language`. Messages the bot sends without anyone asking, such
as ban notices in groups and the daily permission warnings, use the language
of the clone's owner.

## Before you start

You need all of this:

- The bot in every group you want to protect, promoted to admin with the
  **Ban users** permission. Without that permission the bot cannot work.
- The **Delete messages** permission if you want the bot, along with the ban,
  to also clean up the messages left by whoever ends up in the blocklist.
- A group for the staff, where reports arrive and bans are run from. It is not
  mandatory, but without it `/report` and `/support` do not work.
- The numeric IDs of the people to ban, or one of their messages to reply to.

Details on how to promote a bot are in
[Telegram permissions](@/guida/permessi.en.md).

## Setup

1. Create your clone following [Create your own clone](@/guida/clone.en.md),
   then open it and send it `/start`.
2. Create the staff group, add the bot and promote it to admin with the
   permission to ban.
3. From the staff group send `/setstaff`. The bot replies
   "Staff group set successfully." From then on the admins of that group are
   the bot admins: whoever you promote there controls the bot, whoever you
   demote loses the commands.
4. If the staff group is a forum, send `/setstaff` inside the topic you want
   to use. Only that topic counts as the staff chat.
5. Add the bot to the groups to protect and promote it to admin with the
   permission to ban.
6. Optional: create categories with `/addcategory` and `/addmandcategory`,
   then in each group choose which ones to enable with `/setcategories`.
7. Optional: add with `/addbakchat` a group where proofs are archived, so they
   stay readable even months later.

## Commands

### For everyone

| Command | What it does | Who | Where |
|---|---|---|---|
| `/info 123456789` | Tells whether that person is in the blocklist, since when and why. Accepts `@username` too | everyone | private chat |
| `/status` | Tells you whether you are in the blocklist and why | everyone | private chat |
| `/report` | In reply to a message, sends it to the staff with the author's details | everyone | in groups |
| `/support` | Calls the staff. In reply to a message it behaves like `/report` | everyone | in groups |
| `/language` | Switches the bot between English and Italian | everyone | private chat |
| `/clone` | Explains how to create your own copy of the bot | everyone | private chat |

### Managing the blocklist

| Command | What it does | Who | Where |
|---|---|---|---|
| `/bl 123456789 reason` | Starts the guided ban of a person: category, proofs, confirmation. Also works in reply to one of their messages | bot admin | staff chat or private chat |
| `/mbl 123456789 987654321` | Like `/bl` but for several people at once | bot admin | staff chat or private chat |
| `/nban 123456789 reason` | Bans right away, without asking for proofs | bot admin | staff chat or private chat |
| `/snban 123456789 reason` | Like `/nban`, but without a notice in the groups | bot admin | staff chat or private chat |
| `/unbl 123456789` | Removes from the blocklist and unbans everywhere | bot admin | staff chat or private chat |
| `/prove 123456789` | Forwards you the archived proofs for that person | bot admin | staff chat or private chat |
| `/escilo -1001234567890 message` | Makes the bot leave that group, with an optional goodbye message | bot admin | staff chat or private chat |

With `/bl` and `/mbl` the bot replies with the **Open private chat** button:
the rest of the procedure (category, proofs, confirmation) happens there, so
the proofs do not end up in front of everyone.

`/nban` accepts several IDs and several reasons together:
`/nban 111 222 333 | spam - scam` gives each one a different reason, and if a
reason is missing the last one written applies.

### Categories

| Command | What it does | Who | Where |
|---|---|---|---|
| `/addcategory spam` | Creates an optional category, which each group enables if it wants | bot admin | staff chat or private chat |
| `/addmandcategory scam` | Creates a mandatory category, always active in every group | bot admin | staff chat or private chat |
| `/delcategory spam` | Deletes a category | bot admin | staff chat or private chat |
| `/listcategories` | Lists the categories, with the mandatory ones in bold | bot admin | staff chat or private chat |
| `/setcategories` | Opens the menu to turn the optional categories on or off in that group | group admin | in the group |

In the `/setcategories` menu ☑️ marks a mandatory category, which you cannot
touch, ✅ an active optional one and ❌ an optional one turned off. Tap
**✔️ Close** when you are done.

### Configuration

| Command | What it does | Who | Where |
|---|---|---|---|
| `/setstaff` | Registers the current group (or topic) as the staff chat | bot admin | in the staff group |
| `/unsetstaff` | Removes the staff chat | bot admin | anywhere |
| `/setsupport assist` | Creates a second name for `/support`, for example `/assist` | bot admin | anywhere |
| `/unsetsupport` | Removes the alternative name | bot admin | anywhere |
| `/setidcmd verify` | Enables `/id`, with which an admin declares themselves an official bot admin, and gives it a second name, for example `/verify` | bot admin | anywhere |
| `/unsetidcmd` | Disables `/id` | bot admin | anywhere |
| `/setbanfooter For help write /support` | Adds a line at the bottom of the ban message, for example where to ask for help | bot admin | anywhere |
| `/unsetbanfooter` | Removes the line from the ban message | bot admin | anywhere |
| `/setidfooter <text>` | Adds a line at the bottom of `/id` replies | bot admin | anywhere |
| `/unsetidfooter` | Removes the line from `/id` replies | bot admin | anywhere |
| `/addadmin 123456789` | Adds a bot admin | bot admin | anywhere |
| `/deladmin 123456789` | Removes a bot admin. Only needed if you have no staff chat | bot admin | anywhere |
| `/listadmins` | Lists the bot admins | bot admin | anywhere |
| `/addbakchat -1001234567890 12345` | Registers a chat where proofs are archived. With no arguments it uses the current chat | bot admin | anywhere |
| `/delbakchat -1001234567890` | Removes an archive chat. With no arguments it removes the current one | bot admin | anywhere |
| `/listbakchats` | Lists the archive chats | bot admin | anywhere |
| `/refresh` | Checks again the groups where the bot was not an admin and updates the situation | bot admin | private chat |

### Lists and statistics

| Command | What it does | Who | Where |
|---|---|---|---|
| `/listabl` | Lists who is in the blocklist, in pages | bot admin | staff chat or private chat |
| `/listaxlsx` | Sends the same list as an Excel file | bot admin | staff chat or private chat |
| `/importabl @oldbot` | Copies into this bot the blocklist of another blocklist bot, even if that bot was deleted. With no arguments it shows which bots you can import from. Bans already present stay as they are | admin of both bots | staff chat or private chat |
| `/contabl` | Counts the people in the blocklist, split by category | bot admin | staff chat or private chat |
| `/listchats` | Lists the groups the bot is in | bot admin | staff chat or private chat |
| `/contachat` | Counts the groups and channels the bot is in | bot admin | staff chat or private chat |
| `/stat 123456789` | Shows how many chats are really operational and how many bans are still to apply. With a person or group ID it narrows the count | bot admin | staff chat or private chat |
| `/staff -1001234567890` | Lists the admins of that group by role | bot admin | staff chat or private chat |
| `/stats` | How many times the bot was cloned and how many chats it is in | bot admin | private chat |
| `/help` | Summary of the commands | bot admin | anywhere |

The `/stat` summary is computed in the background and shows the time of the
last update. The first time the bot replies to try again in a few minutes.

## Buttons and automations

The ban is not instant everywhere. The bot runs it through a queue, group by
group: if you have many chats a few minutes may pass before the person is out
of all of them.

When you add the bot to a new group, it checks the blocklist right away and
bans whoever is already inside. Mandatory categories are enabled by
themselves in that group, optional ones you choose.

During the `/bl` and `/mbl` flow the **❌ Delete all messages** button
appears. If you turn it on, at ban time the bot also deletes the messages that
person left in the groups. Tap **Finish** when you are done sending proofs.

If someone adds, promotes or removes the bot from a group, the staff chat gets
a notice with who did it, where, and which permissions were granted.

Once a day the bot checks it is still an admin everywhere. Where it is not, it
writes in the group: "The bot is not added as admin or it can't ban". If after
three days nothing changes, it leaves by itself.

## Frequently asked questions

### I banned a person but they are still in a group.

Wait a few minutes: bans are applied through a queue. If nothing changes after
that, the bot lacks the ban permission in that group. Check with `/stat`,
which tells you how many chats are operational and how many bans are still
missing.

### The bot did not delete the old messages.

Telegram gives bots 48 hours to delete other people's messages. After that
nobody can remove them anymore, not even you.

### Who are the bot admins?

If you set a staff chat with `/setstaff`, they are the admins of that chat:
you manage them from Telegram, by promoting or demoting people there. Without
a staff chat you add them by hand with `/addadmin`, and in that case
`/addadmin` and `/deladmin` are the only ways.

### Someone tells me they cannot get in, how do I check?

Have them send `/status` to the bot in private: it will tell them whether they
are in the blocklist, since when and why. On your side you can use `/info`
with their ID or username. Both commands are open to anyone, no permissions
needed.

### The bot tells me it lacks permissions.

It means that in that group it is not an admin, or it is but without the
permission to ban users. The message also tells you how many days are left
before the bot leaves: after three warnings it leaves the group.

### What are mandatory categories for?

They are for things that are not up for debate, for example fraud: they apply
in every group and no group admin can turn them off. Optional categories
instead are turned on by whoever wants them, group by group, with
`/setcategories`.

### Where do the proofs go?

They stay in the bot's archive and you read them again with `/prove`. If you
register an archive chat with `/addbakchat`, the bot copies the messages used
as proof into it, so they stay safe even if the original chats disappear.
