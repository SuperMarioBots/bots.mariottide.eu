+++
title = "Networks Bot"
description = "Gestisce liste di scambio e liste spam: prenotazioni dei gruppi, pubblicazione della lista e post programmati."
weight = 90

[extra]
emoji = "🌐"
repo = "NetworksBots"
clonable = true
+++

## Cosa fa

Questo bot serve a chi gestisce una lista: liste spam, liste di reciproci,
network di gruppi e canali che si scambiano visibilità. Se non gestisci una
lista e non stai cercando di entrare in quella di qualcun altro, quasi
sicuramente non ti serve.

Il meccanismo è sempre lo stesso. Chi gestisce la lista apre le prenotazioni
in una chat apposita, i gestori dei gruppi e dei canali scrivono lì il
comando di prenotazione e scelgono quali chat vogliono mettere in lista, poi
il gestore chiude le prenotazioni e il bot pubblica la lista completa in
tutte le chat prenotate, con il testo e i bottoni che ha configurato. Da lì
in poi il bot può ripetere il post a intervalli, fissarlo, cancellarlo e
riaprire il giro dopo.

Il bot ha anche una seconda personalità, la modalità inoltro, che non ha
niente a che vedere con le liste: prende i messaggi da una chat sorgente e li
ripete in tutte le chat di destinazione. Si accende dalle impostazioni ed è
descritta più in basso.

Non esiste un bot pubblico da aggiungere e via: ogni lista vive nel suo clone,
con i suoi gestori, le sue chat e le sue impostazioni. Il primo passo, se la
lista la gestisci tu, è crearne uno.

## Prima di iniziare

Ci sono tre ruoli e conviene tenerli distinti.

- **Utente**: chiunque. Aggiunge il proprio gruppo o canale, si prenota,
  scrive allo staff.
- **Manager**: gestisce il giro di tutti i giorni, cioè chat, prenotazioni,
  post programmati e ban.
- **Superuser**: manager che può anche creare altri manager e spostare le
  chat di servizio del bot.

Il bot lavora in tre posti diversi: la chat privata con te, la chat staff (se
il gestore ne ha impostata una) e la chat prenotazioni, dove si scrivono i
comandi di prenotazione.

Nel tuo gruppo o canale il bot va promosso amministratore. I permessi che gli
servono:

- **Elimina messaggi**, per togliere il post vecchio prima di rimettere
  quello nuovo;
- **Fissa messaggi**, per fissare la lista quando è previsto;
- **Invita utenti tramite link**, per generare il link della tua chat da
  mettere in lista.

Quando lo promuovi o gli cambi i permessi, il bot manda ai gestori un
riepilogo e ti dice se "I permessi sono sufficenti per il corretto
funzionamento del bot" oppure quali mancano. Vedi anche
[Permessi Telegram](@/guida/permessi.md).

## Configurazione

### Se vuoi entrare in una lista di qualcun altro

1. Aggiungi il bot della lista al tuo gruppo o canale e promuovilo
   amministratore con i permessi qui sopra.
2. Aspetta. I gestori della lista ricevono una notifica e devono premere
   **Metti in lista**: finché non lo fanno, la tua chat non è prenotabile.
3. Quando le prenotazioni sono aperte, vai nella chat prenotazioni della
   lista e scrivi il comando di prenotazione, di solito `#prenota`.
4. Il bot ti apre l'elenco delle chat dove sei amministratore. Tocca quelle
   che vuoi mettere in lista e premi **✅ Conferma ✅**.
5. Se cambi idea prima della chiusura, `#sprenota` toglie una chat dal giro.

Se la lista prevede l'approvazione, accanto alla chat compare che è prenotata
"con approvazione": vuol dire che chi entra dal link deve essere accettato a
mano.

### Se gestisci una lista tua

1. Chiedi il tuo clone, che nasce già con te come superuser. Vedi
   [Creare il tuo clone](@/guida/clone.md).
2. Crea la chat prenotazioni (un gruppo dove la gente scriverà `#prenota`),
   metti dentro il bot e lancia `/setreschat` proprio lì.
3. Se vuoi una chat staff, dove ricevere i messaggi di chi scrive al bot in
   privato, crea anche quella e lancia `/setstaff` dentro. È lì che poi
   funzionano i comandi di ban.
4. Aggiungi i tuoi manager con `/addmanager`, e gli eventuali altri superuser
   con `/addsuperuser`.
5. Manda `/start` in privato al bot e apri **⚙️ Impostazioni**. Qui prepari il
   messaggio template della lista, i bottoni fissi in alto e in fondo, le
   sottoliste, il formato della lista e, se vuoi, il tag di prenotazione
   diverso da `prenota`.
