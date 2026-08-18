+++
title = "CAM Manager"
description = "Dà accesso a tempo a un canale: link di invito con una durata, rimozione automatica alla scadenza."
weight = 80

[extra]
emoji = "🎟"
repo = "CAMManagerBot"
username = "CAM_Manager_Bot"
clonable = false
+++

## Cosa fa

CAM Manager gestisce gli accessi a tempo a un canale. Tu generi un link di
invito con una durata (sette giorni, un mese, quello che vuoi), lo mandi alla
persona, lei entra nel canale e alla scadenza il bot la rimuove da solo. Se
vuoi prorogare, allunghi la scadenza con un tocco.

Ogni link vale per una persona sola e si consuma al primo uso, quindi non
circola. Il conteggio parte quando la persona entra davvero nel canale, non
quando generi il link.

Il bot tiene l'elenco degli iscritti attivi con la data di scadenza di
ognuno, e lo storico di chi è uscito, scaduto o è stato revocato. Funziona su
più canali contemporaneamente: nel menu li scegli uno per uno.

## Prima di iniziare

Il bot si comanda in chat privata. Nel canale deve essere amministratore, e
gli servono due permessi Telegram esatti:

- **Invita utenti tramite link**, per creare i link di invito;
- **Blocca utenti**, per rimuovere chi è scaduto.

Se il bot perde uno dei due, il canale va in pausa da solo e smette di
generare inviti e di rimuovere gli scaduti, finché non glieli ridai. Vedi
[Permessi Telegram](@/guida/permessi.md).

Amministratore del canale devi esserlo anche tu: il bot mostra nel menu solo i
canali dove risulti admin.

## Configurazione

1. Apri il bot in privato e manda `/start`.
2. Nel tuo canale, promuovi il bot amministratore con **Invita utenti tramite
   link** e **Blocca utenti**.
3. Torna sul bot. Se il canale non compare, premi **🔄 Aggiorna i miei
   canali**.
4. Apri **📋 Canali** e scegli il canale (se ne gestisci uno solo, il bot ci
   entra dritto).
5. Entra in **⚙️ Impostazioni** e imposta i **⏱ Preset di durata**, cioè i
   tagli che userai più spesso, scritti in giorni separati da virgola. Di
   default sono `7, 30, 90`. Ogni valore va da 1 a 365.
6. Sempre in impostazioni, scegli l'**🔔 Avviso pre-scadenza**: 24h (il
   valore predefinito), 72h o nessuno.
7. Premi **➕ Link di invito**, scegli una durata e manda il link alla persona.

## Comandi

I comandi sono pochi perché quasi tutto si fa a bottoni.

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/start` | Apre il menu di gestione, o accetta l'invito se ci arrivi da un link | tutti | privato |
| `/menu` | Riapre il menu se l'hai chiuso | admin del canale | privato |
| `/help` | Riepilogo delle voci del menu | tutti | privato |
| `/language` | Cambia lingua tra italiano e inglese | tutti | privato |
| `/cancel` | Annulla la durata che stai scrivendo | tutti | privato |
| `/ping` | Controlla che il bot sia vivo | tutti | privato |

Chi riceve un invito non deve imparare niente: apre il link, preme **Avvia** e
il bot gli manda il link per entrare nel canale.

## Bottoni e automatismi

Il menu principale elenca i canali che gestisci. Dentro un canale trovi cinque
voci.

| Bottone | Cosa fa |
|---|---|
| **➕ Link di invito** | Genera un invito con la durata scelta fra i preset, oppure **✏️ Personalizzato** per scrivere una durata libera come `7d`, `12h`, `30m` |
| **👥 Iscritti** | Elenco degli attivi con la data di scadenza, e la scheda **Cronologia** con chi è uscito, scaduto o revocato |
| **⚙️ Impostazioni** | Preset di durata, avviso pre-scadenza e stato del canale |
| **⏸ Pausa** e **▶️ Riprendi** | Ferma o riattiva inviti e scadenze per quel canale |
| **🔄 Aggiorna admin** | Rilegge da Telegram chi sono gli amministratori del canale |

Nella lista iscritti, su ogni persona hai **➕ Estendi** (di un taglio preset o
di una durata scritta a mano) e **🚫 Revoca**, che chiede conferma e poi
toglie subito la persona dal canale. Dalla cronologia c'è **🔁 Riattiva**, che
rimette dentro qualcuno scegliendo una nuova durata.

Senza che nessuno tocchi niente, il bot fa queste cose:

- fa partire il conteggio quando la persona entra davvero nel canale;
- manda un avviso prima della scadenza, se hai attivato la finestra a 24 o
  72 ore;
- rimuove chi è scaduto entro un minuto dalla scadenza e chiude la sua riga;
- registra chi esce di sua iniziativa;
- mette il canale in pausa se gli togli uno dei due permessi, e ti scrive per
  dirtelo. Quando glieli ridai, riprende e smaltisce le rimozioni arretrate;
- ti manda un riepilogo giornaliero di scadenze, uscite e avvisi mandati.

## Messaggi che riceve l'iscritto

Tutti in privato, nella lingua della persona.

| Quando | Cosa gli arriva |
|---|---|
| Appena entra | "Benvenuto! Il tuo accesso è attivo fino al ..." |
| Prima della scadenza | "Attenzione: il tuo accesso scade il ... Chiedi una proroga all'admin del canale se vuoi restare" |
| Alla scadenza | "Il tuo accesso è scaduto. Grazie per l'iscrizione!" |
| Se lo revochi | "Il tuo accesso è stato revocato dall'admin del canale" |

Se la persona ha bloccato il bot, questi messaggi non le arrivano, ma la
scadenza e la rimozione valgono lo stesso.

## Domande frequenti

### Il canale non compare nel menu

Controlla di aver promosso il bot amministratore nel canale e di essere
amministratore anche tu, poi premi **🔄 Aggiorna i miei canali**. Se hai
appena cambiato gli admin del canale, usa **🔄 Aggiorna admin** dentro il
canale.

### Il bot dice che il canale è in pausa

O l'hai messo tu in pausa con **⏸ Pausa**, o il bot ha perso uno dei due
permessi. Ridaglieli e la pausa si toglie da sola.

### Quanto dura il link che genero?

Il link che mandi alla persona è monouso e scade dopo **24 ore**: se non lo
apre nessuno entro quel tempo, rigenera l'invito.
Il link vero per entrare nel canale, quello che il bot manda dopo lo **Avvia**,
scade dopo un'ora ed è valido per una persona sola. Se scade, rigenera
l'invito.

### Da quando parte il conteggio?

Da quando la persona entra nel canale, non da quando generi il link.

### Posso allungare un accesso già scaduto?

Sì: apri **👥 Iscritti**, vai in **Cronologia**, trova la persona e usa
**🔁 Riattiva** scegliendo una nuova durata. Riceverà un nuovo invito.

### La stessa persona può avere due accessi allo stesso canale?

No. Se ha già un accesso aperto su quel canale, il bot le risponde che è già
iscritta. Per allungarle il tempo usa **➕ Estendi**.

### Come si scrive una durata personalizzata?

Un numero seguito da `d`, `h` o `m`: `7d` sette giorni, `12h` dodici ore,
`30m` trenta minuti. I preset invece si scrivono solo in giorni, separati da
virgola.

### Se tolgo il bot dal canale, cosa succede agli iscritti?

Restano dentro: senza permessi il bot non può rimuovere nessuno. Le scadenze
vengono messe in coda e vengono smaltite quando ripromuovi il bot.
