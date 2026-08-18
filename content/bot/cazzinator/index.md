+++
title = "Cazzinator"
description = "Cancella i media di un gruppo dopo un tempo che decidi tu."
weight = 20

[extra]
emoji = "🍆"
repo = "ToolBoxyBots"
username = "Cazzinator_bot"
clonable = true
+++

## Cosa fa

Metti `#dick` nella didascalia di una foto o di un video e il bot lo cancella
dopo un po'. Il tempo predefinito è due ore, ma puoi indicarne uno tuo, per
esempio `#dick30m`, e un admin può cambiare il valore di tutto il gruppo.

Serve a tenere pulite le chat dove si mandano molti media senza doverli
cancellare a mano. Se vuoi che sparisca tutto senza scrivere niente ogni
volta, con `/alldick 3h` il bot mette in coda ogni media che arriva nel
gruppo.

Nello stesso bot c'è anche `/unsplash`: prende una foto a caso e ci scrive
sopra il testo che gli dai, in stile citazione motivazionale.

## Prima di iniziare

- Si usa in **gruppi e supergruppi**.
- Il bot deve essere **amministratore** con il permesso **Elimina messaggi**.
  Senza quel permesso il bot ignora del tutto i comandi di cancellazione:
  non risponde e non protesta. Vedi
  [Permessi Telegram](@/guida/permessi.md).
- Telegram lascia cancellare i messaggi altrui solo entro **48 ore**, quindi
  i tempi oltre le 24 ore non hanno senso e infatti il bot li taglia a 24 ore.
- Il comando di base è configurabile: qui si chiama `dick`, in un clone può
  chiamarsi come vuoi. In quel caso sostituisci `dick` con la tua parola in
  tutti i comandi qui sotto, compresi `/setdick`, `/alldick` e `/noalldick`.

## Configurazione

1. Aggiungi il bot al gruppo e promuovilo amministratore con il permesso
   **Elimina messaggi**.
2. Manda una foto scrivendo `#dick` nella didascalia. Il bot risponde con il
   momento in cui il media sparirà.
3. Se due ore non sono la durata giusta per il tuo gruppo, un admin dà
   `/setdick 30m` (oppure `1h30m`, fino a un massimo di 24 ore).
4. Per una singola volta puoi scavalcare il predefinito attaccando il tempo al
   comando: `#dick10m` nella didascalia, oppure `/dick10m` in risposta al
   media.
5. Se vuoi la cancellazione automatica di tutto, un admin del gruppo dà
   `/alldick 3h`. Con `/noalldick` la spegne.

## Comandi

I comandi di cancellazione funzionano sia con `/` sia con `#`. `/unsplash`
vuole la barra.

### Per tutti, in gruppo

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `#dick` nella didascalia | Il media viene cancellato dopo il tempo predefinito del gruppo, due ore se nessuno lo ha cambiato. Può stare in qualsiasi punto della didascalia | tutti | Gruppo |
| `#dick1h30m` nella didascalia | Come sopra, ma con il tempo che indichi tu | tutti | Gruppo |
| `/dick` in risposta a un media | Programma la cancellazione di un media già mandato | tutti | Gruppo |
| `/dick1h30m` in risposta a un media | Come sopra, con il tempo che indichi tu | tutti | Gruppo |
| `/unsplash testo` | Manda una foto a caso con sopra il tuo testo, il tuo nome e il tuo username | tutti | Gruppo e privato |
| `/unsplash` in risposta a un messaggio | Come sopra, ma prende il testo e il nome dal messaggio a cui rispondi | tutti | Gruppo e privato |

### Per gli admin del gruppo

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/setdick 1h30m` | Imposta la durata predefinita del gruppo. Il massimo è 24 ore, oltre viene tagliato | admin del gruppo | Gruppo |
| `/alldick 3h` | Attiva la cancellazione automatica di tutti i media del gruppo e ne imposta la durata. Il tempo va sempre indicato | admin del gruppo | Gruppo |
| `/noalldick` | Spegne la cancellazione automatica | admin del gruppo | Gruppo |

Il tempo si scrive attaccato, in ore e minuti: `30m`, `2h`, `1h30m`. Se non
scrivi niente il bot ti risponde con l'esempio giusto.

### Per chi possiede un clone

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/modules` | Apre l'elenco delle funzioni del bot: tocca una voce per accenderla o spegnerla. Vale anche `/moduli` | il proprietario del clone | Privato |

Un clone parte con le funzioni scelte al momento della creazione, ma non sono
definitive: da `/modules` puoi accendere le altre o spegnere quelle che non ti
servono in qualsiasi momento.

Se il bot cambia proprietario, apri @BotFather, chiedi il token del bot con
`/token` e inoltra quel messaggio al bot stesso: da quel momento è tuo e il
proprietario precedente non lo gestisce più. Subito dopo conviene usare
`/revoke` in @BotFather, altrimenti chi lo aveva prima può ancora usare il
vecchio token.

## Bottoni e automatismi

Il bot non ha bottoni.

A ogni media programmato risponde con "Questo messaggio sarà cancellato" e il
momento in cui succederà. Quel messaggio di servizio sparisce insieme al
media, quindi in chat non resta traccia.

Se rilanci il comando sullo stesso media, il timer vecchio viene buttato via e
vale l'ultimo. Vale anche se aggiungi il comando **modificando** la didascalia
dopo aver mandato il media: il bot rilegge la didascalia modificata.

Con gli album il bot tratta tutte le foto insieme: basta il comando su una
sola e spariscono tutte.

Con `/alldick` attivo il bot mette in coda da solo ogni foto, video, GIF,
sticker, videobolla, storia e documento che arriva nel gruppo, senza che
nessuno scriva niente.

## Domande frequenti

### Ho scritto `#dick` e non è successo niente

Quasi sempre manca il permesso **Elimina messaggi**. Il bot non risponde
proprio quando non ce l'ha, perché sa già che non riuscirebbe a cancellare.
Controlla anche che tu stia usando la parola giusta: nei cloni può essere
diversa da `dick`.

### Quanto dura di default?

Due ore per il singolo media, tre ore per la cancellazione automatica di
`/alldick`. Un admin cambia la prima con `/setdick`.

### Posso mettere una settimana?

No. Il massimo è 24 ore, e sopra quella soglia il bot taglia il tempo. Non è
una scelta di comodo: Telegram non lascia cancellare a un bot i messaggi
altrui più vecchi di 48 ore.

### Cancella anche i messaggi di testo?

No. Il comando in risposta programma la cancellazione del messaggio a cui
rispondi qualunque esso sia, ma la cancellazione automatica di `/alldick`
guarda solo i media: foto, video, GIF, sticker, videobolle, storie e
documenti.

### Chi può accendere la cancellazione automatica?

Solo gli amministratori del gruppo, come per `/setdick`. Gli altri membri
possono comunque far cancellare i propri media, mettendo `#dick` nella
didascalia o rispondendo al media con `/dick`.

### `/unsplash` che foto usa?

Una foto a caso presa da Unsplash, diversa ogni volta. Il testo viene scritto
sopra in maiuscolo, con sotto il nome di chi lo ha chiesto o di chi ha
scritto il messaggio a cui rispondi.