6. Man mano che la gente aggiunge il bot alle proprie chat, i manager
   ricevono la notifica e premono **Metti in lista** per autorizzarle.
7. Quando è ora, scrivi `/aperte` nella chat prenotazioni. Alla fine del giro
   `/chiuse`.
8. Per pubblicare, dal menu usa **📨 Programma Post**: inoltri il messaggio da
   pubblicare e il bot ti guida a scegliere quando, ogni quanto, dove, se
   fissarlo e se aprire o chiudere le prenotazioni insieme al post.

Le liste possono essere più di una: dal menu principale con **➕ Aggiungi
lista** ne crei un'altra, ognuna con la sua chat prenotazioni, il suo tag e
le sue impostazioni.

## Comandi

Il comando di prenotazione non è fisso. `prenota` è solo il valore di
partenza: ogni lista può usare il suo, deciso dal gestore in **⚙️
Impostazioni**, **#️⃣ Configura tag #prenota**. Se una lista usa `normale`,
allora i comandi diventano `#normale`, `#sprenotanormale`, `/apertenormale`,
`/chiusenormale`. Qui sotto sono scritti con il valore di partenza.

### Per tutti

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/start` | Presentazione del bot. Se c'è una chat staff, da qui scrivi ai gestori | tutti | privato |
| `#prenota` | Apre l'elenco delle tue chat e ti fa prenotare quelle che vuoi | tutti | chat prenotazioni |
| `#sprenota` | Toglie una tua chat dalla lista in corso | tutti | chat prenotazioni |
| `/clone` | Chiede una copia indipendente del bot | tutti | privato |
| `/language` | Cambia lingua | tutti | ovunque |
| `/paysupport` | Contatto per problemi con i pagamenti | tutti | ovunque |
| `/ping` | Controlla che il bot sia vivo | tutti | ovunque |

Sia `#prenota` sia `/prenota` funzionano, ma solo dentro la chat prenotazioni
di quella lista.

### Per i manager

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/aperte [iscritti] [gruppi\|canali]` | Apre le prenotazioni. Il numero è il minimo di iscritti richiesto, la parola limita il giro ai soli gruppi o ai soli canali | manager | chat prenotazioni |
| `/chiuse` | Chiude le prenotazioni | manager | chat prenotazioni |
| `/addchat` | Aggiunge una chat al bot inoltrando un suo messaggio | manager | privato, chat staff |
| `/delchat` | Toglie una chat dal bot | manager | privato, chat staff |
| `/add <chat_id> [nome]` | Mette in lista una chat già registrata, a mano | manager | privato, chat staff |
| `/del <chat_id>` | Toglie dalla lista una chat, a mano | manager | privato, chat staff |
| `/adddefault [chat_id]` | La chat entra in lista di default a ogni giro | manager | ovunque |
| `/deldefault [chat_id]` | Toglie il default alla chat | manager | ovunque |
| `/addcontroller [chat_id]` | La chat riceve i post ma non compare nella lista pubblicata | manager | ovunque |
| `/delcontroller [chat_id]` | La chat torna a comparire in lista come le altre | manager | ovunque |
| `/setrequest [chat_id]` | La chat entrerà in lista con il link a richiesta di ingresso | manager | ovunque |
| `/unsetrequest [chat_id]` | Torna al link diretto per quella chat | manager | ovunque |
| `/newlink <chat_id> <link>` | Impone un link fisso per una chat, invece di quello generato | manager | privato, chat staff |
| `/dellink <chat_id>` | Torna al link generato dal bot | manager | privato, chat staff |
| `/check [chat_id]` | Verifica i permessi del bot nelle chat | manager | privato, chat staff |
| `/escilo <chat_id>` | Fa uscire il bot dalle chat indicate | manager | ovunque |
| `/generate` | Rigenera il testo della lista dal template | manager | privato, chat staff |
| `/staff` | Elenca gli amministratori della chat, divisi per ruolo | manager | gruppo |
| `/admins` | Mostra gli amministratori che il bot ha in memoria | manager | privato, chat staff |
| `/reload_admins` | Rilegge da Telegram gli admin di tutte le chat | manager | privato, chat staff |
| `/counts` | Conta gli iscritti di ogni chat | manager | privato, chat staff |
| `/addban` | Blocca un utente, anche rispondendo al suo messaggio in chat staff | manager | privato, chat staff |
| `/delban` | Sblocca un utente | manager | privato, chat staff |
| `/listbans` | Elenca gli utenti bloccati | manager | privato, chat staff |
| `/check_staff_banned` | Controlla se qualcuno dei bloccati è ancora in giro | manager | privato, chat staff |

I comandi di ban esistono solo se il gestore ha impostato una chat staff.
`/reload_admins` e `/counts` sono lenti: il bot ti avvisa che ci vogliono
minuti.

### Per i superuser

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/addmanager <utente>` | Aggiunge un manager | superuser | ovunque |
| `/delmanager <utente>` | Toglie un manager | superuser | ovunque |
| `/listmanagers` | Elenca i manager | superuser | ovunque |
| `/addsuperuser <utente>` | Promuove qualcuno a superuser | superuser | ovunque |
| `/delsuperuser <utente>` | Torna a manager semplice | superuser | ovunque |
| `/listsuperusers` | Elenca i superuser | superuser | ovunque |
| `/setreschat` | Rende chat prenotazioni la chat da cui lo scrivi | superuser | nella chat scelta |
| `/unsetreschat` | Toglie la chat prenotazioni della lista corrente | superuser | ovunque |
| `/setstaff` | Rende chat staff la chat da cui lo scrivi | superuser | nella chat scelta |
| `/unsetstaff` | Toglie la chat staff | superuser | ovunque |

