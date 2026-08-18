+++
title = "Create your own clone"
description = "How to get an independent copy of a bot, with your own data and your own groups."
weight = 1
+++

A clone is an identical copy of the bot with its own username and its own
data: its own admins, groups and settings. The code and the server stay mine,
so your clone gets every update, but nobody else touches your data.

Cloning is worth it even when the public bot already works: a bot dedicated to
your group is faster, because it does not share Telegram's rate limits with
thousands of other chats.

## Picking the features before you clone

Cazzinator and Tagga run on the same program and differ only in which
features are on. On either one's page inside
[@VetrinaSuperMarioBot](https://t.me/VetrinaSuperMarioBot) there is a
**Choose features** button: it opens the list already set up like the bot you
are looking at and lets you turn the others on, so you can clone Tagga and
keep `/unsplash` too. Leave it alone and the clone starts with the features
of the bot you picked.

Nothing is final: from the clone you can change them any time with
`/modules`.

## Easy way: one tap

Use this when the button is offered. It needs a recent Telegram version.

1. Open [@VetrinaSuperMarioBot](https://t.me/VetrinaSuperMarioBot).
2. Pick the bot you want to clone.
3. Press **Create clone (easy)**, then **Create the clone**.
4. Telegram asks for the new bot's name and username and does the rest.
   No @BotFather needed.
5. Open your new bot and send it `/start`.

## Manual way: @BotFather

Works on any Telegram version.

1. Open [@BotFather](https://t.me/BotFather).
2. Send `/newbot`.
3. Type the display name for your bot.
4. Type the username. It has to end in `bot`.
5. @BotFather replies with a message containing the **token**.
6. **Forward that message** (a real forward, showing "Forwarded from
   BotFather") to the bot you want to clone, or to
   [@VetrinaSuperMarioBot](https://t.me/VetrinaSuperMarioBot).
7. Open your new bot and send it `/start`.

The token is the bot's password: whoever holds it controls the bot. If you
leak it, go back to @BotFather and use `/revoke`.

## Common errors

**"You forwarded the wrong message."**
The message has to be forwarded straight from @BotFather, not copied and
pasted, and not forwarded with the sender hidden.

**"You must forward the message from @BotFather that starts with..."**
Only three @BotFather messages work: the creation one
(`Done! Congratulations on your new bot.`), the revoke one
(`Token for the bot ... has been revoked.`) and the reply to `/token`
(`Here is the token for bot`).

**The clone does not answer.**
After registration you have to open it and send `/start`. If it still stays
quiet, check you did not revoke the token on @BotFather afterwards.

## Which bots can be cloned

AnonyMedia, Blocklist, Cazzinator, Master Control Program, Networks, Tagga and
Watermark can. CAM Manager and Ubot Manager cannot: they are single instances
you use directly. Better Limitati is cloned on request, write to me.
