+++
title = "Blocklist"
description = "Una lista nera condivisa: banni una persona una volta sola e sparisce da tutti i tuoi gruppi."
weight = 30

[extra]
emoji = "🚷"
repo = "BlocklistBots"
clonable = true
+++

## Cosa fa

Blocklist tiene una lista nera di utenti valida per tutti i gruppi in cui il
bot è amministratore. Quando uno del tuo staff mette una persona in blocklist,
il bot la banna ovunque: nei gruppi che hai adesso e in quelli che aggiungerai
domani. Non devi ripetere il ban gruppo per gruppo.

Ogni ban può portarsi dietro delle prove (i messaggi che hanno causato la
segnalazione, inoltrati al bot) e una categoria, per esempio spam, scam o
truffa. Le prove restano archiviate e si possono rileggere in qualsiasi
momento con `/prove`.

Non esiste un Blocklist pubblico da usare così com'è: il bot si usa clonato,
perché la lista nera, le categorie, i gruppi e lo staff sono tuoi e non li
condividi con nessuno.

## Prima di iniziare

Serve tutto questo:

- Il bot dentro ogni gruppo che vuoi proteggere, promosso amministratore con
  il permesso **Blocca utenti**. Senza quel permesso il bot non può lavorare.
- Il permesso **Elimina messaggi** se vuoi che, insieme al ban, il bot
  ripulisca anche i messaggi lasciati da chi finisce in blocklist.
- Un gruppo per lo staff, dove arrivano le segnalazioni e da cui si comandano
  i ban. Non è obbligatorio, ma senza di esso `/report` e `/support` non
  funzionano.
- Gli ID numerici delle persone da bannare, oppure un loro messaggio a cui
  rispondere.

I dettagli su come si promuove un bot stanno in
[Permessi Telegram](@/guida/permessi.md).

## Configurazione

1. Crea il tuo clone seguendo [Creare il tuo clone](@/guida/clone.md), poi
   aprilo e mandagli `/start`.
2. Crea il gruppo dello staff, aggiungi il bot e promuovilo amministratore con
   il permesso di bannare.
3. Dal gruppo dello staff manda `/setstaff`. Il bot risponde
   "Staff group set successfully". Da quel momento gli amministratori di quel
   gruppo sono gli admin del bot: chi promuovi lì comanda il bot, chi togli
   perde i comandi.
4. Se il gruppo dello staff è un forum, manda `/setstaff` dentro il topic che
   vuoi usare. Solo quel topic vale come chat staff.
5. Aggiungi il bot ai gruppi da proteggere e promuovilo amministratore con il
   permesso di bannare.
6. Facoltativo: crea le categorie con `/addcategory` e `/addmandcategory`, poi
   in ogni gruppo scegli quali attivare con `/setcategories`.
7. Facoltativo: aggiungi con `/addbakchat` un gruppo dove archiviare le prove,
   così restano leggibili anche a distanza di mesi.

## Comandi

### Per tutti

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/info 123456789` | Dice se quella persona è in blocklist, da quando e per quale motivo. Accetta anche `@username` | tutti | chat privata |
| `/status` | Dice a te se sei in blocklist e perché | tutti | chat privata |
| `/report` | In risposta a un messaggio, lo manda allo staff con i dati di chi lo ha scritto | tutti | nei gruppi |
| `/support` | Chiama lo staff. In risposta a un messaggio si comporta come `/report` | tutti | nei gruppi |
| `/clone` | Spiega come creare la tua copia del bot | tutti | chat privata |

### Gestione della blocklist

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/bl 123456789 motivo` | Avvia il ban guidato di una persona: categoria, prove, conferma. Funziona anche in risposta a un suo messaggio | admin del bot | chat staff o chat privata |
| `/mbl 123456789 987654321` | Come `/bl` ma per più persone in una volta sola | admin del bot | chat staff o chat privata |
| `/nban 123456789 motivo` | Banna subito, senza chiedere prove | admin del bot | chat staff o chat privata |
| `/snban 123456789 motivo` | Come `/nban`, ma senza avvisare nei gruppi | admin del bot | chat staff o chat privata |
| `/unbl 123456789` | Toglie dalla blocklist e sbanna ovunque | admin del bot | chat staff o chat privata |
| `/prove 123456789` | Ti inoltra le prove archiviate per quella persona | admin del bot | chat staff o chat privata |
| `/escilo -1001234567890 messaggio` | Fa uscire il bot da quel gruppo, con un messaggio di addio facoltativo | admin del bot | chat staff o chat privata |

