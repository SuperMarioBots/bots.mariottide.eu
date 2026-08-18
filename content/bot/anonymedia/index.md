+++
title = "AnonyMedia"
description = "Manda foto e video nei tuoi gruppi senza che nessuno sappia chi li ha mandati."
weight = 60

[extra]
emoji = "🕵🏻"
repo = "AnonyMediaBots"
username = "AnonyMediaBot"
clonable = true
+++

## Cosa fa

AnonyMedia pubblica foto, video, GIF, documenti e videomessaggi nei gruppi al posto
tuo. Chi guarda il gruppo vede un post del bot, non il tuo nome: il media
resta anonimo per tutti tranne che per lo staff, che sa sempre chi ha mandato
cosa.

Si usa in chat privata con il bot. Gli scrivi, scegli il gruppo dalla lista e
mandi il media. Se sei in whitelist il post esce subito, altrimenti passa prima
dalle mani dello staff, che lo approva o lo scarta con dei pulsanti.

Ogni media pubblicato porta sotto il pulsante
**😏 Invia media in forma anonima 😏**, così chi lo vede nel gruppo può fare
la stessa cosa con un tocco.

## Prima di iniziare

Per usarlo da utente serve poco: essere iscritto a un gruppo dove c'è già il
bot. La lista dei gruppi che ti propone è costruita su questo, quindi se non
scrivi da tanto tempo può capitare che il gruppo non compaia: manda un
messaggio nel gruppo e riprova.

Per attivarlo su un tuo gruppo servono due chat:

- La **chat pubblica**, cioè il gruppo dove usciranno i media. Il bot deve
  starci dentro e poter scrivere. I canali non si possono collegare: Telegram
  non consegna ai bot i comandi scritti lì dentro.
- La **chat staff**, un gruppo separato dove arrivano i media da controllare.
  Serve anche se pensi di approvare tutto: è il posto da cui si comandano
  whitelist e moderazione.

Conviene dare al bot anche il permesso **Elimina messaggi** nella chat
pubblica: senza, `/delete` lascia in giro il comando e la cancellazione
automatica dopo due ore non sempre riesce. I dettagli stanno in
[Permessi Telegram](@/guida/permessi.md).

## Configurazione

1. Crea il gruppo dello staff e aggiungici il bot.
2. Nel gruppo dello staff manda `/register`. Il bot risponde con un comando
   `/confirm` seguito da un codice, valido 15 minuti.
3. Copia quel comando e fallo mandare **nel gruppo pubblico** da una persona
   che ne è amministratore. Il bot controlla che chi scrive sia davvero admin
   lì.
4. Il bot conferma in entrambe le chat: da quel momento le due sono collegate.
5. Se il gruppo dello staff è un forum, manda `/register` dentro il topic dove
   vuoi ricevere i media: le richieste da moderare arriveranno lì.
6. Metti in whitelist le persone di cui ti fidi con `/whitelist`, così i loro
   media escono senza passare dalla moderazione.

Per rifare il collegamento (per esempio dopo aver cambiato gruppo staff) basta
ripetere `/register` e `/confirm`: l'ultima registrazione sostituisce la
precedente.

## Comandi

### Per chi manda i media

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/start` | Mostra i gruppi in cui puoi pubblicare e apre l'invio | tutti | chat privata |
| `/help` | Spiega come si usa | tutti | ovunque |
| `/delete` | In risposta a un media pubblicato, lo cancella. Funziona solo se quel media lo hai mandato tu | chi ha inviato quel media | nel gruppo |
| `/clone` | Spiega come creare la tua copia del bot | tutti | chat privata |
| `/ping` | Risponde `PONG`, serve solo a capire se il bot è vivo | tutti | ovunque |

### Per lo staff

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/register` | Genera il codice da usare con `/confirm` per collegare un gruppo | staff | nel gruppo staff |
| `/confirm CODICE` | Completa il collegamento | admin del gruppo | nel gruppo pubblico |
| `/whitelist @tizio` | Mette una o più persone in whitelist: i loro media escono senza controllo. Accetta anche gli ID numerici | staff | nel gruppo staff |
| `/delwhitelist @tizio` | Toglie dalla whitelist | staff | nel gruppo staff |
| `/inwhitelist @tizio` | Dice se una persona è in whitelist | staff | nel gruppo staff |
| `/whitelists` | Elenca tutte le persone in whitelist | staff | nel gruppo staff |
| `/tagwhitelist` | Nomina le persone in whitelist ancora iscritte al gruppo, cinque per messaggio | staff | nel gruppo staff |
| `/help` | Riepilogo dei comandi staff | staff | nel gruppo staff |