Dopo `/setstaff` e `/setreschat` il bot si riavvia da solo per applicare la
modifica: qualche secondo e torna a rispondere.

## Bottoni e automatismi

Il menu di `/start` per i manager ha queste voci:

| Bottone | Cosa fa |
|---|---|
| **📨 Programma Post** | Inoltri un messaggio e il bot ti guida su quando, ogni quanto, in quali chat, se fissarlo, se aprire o chiudere le prenotazioni insieme |
| **🗒 Elenca Post Programmati** | Elenco dei post in coda, con modifica del testo, dei link per singola chat e cancellazione |
| **⚙️ Impostazioni** | Template, bottoni, sottoliste, formato lista, tag di prenotazione |
| **➕ Aggiungi Canale** e **➖ Rimuovi Canale** | Aggiungono o tolgono una chat inoltrando un suo messaggio |
| **🗒 Elenca chat** | Le chat registrate sul bot |
| **➕ Aggiungi lista** e **➖ Rimuovi lista** | Gestiscono più liste in parallelo sullo stesso bot |
| **🌐 Lingua** | Cambia lingua |
| **📔 Guida** | Apre la guida del bot |
| **Supporta ❤️** | Donazione con Telegram Stars o PayPal |
| **❌ Chiudi** | Chiude il menu |

Dentro le impostazioni: **💌 Configura messaggio template** è il testo della
lista, **⬆️ Configura bottoni fissi in alto** e **⬇️ Configura bottoni fissi
in fondo** aggiungono bottoni sopra e sotto, **🔗 Configura link "dummy"** è
il link usato dai separatori, **📑 Configura sottoliste** divide la lista in
sezioni, **📋 Configura formato lista** decide colonne e comportamento nei
gruppi con i topic, **#️⃣ Configura tag #prenota** cambia il comando di
prenotazione. Se il bot gestisce una lista sola e non ha bot slave, compare
anche **🤖 Configura bot master**.

Senza che nessuno scriva niente, il bot:

- avvisa i manager quando qualcuno lo aggiunge o lo toglie da una chat, con i
  bottoni **Metti in lista**, **Controlla**, **Amministratori** e **Rimuovi
  il bot**;
- controlla i permessi a ogni cambio di ruolo e scrive cosa manca;
- pubblica i post programmati alle ore stabilite, li fissa se glielo hai
  chiesto e cancella il post precedente;
- apre e chiude le prenotazioni insieme al post, se hai impostato così la
  programmazione;
- inoltra allo staff i messaggi che gli utenti scrivono in privato, e riporta
  all'utente le risposte dello staff;
- mette in pausa per una settimana le chat che continuano a rifiutare i post,
  invece di riprovare all'infinito;
- limita chi ripete `#prenota` troppo in fretta, con un "Troppo veloce!
  Attendi ... e riprova".

## Modalità inoltro

Con **📡 Passa a modalità inoltro** il bot cambia mestiere. Sparisce tutta la
parte di liste e prenotazioni e resta un inoltratore: definisci una o più
chat sorgente e una o più chat destinazione, e ogni messaggio che compare
nella sorgente viene ripetuto nelle destinazioni. Con **📋 Passa a modalità
scheduler** torni indietro.

Il menu di questa modalità è tutto a interruttori, che si accendono e
spengono toccandoli:

