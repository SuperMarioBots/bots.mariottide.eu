+++
title = "Watermark Bot"
description = "Mette la tua firma in diagonale sui media che gli mandi."
weight = 70

[extra]
emoji = "📸"
repo = "WatermarkBots"
username = "overprint_bot"
clonable = true
+++

## Cosa fa

Imposti una firma una volta sola, poi mandi al bot una foto, un video, una GIF,
una videobolla o un documento e il bot te lo rimanda con la firma scritta in
diagonale sopra, dall'angolo in basso a sinistra a quello in alto a destra.

La firma è un testo tuo: un nome, uno username, il nome di un canale. Puoi
scegliere tra otto caratteri corsivi, e sotto ogni media rifirmato trovi
quattro bottoni per rifare il lavoro più chiaro, più scuro, più piccolo o più
grande finché non ti piace.

Il bot non passa dalle API standard dei bot, quindi accetta anche file ben
oltre i 50 MB: i video lunghi vanno bene, ci mette solo più tempo.

## Prima di iniziare

- Si usa **solo in chat privata**: nei gruppi risponde soltanto a `/ping`, quindi non aggiungerlo.
- Non serve nessun permesso e non va promosso da nessuna parte.
- Prima della firma il bot non lavora: se mandi un media senza avere
  configurato niente, ti risponde chiedendoti di impostare la firma.

## Configurazione

1. Apri il bot e mandagli `/start`.
2. Premi **✍ Imposta la firma** e scrivi il testo che vuoi come firma. In
   alternativa fai tutto in un colpo con `/firma Mario`.
3. Se il carattere predefinito non ti convince, premi
   **🔠 Imposta il carattere** e scegline un altro tra gli otto disponibili.
4. Manda un media. Il bot risponde con un messaggio di attesa e poi con il
   media firmato.
5. Usa i bottoni sotto il risultato per aggiustare tonalità e dimensione.

Firma e carattere restano salvati: li imposti una volta e valgono per tutti i
media successivi, finché non li cambi.

## Comandi

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/start` | Messaggio di benvenuto con i due bottoni di configurazione | tutti | Privato |
| `/firma Mario` | Imposta la firma in un colpo solo, senza passare dai bottoni | tutti | Privato |
| `/signature Mario` | Uguale a `/firma` | tutti | Privato |
| `/clone` | Spiega come creare la tua copia del bot: crei il bot su @BotFather e gli inoltri il messaggio con il token | tutti | Privato |
| `/ping` | Risponde `PONG`, serve solo a capire se il bot è vivo | tutti | ovunque |

Se dai `/firma` senza scrivere niente dopo, il bot ti chiede di rilanciarlo
indicando la firma.

## Bottoni e automatismi

**✍ Imposta la firma** apre una domanda: il messaggio successivo che scrivi
diventa la tua firma, testo compreso di spazi ed emoji.

**🔠 Imposta il carattere** mostra gli otto caratteri disponibili. Ne scegli
uno e vale da subito per i media successivi.

Sotto ogni media firmato ci sono quattro bottoni, e ognuno rifà il render
partendo dal media originale:

- **🔅** più chiaro, la firma si vede meno.
- **🔆** più scuro, la firma si vede di più.
- **➖** più piccola.
- **➕** più grande.

Puoi premerli quante volte vuoi, anche in sequenza. Oltre un certo punto il
bot smette di cambiare, perché sotto o sopra certi valori la firma sparirebbe
o coprirebbe tutto.

Ogni render passa da una coda. Il messaggio di attesa ti dice quanti media ci
sono davanti al tuo: un video lungo può richiedere diversi minuti. Foto e
video hanno code separate, quindi una foto non resta bloccata dietro a un
film.

## Domande frequenti

### Ho mandato un video e il bot sembra bloccato

Non lo è: sta lavorando. Il messaggio di attesa lo dice chiaro, "non rimandare
lo stesso media pensando che il bot sia bloccato". Ogni copia che mandi finisce
in fondo alla stessa coda e allunga l'attesa a te e a tutti gli altri. Aspetta
e basta.

### Posso mandare file grossi?

Sì. Il limite dei 50 MB delle API standard qui non c'è. Più il file è grande,
più tempo serve.

### Che cosa accetta?

Foto, video, GIF, videobolle e documenti. Un'immagine mandata come file torna
indietro come file, non come foto.

### La firma esce sempre uguale?

Sulle foto sì: con le stesse impostazioni due passaggi sullo stesso file danno
lo stesso risultato. Sui video l'angolo cambia un po' a ogni render, quindi
due copie dello stesso video non escono mai identiche.

### Posso cambiare firma?

Quando vuoi, con `/firma` o con il bottone. Vale dal media successivo, quelli
già firmati restano come sono.

### I miei media li vede qualcuno?

Sì, in parte, e tanto vale dirlo. Ogni media che arriva al bot pubblico viene
inoltrato in automatico a un canale privato di controllo che leggo io, insieme
al nome di chi lo ha mandato, alla firma e al carattere usati. Serve a capire
cosa passa dal bot e a intervenire sugli abusi. Non succede sui cloni: un clone
tuo non inoltra niente da nessuna parte. Se la cosa non ti va bene, clona il
bot oppure non mandargli niente che non manderesti a me.
