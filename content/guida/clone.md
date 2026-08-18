+++
title = "Creare il tuo clone"
description = "Come ottenere una copia indipendente di un bot, con i tuoi dati e i tuoi gruppi."
weight = 1
+++

Un clone è una copia identica del bot, con un suo username e dati suoi:
propri admin, propri gruppi, propria configurazione. Il codice e il server
restano i miei, quindi il clone si aggiorna insieme a tutti gli altri, ma
nessuno che non sia tu ci mette le mani.

Conviene clonare anche quando il bot pubblico funziona già: un bot dedicato
al tuo gruppo è più veloce, perché non divide i limiti di Telegram con
migliaia di altre chat.

## Scegliere le funzioni prima di clonare

Cazzinator e Tagga girano sullo stesso programma e si distinguono solo per le
funzioni accese. Sulla pagina di uno dei due, dentro
[@VetrinaSuperMarioBot](https://t.me/VetrinaSuperMarioBot), trovi il bottone
**Scegli le funzioni**: apre l'elenco già impostato come il bot che stai
guardando e ti lascia accendere le altre, per esempio clonare Tagga tenendoti
anche `/unsplash`. Se non lo tocchi, il clone parte con le funzioni del bot
che hai scelto.

Non è una decisione definitiva: dal clone puoi cambiarle quando vuoi con
`/modules`.

## Metodo facile: un tap

Se lo vedi offerto, questo è il metodo più rapido. Serve una versione
recente di Telegram.

1. Apri [@VetrinaSuperMarioBot](https://t.me/VetrinaSuperMarioBot).
2. Scegli il bot che vuoi clonare.
3. Premi **Crea clone (facile)**, poi **Crea il clone**.
4. Telegram ti chiede nome e username del nuovo bot e fa tutto in automatico.
   Non serve passare da @BotFather.
5. Apri il bot appena creato e mandagli `/start`.

## Metodo manuale: @BotFather

Funziona sempre, su qualsiasi versione di Telegram.

1. Apri [@BotFather](https://t.me/BotFather).
2. Manda `/newbot`.
3. Scrivi il nome che vuoi dare al bot (quello visibile, con spazi e emoji).
4. Scrivi lo username, che deve finire per `bot`.
5. @BotFather risponde con un messaggio che contiene il **token**.
6. **Inoltra quel messaggio** (inoltro vero, con la citazione "Inoltrato da
   BotFather") al bot che vuoi clonare, oppure a
   [@VetrinaSuperMarioBot](https://t.me/VetrinaSuperMarioBot).
7. Apri il tuo nuovo bot e mandagli `/start`.

Il token è la password del bot: chi ce l'ha lo controlla. Se lo mandi per
sbaglio a qualcun altro, torna su @BotFather e usa `/revoke`.

## Errori comuni

**"Hai inoltrato il messaggio sbagliato."**
Il messaggio deve arrivare inoltrato direttamente da @BotFather, non copiato
e incollato e non inoltrato senza citazione. Su Telegram, quando inoltri,
lascia attiva l'opzione che mostra il mittente originale.

**"Devi inoltrare il messaggio da @BotFather che inizia per..."**
Vanno bene solo tre messaggi di @BotFather: quello di creazione
(`Done! Congratulations on your new bot.`), quello di revoca del token
(`Token for the bot ... has been revoked.`) e quello che risponde a
`/token` (`Here is the token for bot`).

**Il clone non risponde.**
Dopo la registrazione va aperto e avviato con `/start`. Se ancora non
risponde, controlla di non avere revocato il token su @BotFather dopo la
registrazione.

## Quali bot si possono clonare

Si clonano AnonyMedia, Blocklist, Cazzinator, Master Control Program,
Networks, Tagga e Watermark. CAM Manager e Ubot Manager no: sono istanze
uniche, si usano direttamente. Better Limitati si clona su richiesta,
scrivimi.