Con `/bl` e `/mbl` il bot risponde con il pulsante **Apri chat privata**: il
resto della procedura (categoria, prove, conferma) si svolge lì, così le prove
non finiscono davanti a tutti.

`/nban` accetta più ID e più motivi insieme:
`/nban 111 222 333 | spam - scam` assegna un motivo diverso a ognuno, e se un
motivo manca vale l'ultimo scritto.

### Categorie

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/addcategory spam` | Crea una categoria opzionale, che ogni gruppo attiva se vuole | admin del bot | chat staff o chat privata |
| `/addmandcategory scam` | Crea una categoria obbligatoria, sempre attiva in tutti i gruppi | admin del bot | chat staff o chat privata |
| `/delcategory spam` | Cancella una categoria | admin del bot | chat staff o chat privata |
| `/listcategories` | Elenca le categorie, con le obbligatorie in grassetto | admin del bot | chat staff o chat privata |
| `/setcategories` | Apre il menu per attivare o disattivare le categorie opzionali in quel gruppo | admin del gruppo | nel gruppo |

Nel menu di `/setcategories` il segno ☑️ indica una categoria obbligatoria,
che non puoi toccare, ✅ una opzionale attiva e ❌ una opzionale spenta. Premi
**✔️ Chiudi** quando hai finito.

### Configurazione

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/setstaff` | Registra il gruppo (o il topic) corrente come chat staff | admin del bot | nel gruppo staff |
| `/unsetstaff` | Toglie la chat staff | admin del bot | ovunque |
| `/setsupport aiuto` | Crea un secondo nome per `/support`, per esempio `/aiuto` | admin del bot | ovunque |
| `/unsetsupport` | Toglie il nome alternativo | admin del bot | ovunque |
| `/addadmin 123456789` | Aggiunge un admin del bot | admin del bot | ovunque |
| `/deladmin 123456789` | Toglie un admin del bot. Serve solo se non hai una chat staff | admin del bot | ovunque |
| `/listadmins` | Elenca gli admin del bot | admin del bot | ovunque |
| `/addbakchat -1001234567890 12345` | Registra una chat dove archiviare le prove. Senza argomenti usa la chat corrente | admin del bot | ovunque |
| `/delbakchat -1001234567890` | Toglie una chat di archivio. Senza argomenti toglie quella corrente | admin del bot | ovunque |
| `/listbakchats` | Elenca le chat di archivio | admin del bot | ovunque |
| `/refresh` | Ricontrolla i gruppi dove il bot non risultava amministratore e aggiorna la situazione | admin del bot | chat privata |