| Interruttore | Cosa cambia |
|---|---|
| **Inoltrare i nuovi messaggi** | Interruttore generale dell'inoltro |
| **Copiare i messaggi** oppure **Inoltrare i messaggi** | Con la copia non si vede da dove arriva il messaggio, con l'inoltro sì |
| **Inoltrare i messaggi con bottoni** | Passa o scarta i messaggi che hanno bottoni |
| **Inoltrare i messaggi con link** | Passa o scarta i messaggi che contengono link |
| **Avvisare i manager quando il bot cambia chat** | Notifica ai manager ogni aggiunta, rimozione o cambio di ruolo |
| **Modalità approvazione** | Una nuova destinazione riceve solo dopo che un manager l'ha approvata |
| **Inoltrare l'ultimo messaggio quando il bot viene aggiunto** | Appena entra in una chat nuova, ci rimanda l'ultimo post |
| **Permettere agli utenti di rispondere ai post inoltrati** | Chi risponde a un post in destinazione viene messo in contatto con chi l'ha scritto |
| **Ultimo post** oppure **Post casuale** | Cosa ripubblica il timer di ripetizione |

Le altre voci sono **➕ Aggiungi Canale**, **➖ Rimuovi Canale**, **🗒 Elenca
chat**, **⏰ Ripetizione** (ogni quanti secondi ripetere, zero per spegnere) e
**⟳ Aggiorna lista messaggi**.

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/addchat [chat_id [topic_id]]` | Segna una chat come sorgente | manager | ovunque |
| `/delchat [chat_id [topic_id]]` | Toglie la chat sorgente | manager | ovunque |
| `/listchats` | Elenca sorgenti e destinazioni | manager | ovunque |
| `/approve [chat_id [topic_id]]` | Approva una destinazione in attesa | manager | ovunque |
| `/setexpiration <giorni> [chat_id [topic_id]]` | Dà una scadenza alla sorgente. Un numero negativo la anticipa | manager | ovunque, anche nella sorgente |
| `/unsetexpiration [chat_id [topic_id]]` | Toglie la scadenza | manager | ovunque, anche nella sorgente |
| `/enabletopic <chat_id> <topic_id>` | Attiva un topic come destinazione | manager | ovunque |
| `/disabletopic <chat_id> <topic_id>` | Disattiva quel topic | manager | ovunque |
| `/enablesourcetopic <chat_id> <topic_id>` | Attiva un topic come sorgente | manager | ovunque |
| `/disablesourcetopic <chat_id> <topic_id>` | Disattiva quel topic sorgente | manager | ovunque |
| `/forward` | In risposta a un messaggio nella sorgente, lo manda subito in tutte le destinazioni | manager | chat sorgente |

## Domande frequenti

### Ho scritto #prenota e il bot non risponde

Il comando funziona solo dentro la chat prenotazioni di quella lista, e solo
quando le prenotazioni sono aperte. Se sono chiuse il bot risponde
"Impossibile effettuare la prenotazione dato che le prenotazioni per questa
lista non sono attualmente aperte".

### Il bot dice che non sono admin di nessuna chat prenotata

Vuol dire che nessuna delle chat dove sei amministratore è stata autorizzata
dai gestori della lista, oppure che non rispetta i requisiti del giro in
corso: minimo di iscritti, solo gruppi o solo canali. Aggiungi il bot alla
tua chat e aspetta che un manager prema **Metti in lista**.

### Non trovo #prenota, la lista usa un'altra parola

Ogni lista può cambiare il tag. Guarda il messaggio di apertura delle
prenotazioni: il comando giusto è scritto lì.

### Ho tolto una chat per sbaglio, posso rimetterla?

Sì, finché le prenotazioni sono aperte. Riscrivi il comando di prenotazione e
riseleziona la chat.

### Il post non arriva nel mio gruppo

Nell'ordine: il bot è ancora amministratore, ha ancora **Elimina messaggi** e
**Fissa messaggi**, e la tua chat è davvero in lista in questo giro. Un
manager può lanciare `/check` per vedere i permessi chat per chat. Se la tua
chat ha rifiutato i post per giorni, il bot la mette in pausa per una
settimana.

### Cosa vuol quel "con approvazione" accanto alla mia chat?

Che la tua chat entra in lista con il link a richiesta di ingresso: chi arriva
dal link non entra da solo, deve essere accettato. Lo decide un manager della lista
con `/setrequest`.

### A cosa serve la chat staff?

È dove finiscono i messaggi che gli utenti scrivono al bot in privato. I
manager rispondono citando il messaggio e la risposta torna all'utente. È
anche l'unico posto dove funzionano i comandi di ban.

### Devo per forza creare un clone?

Se gestisci una lista tua sì: chat, manager e impostazioni stanno dentro il
clone, e non c'è un bot pubblico che possa ospitare la lista di qualcun altro.
Se invece vuoi solo entrare nella lista di un altro, il clone lo ha già lui:
a te basta aggiungere al gruppo il bot che ti indica.

### Perché il bot si è riavviato dopo /setstaff?

Perché quelle impostazioni cambiano il modo in cui lavora. Il bot te lo dice e
torna disponibile in pochi secondi.