## Bottoni e automatismi

Quando arriva un media da moderare, lo staff lo riceve con cinque pulsanti:

- **✅ Accetta** pubblica il media nel gruppo.
- **❌ Rifiuta** lo scarta e non pubblica niente.
- **🍆 Dick (2h)** pubblica il media e lo cancella da solo dopo due ore. Nel
  gruppo compare l'avviso "Questo messaggio sarà cancellato fra 2 ore", e
  anche la copia rimasta nella chat staff sparisce.
- **🚫 Banna** scarta il media e impedisce a quella persona di mandarne altri
  in quel gruppo tramite il bot. Non tocca la sua iscrizione al gruppo.
- **✅ Whitelist + Accetta** pubblica il media e mette chi lo ha mandato in
  whitelist, così la volta dopo non passa più dal controllo.

Il messaggio nella chat staff, una volta gestito, perde i pulsanti e riporta
chi ha deciso cosa.

Se scrivi `#dick` (o `/dick`) nella didascalia, il media si cancella da solo dopo due ore
anche quando viene approvato normalmente.

Non serve partire per forza da `/start`: puoi mandare il media al bot e
scegliere il gruppo dopo. Nei gruppi forum il bot ti chiede anche in quale
sezione pubblicare. Dopo ogni invio compaiono i pulsanti **📤 Invia un altro**
e **📤 Stesso gruppo**, per ripetere senza rifare la scelta.

Sui media pubblicati il bot applica una filigrana con lo username della chat,
o con il suo nome se non ha uno username. È attiva di default e non c'è un
comando per spegnerla.

## Deep link: mandare la gente dritta al tuo gruppo

Se metti un pulsante o un link con questo indirizzo, chi lo tocca apre il bot
già impostato sul tuo gruppo e salta la scelta dalla lista:

```
https://t.me/AnonyMediaBot?start=CHAT_ID
```

Al posto di `CHAT_ID` va l'ID numerico del gruppo, quello che inizia per
`-100`. È lo stesso link che il bot mette sotto ogni media pubblicato. Il
controllo resta: se chi tocca il link non è iscritto al gruppo o è stato
bannato dal bot, non pubblica niente.

## Domande frequenti

### Lo staff sa chi sono?

Sì. L'anonimato vale verso il gruppo, non verso chi modera: nella chat staff
il tuo media arriva collegato al tuo account, e il bot avvisa che in caso di
abuso si viene bannati. Se sei in whitelist il media non passa dalla chat
staff, ma resta comunque registrato.

### Il bot dice che non sono in nessun gruppo.

Compaiono solo i gruppi dove ci sei tu e c'è anche il bot. Se non scrivi da
molto tempo, manda un messaggio nel gruppo e premi **🔄 Ricarica**.

### Ho mandato un video e non è uscito niente.

Sopra i 20 MB il bot non riesce a lavorare il file e la richiesta viene
scartata. Manda un file più leggero, oppure comprimi il video prima.

### Posso cancellare un media già pubblicato?

Sì, ma solo il tuo: rispondi a quel media nel gruppo con `/delete`. Il bot
controlla che sia partito da te e lo elimina. Sui media di altri il comando
non fa niente.

### "Stai inviando troppi media. Aspetta un minuto e riprova."

C'è un limite di tre invii al minuto a testa. Aspetta sessanta secondi e
riparti.

### Il codice di `/confirm` non funziona più.

Dura quindici minuti. Genera il codice nuovo con `/register` nel gruppo dello
staff, tenendo conto che tra un codice e l'altro il bot fa passare mezzo
minuto.

### Posso usarlo su un canale?

No. Telegram non consegna ai bot i comandi scritti dentro un canale, quindi
`/confirm` da lì non arriva mai e il canale non si può collegare. Sia la chat
pubblica sia la chat staff devono essere gruppi.