### Liste e statistiche

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/listabl` | Elenca chi è in blocklist, a pagine | admin del bot | chat staff o chat privata |
| `/listaxlsx` | Manda la stessa lista come file Excel | admin del bot | chat staff o chat privata |
| `/contabl` | Conta le persone in blocklist, divise per categoria | admin del bot | chat staff o chat privata |
| `/listchats` | Elenca i gruppi dove sta il bot | admin del bot | chat staff o chat privata |
| `/contachat` | Conta gruppi e canali dove sta il bot | admin del bot | chat staff o chat privata |
| `/stat 123456789` | Mostra quante chat sono davvero operative e quanti ban risultano ancora da applicare. Con un ID di persona o di gruppo restringe il conto | admin del bot | chat staff o chat privata |
| `/staff -1001234567890` | Elenca gli amministratori di quel gruppo divisi per ruolo | admin del bot | chat staff o chat privata |
| `/stats` | Quante volte il bot è stato clonato e in quante chat sta | admin del bot | chat privata |
| `/help` | Riepilogo dei comandi | admin del bot | ovunque |

Il riepilogo di `/stat` viene calcolato in sottofondo e riporta l'ora
dell'ultimo aggiornamento. La prima volta il bot risponde di riprovare tra
qualche minuto.

## Bottoni e automatismi

Il ban non è istantaneo ovunque. Il bot lo esegue in coda, gruppo per gruppo:
se hai molte chat possono passare alcuni minuti prima che la persona sia fuori
da tutte.

Quando aggiungi il bot a un gruppo nuovo, lui controlla subito la blocklist e
banna chi è già dentro. Le categorie obbligatorie vengono attivate da sole in
quel gruppo, le opzionali le scegli tu.

Durante il flusso di `/bl` e `/mbl` compare il pulsante
**❌ Cancella tutti i messaggi**. Se lo attivi, al momento del ban il bot
elimina anche i messaggi che quella persona ha lasciato nei gruppi. Premi
**Termina** quando hai finito di mandare le prove.

Se qualcuno ti aggiunge, ti promuove o ti toglie il bot da un gruppo, la chat
staff riceve un avviso con chi lo ha fatto, dove, e quali permessi ha
concesso.

Una volta al giorno il bot controlla di essere ancora amministratore ovunque.
Dove non lo è, scrive nel gruppo: "Il bot non è impostato come admin o non ha
il permesso di bannare". Se dopo tre giorni la situazione non cambia, esce da
solo.

## Domande frequenti

### Ho bannato una persona ma è ancora in un gruppo.

Aspetta qualche minuto: i ban vengono applicati in coda. Se dopo non cambia
niente, in quel gruppo manca al bot il permesso di bannare. Controlla con
`/stat`, che ti dice quante chat sono operative e quanti ban risultano ancora
mancanti.

### Il bot non ha cancellato i vecchi messaggi.

Telegram lascia ai bot 48 ore per cancellare i messaggi altrui. Passato quel
tempo nessuno può più toglierli, nemmeno tu.

### Chi sono gli admin del bot?

Se hai impostato una chat staff con `/setstaff`, sono gli amministratori di
quella chat: li gestisci da Telegram, promuovendo o togliendo persone lì.
Senza chat staff li aggiungi a mano con `/addadmin`, e in quel caso
`/addadmin` e `/deladmin` sono gli unici modi.

### Una persona mi dice che non riesce a entrare, come faccio a controllare?

Falle mandare `/status` al bot in privato: le dirà se è in blocklist, da
quanto e perché. Da parte tua puoi usare `/info` con il suo ID o username.
Entrambi i comandi sono aperti a chiunque, non servono permessi.

### Il bot mi scrive che non ha i permessi.

Vuol dire che in quel gruppo non è amministratore, o lo è ma senza il permesso
di bloccare utenti. Il messaggio ti dice anche quanti giorni mancano prima che
il bot esca: dopo tre avvisi lascia il gruppo.

### A cosa servono le categorie obbligatorie?

Servono per le cose su cui non si tratta, per esempio le truffe: valgono in
tutti i gruppi e nessun amministratore di gruppo può disattivarle. Le
categorie opzionali invece le accende chi vuole, gruppo per gruppo, con
`/setcategories`.

### Le prove dove finiscono?

Restano nell'archivio del bot e le rileggi con `/prove`. Se registri una chat
di archivio con `/addbakchat`, il bot ci ricopia dentro i messaggi usati come
prova, così restano al sicuro anche se le chat originali spariscono.
