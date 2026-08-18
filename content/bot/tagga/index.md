+++
title = "Tagga Bot"
description = "Nomina tutti i membri di un gruppo partendo da un solo messaggio."
weight = 10

[extra]
emoji = "📢"
repo = "ToolBoxyBots"
username = "Tagga_Bot"
clonable = true
+++

## Cosa fa

Scrivi un messaggio che inizia con `@all` e il bot risponde nominando tutti i
membri del gruppo, cinque per messaggio. Cinque è il massimo che Telegram
consente in una singola menzione, quindi su un gruppo grande il bot manda
parecchi messaggi di seguito, uno ogni tre secondi circa.

Nella maggior parte dei gruppi il bot lavora da utente normale: gli basta
stare nel gruppo e leggere il messaggio che fa partire il tag. Se però il
gruppo ha la lista dei membri nascosta, Telegram non la mostra a chi non è
amministratore e il bot finisce per nominare solo gli admin: in quel caso
devi promuoverlo, anche senza dargli nessun permesso.

Il resto sono impostazioni: chi può far partire il tag, come devono apparire
le menzioni (nome, emoji o menzione invisibile), se il bot deve rispondere al
tuo messaggio o ricopiarne il testo, e quale parola fa da innesco al posto di
`all`.

## Prima di iniziare

- Si usa in **gruppi e supergruppi**: i tag partono solo lì. In chat privata
  il bot risponde alla guida e a `/clone`.
- Il bot va aggiunto al gruppo. Se la lista dei membri è visibile a tutti,
  basta come **utente normale**.
- Se il gruppo ha la **lista dei membri nascosta**, il bot va promosso
  **amministratore**, altrimenti Telegram gli mostra solo gli amministratori e
  il tag nomina soltanto quelli. Non servono permessi: promuovilo e lascia
  tutte le caselle spente. Vedi [Permessi Telegram](@/guida/permessi.md).
- Funziona anche nei gruppi con i topic: ogni topic ha il suo tag in corso,
  indipendente dagli altri.
- Il bot non nomina gli altri bot né gli account cancellati.

## Configurazione

1. Aggiungi il bot al gruppo. Se nelle impostazioni del gruppo la lista dei
   membri è nascosta, promuovilo amministratore senza spuntare nessun
   permesso.
2. Scrivi un messaggio che **inizia** con `@all`, per esempio
   `@all riunione alle 21`. Vanno bene anche `#all` e `/all`.
3. Il bot conferma con "Comando accettato con successo" e comincia a taggare.
4. Se vuoi che solo gli amministratori possano usarlo, dai `/onlyadmins`.
5. Scegli come devono apparire le menzioni: `/nametagtype` (predefinito),
   `/emojitagtype` oppure `/emptytagtype`.
6. Se preferisci che il bot ricopi il tuo testo invece di rispondere al tuo
   messaggio, dai `/copymessage`.
7. Se `all` non ti piace, cambialo con `/set_tag_command annuncio`: da quel
   momento il tag parte con `@annuncio`.

## Comandi

Il testo deve **iniziare** con la parola di innesco: `@all ragazzi` funziona,
`ragazzi @all` no.

### Per tutti, in gruppo

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `@all messaggio` | Fa partire il tag di tutti i membri, cinque per messaggio. Vanno bene anche `#all` e `/all` | tutti, o solo gli admin se hai dato `/onlyadmins` | Gruppo |
| `/stopall` | Ferma un tag in corso. Valgono anche `@stopall` e `#stopall` | chi ha lanciato il tag o un admin del gruppo | Gruppo |
| `/lottery` | Estrae a sorte un membro del gruppo e lo annuncia | tutti | Gruppo |

### Per gli admin del gruppo

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/onlyadmins` | Il bot accetta i tag solo dagli admin | admin del gruppo | Gruppo |
| `/noonlyadmins` | Il bot accetta i tag da tutti | admin del gruppo | Gruppo |
| `/copymessage` | Il bot copia il testo del messaggio invece di rispondere ad esso, e ci mette sotto un link all'originale | admin del gruppo | Gruppo |
| `/nocopymessage` | Il bot torna a rispondere al messaggio | admin del gruppo | Gruppo |
| `/nametagtype` | Le menzioni mostrano il nome della persona. È l'impostazione predefinita | admin del gruppo | Gruppo |
| `/emojitagtype` | Le menzioni mostrano una faccina a caso al posto del nome | admin del gruppo | Gruppo |
| `/emptytagtype` | Le menzioni sono invisibili: arriva la notifica, ma nel messaggio non si legge niente | admin del gruppo | Gruppo |
| `/set_tag_command annuncio` | Cambia la parola che fa partire il tag in quel gruppo | admin del gruppo | Gruppo |
| `/unset_tag_command` | Rimette la parola predefinita | admin del gruppo | Gruppo |

Queste impostazioni valgono per tutto il gruppo, anche se le dai dentro un
topic.

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

Il bot non ha bottoni: si guida a comandi.

Quando entra in un gruppo registra da solo il menu dei comandi, quindi li
trovi nella tendina `/` senza fare niente.

Un tag alla volta per topic. Se qualcuno ne lancia un altro mentre il primo
sta ancora andando, il bot risponde "@all già in corso, questo comando sarà
ignorato" e cancella l'avviso dopo qualche secondo.

Quando il bot risponde al messaggio che ha fatto partire il tag e quel
messaggio viene cancellato, il bot si ferma e avvisa che l'originale non c'è
più.

Il messaggio di attesa ("il bot inizierà a taggare appena possibile") sparisce
da solo quando parte il primo blocco di menzioni.

## Domande frequenti

### Perché tagga solo cinque persone alla volta?

È un limite di Telegram, non del bot: un messaggio non può contenere più di
cinque menzioni. Su un gruppo da mille persone servono duecento messaggi, e
tra uno e l'altro il bot aspetta qualche secondo per non farsi rallentare.

### Devo renderlo amministratore?

Solo se il gruppo ha la lista dei membri nascosta. In quel caso Telegram non
fa vedere i membri a chi non è admin, quindi il bot nomina soltanto gli
amministratori. Promuoverlo senza spuntare nessun permesso risolve. Negli
altri gruppi non serve.

### Il tag ha saltato delle persone

Se ha nominato solo gli amministratori, il gruppo ha la lista dei membri
nascosta e il bot non è admin: promuovilo. Il bot inoltre non nomina mai gli
altri bot né gli account cancellati. Se mancano persone vere, quasi sempre il
tag si è fermato prima: controlla che il messaggio originale ci sia ancora e
che nessuno abbia dato `/stopall`.

### Come lo fermo se è partito per sbaglio?

`/stopall`. Lo può dare chi ha lanciato il tag oppure un admin del gruppo.

### Posso far partire il tag con una parola mia?

Sì, un admin del gruppo dà `/set_tag_command` seguito dalla parola che vuole.
Vale solo per quel gruppo, e da quel momento la parola vecchia non funziona
più. Con `/unset_tag_command` si torna a quella predefinita.

### Che differenza c'è tra le tre modalità di menzione?

Con `/nametagtype` leggi i nomi, ed è la più chiara. Con `/emojitagtype` al
posto dei nomi compaiono faccine, il messaggio resta corto. Con
`/emptytagtype` la menzione è un carattere invisibile: la notifica arriva
lo stesso, ma il messaggio sembra vuoto.

### È lento sul mio gruppo

Il bot pubblico serve migliaia di chat e i limiti di Telegram sono condivisi.
Un bot dedicato al tuo gruppo parte prima e finisce prima.
