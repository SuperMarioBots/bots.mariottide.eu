+++
title = "Better Limitati"
description = "Uno sportello anonimo: chi scrive al bot parla con tutto lo staff, senza sapere chi gli risponde."
weight = 50

[extra]
emoji = "⚔️"
repo = "BetterLimitatiBots"
clonable = false
+++

## Cosa fa

Better Limitati mette un bot fra le persone e lo staff. L'utente scrive in
privato al bot, il messaggio arriva nella chat degli operatori (un gruppo, o un
singolo topic di un gruppo forum), un operatore risponde citando il messaggio
arrivato e la risposta torna in privato all'utente. L'utente vede solo il bot:
non sa chi gli ha risposto, non entra in nessun gruppo e non ha modo di risalire
allo staff.

La risposta di un operatore viene rispecchiata anche in tutte le altre chat
operatore, con scritto chi ha risposto a chi. Così, se lo staff è diviso su più
gruppi o su più topic, nessuno risponde due volte alla stessa domanda. Modifiche
e reaction viaggiano nei due sensi: se l'utente corregge un messaggio, la copia
nella chat operatore si aggiorna, e viceversa.

I due usi tipici sono le verifiche dei gruppi (la videobolla o il vocale
dell'utente arriva sul gruppo staff, senza scambio di contatti) e il contatto per
chi è limitato da Telegram e non può scrivere in privato a chi non lo ha in
rubrica: al bot può scrivere lo stesso.

Questo bot non ha il pulsante di clonazione automatica: si ottiene su richiesta.
Se ti serve, scrivimi da [Supporto e contatti](@/guida/supporto.md) e ti preparo
la tua istanza, con i tuoi gruppi e i tuoi operatori.

## Prima di iniziare

Ti serve un posto dove ricevere i messaggi: un gruppo dello staff va benissimo.
Se il gruppo ha i topic, puoi registrare il singolo topic e tenere lo sportello
separato dal resto delle discussioni.

Il bot va aggiunto al gruppo. Non deve per forza essere amministratore, perché
gli operatori rispondono ai suoi messaggi e quelle risposte le vede sempre. Se
vuoi usare `/onlyadmins`, tienilo comunque nel gruppo prima di lanciare il
comando: legge la lista degli amministratori da lì.

Nei gruppi forum conta il topic da cui scrivi: il comando registra la coppia
gruppo più topic. Se sbagli topic, i messaggi arrivano nel posto sbagliato.

## Configurazione

1. Chiedimi il bot da [Supporto e contatti](@/guida/supporto.md). Te lo consegno
   già attivo, con te come primo amministratore.
2. Aggiungi il bot al gruppo dello staff.
3. Scrivi `/addchat` nel gruppo, o dentro il topic che vuoi usare. Da quel
   momento i messaggi degli utenti arrivano lì.
4. Aggiungi gli altri responsabili con `/addadmin` (in risposta a un loro
   messaggio, o con il loro `@username`). Chi diventa amministratore riceve anche
   in privato le copie dei messaggi.
5. Controlla con `/listchats` che siano registrate solo le chat che vuoi.
6. Personalizza il benvenuto con `/setstart` e la conferma che l'utente riceve
   dopo aver scritto con `/setreply`.
7. Se vuoi che risponda solo chi comanda, scrivi `/onlyadmins` nella chat
   operatore.

## Comandi

### Per chi scrive al bot

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/start` | Avvia il bot e mostra il messaggio di benvenuto | tutti | privato |
| `/help` | Mostra il messaggio di benvenuto predefinito, anche se lo hai cambiato con `/setstart` | tutti | privato |
| `/ping` | Risponde `PONG`, serve solo a capire se il bot è vivo | tutti | ovunque |
| `/language` | Scegli la lingua del bot da una lista di bottoni | tutti | privato |

### Per gli admin del bot

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/addchat` | Registra come chat operatore la chat (o il topic) da cui scrivi | admin del bot | gruppo, topic o privato |
| `/delchat` | Toglie quella chat dalle chat operatore | admin del bot | gruppo, topic o privato |
| `/listchats` | Elenca le chat operatore registrate | admin del bot | ovunque |
| `/addadmin @utente` | Aggiunge un amministratore del bot e registra la sua chat privata come chat operatore | admin del bot | ovunque |
| `/deladmin @utente` | Toglie un amministratore e la sua chat privata | admin del bot | ovunque |
| `/listadmins` | Elenca gli amministratori | admin del bot | ovunque |
| `/addban @utente` | Impedisce a una persona di scrivere al bot | admin del bot | ovunque |
| `/delban @utente` | Toglie il divieto | admin del bot | ovunque |
| `/listbans` | Elenca le persone bloccate | admin del bot | ovunque |
| `/onlyadmins` | In quella chat operatore possono rispondere solo gli amministratori del gruppo | admin del bot | nella chat operatore |
| `/noonlyadmins` | Torna a lasciare rispondere chiunque | admin del bot | nella chat operatore |
| `/original` | In risposta a un messaggio ricevuto, riporta l'originale con il suo mittente | admin del bot | nella chat operatore |
| `/setstart Ciao!` | Imposta il messaggio di benvenuto. La formattazione di Telegram non viene salvata: per il grassetto scrivi i tag HTML, per esempio `<b>ciao</b>` | admin del bot | ovunque |
| `/unsetstart` | Torna al benvenuto predefinito | admin del bot | ovunque |
| `/setreply Ti rispondiamo presto` | Imposta la conferma che l'utente riceve dopo aver scritto | admin del bot | ovunque |
| `/unsetreply` | Torna alla conferma predefinita, quella che sparisce da sola | admin del bot | ovunque |
| `/hidestart` | Gli `/start` degli utenti non arrivano nelle chat operatore | admin del bot | ovunque |
| `/unhidestart` | Torna a mostrarli | admin del bot | ovunque |
| `/hidehelp` | Gli `/help` degli utenti non arrivano nelle chat operatore | admin del bot | ovunque |
| `/unhidehelp` | Torna a mostrarli | admin del bot | ovunque |
| `/setbuttons` | Mette una tastiera di bottoni sotto la chat dell'utente | admin del bot | ovunque |
| `/unsetbuttons` | Toglie la tastiera | admin del bot | ovunque |

Gli amministratori del bot, scrivendo `/start` o `/help` in privato, ricevono
questa lista invece del benvenuto.

### La sintassi di /setbuttons

I bottoni si scrivono nello stesso messaggio del comando: ogni riga a capo è una
riga di tastiera, le colonne si separano con `||`. Per esempio:

```
/setbuttons Assistenza||Segnalazione
Come funziona
```

produce due bottoni affiancati (Assistenza e Segnalazione) e sotto un bottone
largo (Come funziona). Toccare un bottone equivale a scrivere quel testo, quindi
il messaggio arriva agli operatori come qualsiasi altro. Con `/unsetbuttons` la
tastiera sparisce.

## Bottoni e automatismi

Il grosso del lavoro avviene senza comandi. Ogni messaggio privato che arriva al
bot viene mandato in copia a tutte le chat operatore, con in testa il nome e
l'ID di chi ha scritto. Foto, vocali, videobolle, documenti e sondaggi arrivano
come sono; i messaggi inoltrati restano inoltri, così si vede da dove vengono.

Per rispondere basta citare il messaggio nella chat operatore e scrivere: la
risposta parte in privato all'utente, agganciata al messaggio giusto. Nella chat
operatore compare una conferma che si cancella da sola dopo qualche secondo, per
non sporcare. Nelle altre chat operatore compare invece la copia della risposta,
con scritto quale operatore ha risposto a quale utente.

Anche le catene di risposta si mantengono: se l'utente cita una risposta dello
staff, gli operatori la vedono citata, e viceversa. Modifiche e reaction si
propagano nei due sensi. Se l'utente ha bloccato il bot, l'operatore lo scopre
subito, perché il bot lo scrive in chat.

## Domande frequenti

### L'utente può scoprire chi sono gli operatori?

No. Vede solo il bot. Nomi e gruppi dello staff restano dalla parte degli
operatori, e la risposta gli arriva dal bot.

### Come si usa nei gruppi con i topic?

Apri il topic dedicato e scrivi `/addchat` da lì. Vengono registrati insieme il
gruppo e il topic, quindi i messaggi arrivano in quel topic e non altrove. Puoi
registrare più topic dello stesso gruppo.

### Posso avere più di un gruppo operatore?

Sì, quante chat vuoi. Ogni messaggio arriva in tutte, e ogni risposta viene
rispecchiata in quelle dove non è stata scritta.

### Chi può rispondere agli utenti?

Di base chiunque sia nella chat operatore. Con `/onlyadmins` in quella chat
rispondono solo gli amministratori del gruppo (e gli amministratori del bot).

### Un utente sta scrivendo cose moleste

`/addban`, in risposta a un suo messaggio o con il suo `@username`. Da quel
momento quello che scrive non arriva più a nessuno. Con `/delban` torna tutto
come prima.

### Perché ricevo i messaggi anche in privato?

Perché `/addadmin` registra anche la chat privata di chi diventa amministratore.
Se non ti serve, scrivi `/delchat` nella tua chat privata con il bot: resti
amministratore, ma smetti di ricevere le copie.

### Come lo ottengo?

Su richiesta, non c'è un pulsante di clonazione automatica. Scrivimi da
[Supporto e contatti](@/guida/supporto.md).
