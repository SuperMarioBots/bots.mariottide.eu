+++
title = "Ubot Manager"
description = "Prende i messaggi da un tuo canale e li rimanda a tutti i gruppi di una cartella Telegram, a orari che decidi tu."
weight = 100

[extra]
username = "Ubot_Manager_Bot"
emoji = "🪄"
repo = "ubot"
clonable = false
+++

## Cosa fa

Ubot Manager pubblica per te. Scegli un canale da cui prendere i messaggi,
scegli una cartella Telegram che contiene i gruppi dove vuoi pubblicare, dici
ogni quanto, e il bot fa il resto. A ogni giro prende un messaggio nuovo dal
canale e lo manda in tutti i gruppi della cartella.

La differenza rispetto agli altri bot è che qui non lavora un bot dentro i
gruppi: lavora il tuo account. Colleghi il tuo account una volta sola con
`/login` e da lì in poi i messaggi partono come se li scrivessi tu. Per questo
funziona anche nei gruppi dove i bot non possono entrare o non possono
scrivere.

Puoi avere più cartelle in parallelo, ognuna con il suo canale sorgente, il
suo intervallo e le sue impostazioni.

## Prima di iniziare

Si usa solo in chat privata con il bot. Non va aggiunto a nessun gruppo e non
va promosso amministratore da nessuna parte: i permessi che servono sono
quelli che hai già tu nei tuoi gruppi.

Serve:

- il tuo account Telegram, collegato al bot con `/login`;
- una cartella Telegram che contiene i gruppi di destinazione;
- un canale (di tipo canale, non gruppo) di cui sei già membro, da usare come
  sorgente dei messaggi.

Dopo il login Telegram ti segnala una nuova sessione chiamata **Windows 10
Desktop**. Quella sessione è il bot. Non terminarla: se la revochi il bot
smette di pubblicare e devi rifare `/login`.

## Configurazione

1. Apri il bot in privato e manda `/start`.
2. Manda `/login` e premi **Apri accesso sicuro**. Si apre una pagina dove
   inserisci il numero di telefono e il codice che Telegram ti manda
   nell'app.
3. Nell'app Telegram crea la cartella con i gruppi di destinazione:
   **Impostazioni**, **Cartelle**, **Crea nuova cartella**, poi aggiungi i
   gruppi.
4. Torna sul bot, manda `/spam` e premi **+ Aggiungi cartella**. Scegli la
   cartella appena creata.
5. Dentro la cartella premi **Canale sorgente** e scegli il canale da cui
   prendere i messaggi, oppure mandane l'@username o il link di invito.
6. Premi **Imposta timer**, scegli ogni quanto pubblicare (per esempio ogni
   2 ore), se andare avanti all'infinito o fermarsi dopo un certo numero di
   invii, ed eventualmente un orario fisso di partenza per allineare i giri
   all'orologio.

Da quel momento il bot va da solo. Se vuoi vedere subito il risultato, premi
**Esegui spam ora**.

## Comandi

Tutti in chat privata con il bot.

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/start` | Messaggio di benvenuto e primi passi | tutti | privato |
| `/login` | Collega il tuo account Telegram al bot | tutti | privato |
| `/logout` | Scollega la sessione e cancella l'accesso | tutti | privato |
| `/spam` | Apre la gestione di cartelle, canali sorgente e timer | tutti | privato |
| `/errors` | Mostra gli errori degli ultimi invii, gruppo per gruppo | tutti | privato |
| `/guide` | Tutorial passo passo dentro il bot | tutti | privato |
| `/language` | Cambia lingua tra italiano e inglese | tutti | privato |
| `/paysupport` | Contatto per problemi con i pagamenti | tutti | privato |
| `/cancel` | Annulla l'operazione in corso | tutti | privato |
| `/help` | Elenco dei comandi | tutti | privato |

## Bottoni e automatismi

Quasi tutto si fa dai bottoni di `/spam`. Dentro la scheda di una cartella
trovi:

| Bottone | Cosa fa |
|---|---|
| **Esegui spam ora** | Pubblica subito, senza aspettare il prossimo giro |
| **Invia messaggio manualmente** | Scegli tu il messaggio da mandare adesso |
| **🔄 Auto-elimina** | Cancella il messaggio precedente prima di mandarne uno nuovo |
| **⏸️ Pausa** e **Riprendi** | Ferma e riavvia il timer senza perdere la programmazione |
| **Elimina ultimo invio** | Toglie l'ultimo blocco di messaggi da tutti i gruppi |
| **📋 Lista chat** | Mostra i gruppi presenti nella cartella |
| **Imposta timer** e **Elimina timer** | Cambiano o tolgono la programmazione |
| **Canale sorgente** | Sceglie il canale da cui prendere i messaggi |

Nel menu principale di `/spam`, fuori dalla scheda della cartella:

| Bottone | Cosa fa |
|---|---|
| **🔄 Controlla cartelle** | Rilegge le cartelle dal tuo account Telegram |
| **📊 Attività recente** | Riepilogo di come sono andati gli ultimi invii |

Il bot fa da solo tre cose: pubblica all'intervallo che hai scelto scegliendo
ogni volta un messaggio nuovo dal canale, aggiorna il messaggio fissato nella
chat con te con il risultato di ogni giro, e ti avvisa se la sessione del tuo
account smette di funzionare.

Il bot è gratuito e nessuno è autorizzato a venderlo. Se qualcuno ti chiede
soldi per averlo, segnalalo su [@SuperMarioUbot](https://t.me/SuperMarioUbot).
Sullo stesso canale trovi le novità e il
[video tutorial](https://t.me/SuperMarioUbot/15).

## Domande frequenti

### Telegram mi segnala una sessione "Windows 10 Desktop", è sicuro?

Sì, è la connessione del bot al tuo account. Non terminarla: se la revochi il
bot smette di funzionare.

### Ho terminato la sessione per sbaglio, cosa faccio?

Manda di nuovo `/login` e ricollega l'account. Cartelle, canali sorgente e
timer restano dove sono.

### Il bot ha smesso di pubblicare

Guarda il messaggio fissato nella chat con il bot: mostra come è andato ogni
giro. Le cause più comuni sono due, il canale sorgente non ha messaggi nuovi
oppure la sessione è stata revocata. Con `/errors` vedi quali gruppi hanno
rifiutato gli ultimi invii e perché.

### Come cambio il canale sorgente?

Manda `/spam`, apri la cartella, premi **Canale sorgente** e scegline un
altro.

### Posso gestire più cartelle insieme?

Sì. Ogni cartella ha canale sorgente, timer e impostazioni indipendenti.
Aggiungine quante ne vuoi.

### Il bot si paga?

No. È gratuito. Dentro `/spam` c'è un bottone **Supporta ❤️** con Telegram
Stars e PayPal, ma è una donazione per coprire i costi del servizio e non
sblocca nulla.

### Cosa succede se faccio /logout?

La sessione viene cancellata dal server e il bot smette di pubblicare. Per
ripartire serve un nuovo `/login`.
