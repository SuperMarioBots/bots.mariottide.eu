+++
title = "Master Control Program"
description = "Amministrazione avanzata per i gruppi: ban automatici sui profili sospetti, antispam, mute di massa e cancellazione a tempo."
weight = 40

[extra]
emoji = "🛡️"
repo = "MasterControlProgramBots"
username = "MasterControlProgramBot"
clonable = true
+++

## Cosa fa

Master Control Program è il bot di amministrazione per i gruppi grandi, quelli
dove i profili spam entrano a ondate e nessuno ha voglia di guardarli uno per
uno. Il pezzo forte sono gli specialban: descrivi che aspetto ha un profilo
indesiderato (nome, bio, lingua, età, canale personale) e il bot banna da solo
chiunque corrisponda, appena entra o appena scrive.

Intorno a quello ci sono i lavori sporchi di ogni gruppo: cancellare i messaggi
di servizio, togliere l'intestazione "inoltrato da" ai messaggi ripubblicati dai
canali, limitare quanti link al giorno può mandare una persona, mutare chi entra
finché un admin non lo sblocca, bannare chi entra ed esce di continuo, cancellare
i media dopo qualche ora, trovare i membri inattivi.

Tutte le impostazioni si gestiscono con `/msettings`, un pannello a bottoni che
mostra come è configurato il gruppo in quel momento. I comandi scritti restano
validi e fanno esattamente le stesse cose: usa quello che ti è più comodo.

## Prima di iniziare

Il bot si usa nei gruppi (funziona anche nei supergruppi con i topic). In privato
rispondono solo i comandi informativi.

Va aggiunto al gruppo e promosso amministratore. I permessi Telegram che servono:

- **Elimina messaggi**: per i messaggi di servizio, i messaggi di chi viene
  bannato, la cancellazione a tempo dei media e il limite antispam.
- **Blocca utenti**: per gli specialban, i ban di chi esce, i mute di massa.
- **Fissa messaggi**: solo se vuoi che sfissi da solo i post inoltrati dal canale
  collegato.
- **Aggiungi amministratori**: solo se usi `/addtitle` per dare i titoli
  personalizzati agli admin.

Se vuoi il canale di log, il bot deve essere amministratore anche là.
Dettagli in [Permessi Telegram](@/guida/permessi.md).

## Configurazione

1. Aggiungi il bot al gruppo e promuovilo amministratore con i permessi qui
   sopra.
2. Scrivi `/msettings` nel gruppo: si apre il pannello con tutte le impostazioni.
3. Accendi quello che ti serve toccando i bottoni. Le voci con un valore
   (Automute, Uscitiban, Spam limit, ore della cancellazione a tempo) girano fra
   i valori possibili a ogni tocco.
4. Entra in **Specialbans** e aggiungi le prime regole. Il pannello ti guida per
   categoria: Nome, Bio, Lingua, Età utente, Canale personale.
5. Se vuoi tenere traccia di quello che il bot fa, crea un canale, mettici il bot
   come amministratore, poi scrivi `/canalelog` nel gruppo e inoltra nel canale
   il messaggio che il bot ti dà. Conferma con **Sì**.
6. Escludi dagli automatismi le persone che devono restare fuori (bot di
   servizio, redattori che inoltrano dai canali) con i comandi di esclusione.

## Comandi

### Informazioni

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/start` | Messaggio di benvenuto | tutti | privato |
| `/help` | Rimanda alla guida e suggerisce di clonare | tutti | privato e gruppo |
| `/clone` | Istruzioni per creare il tuo clone | tutti | privato e gruppo |
| `/ping` | Risponde PONG, serve a vedere se il bot è vivo | tutti | privato e gruppo |
| `/info` | ID, lingua e datacenter di una persona (in risposta, con `@username` o con l'ID) | tutti | privato e gruppo |
| `/dc` | Solo il datacenter, ricavato dalla foto profilo | tutti | privato e gruppo |
| `/search_id @utente` | Storico dei nomi e degli username di quella persona | tutti | privato |
| `/test` | Quanti membri ha il gruppo | tutti | privato e gruppo |
| `/stats` | Quanti cloni e quante chat gestisce il bot | tutti | privato e gruppo |

### Pannello impostazioni

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/msettings` | Apre il pannello a bottoni con tutte le impostazioni della chat | admin del gruppo | gruppo |
| `/mimpostazioni` | Lo stesso pannello, con il nome in italiano | admin del gruppo | gruppo |

### Moderazione automatica

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/delservice` | Cancella i messaggi di servizio (ingressi, uscite, cambi di foto) | admin del gruppo | gruppo |
| `/undelservice` | Smette di cancellarli | admin del gruppo | gruppo |
| `/disinoltra` | Ripubblica i messaggi inoltrati dai canali senza l'intestazione, e dice chi li aveva mandati | admin del gruppo | gruppo |
| `/undisinoltra` | Disattiva il disinoltro | admin del gruppo | gruppo |
| `/silent` | Il bot smette di annunciare in chat quello che fa | admin del gruppo | gruppo |
| `/unsilent` | Torna ad annunciarlo | admin del gruppo | gruppo |
| `/sfissadiscussione` | Sfissa da solo i post inoltrati dal canale collegato | admin del gruppo | gruppo |
| `/unsfissadiscussione` | Smette di sfissarli | admin del gruppo | gruppo |
| `/uscitiban 2` | Banna chi esce dal gruppo il numero di volte indicato (senza numero vale 1) | admin del gruppo | gruppo |
| `/unuscitiban` | Disattiva il ban di chi esce e azzera il conteggio | admin del gruppo | gruppo |
| `/automute` | Muta chi entra, finché un admin non lo sblocca | admin del gruppo | gruppo |
| `/automutemedia` | Chi entra può scrivere testo ma non mandare media | admin del gruppo | gruppo |
| `/unautomute` | Disattiva il mute all'ingresso | admin del gruppo | gruppo |
| `/setspamlimit 10` | Limite giornaliero di inoltri e link a Telegram (inviti e `@username` di gruppi o canali) per persona, oltre il quale il messaggio viene cancellato | admin del gruppo | gruppo |
| `/unsetspamlimit` | Toglie il limite e azzera i conteggi | admin del gruppo | gruppo |
| `/specialbans` | Elenca le regole di specialban attive nel gruppo | admin del gruppo | gruppo |
| `/specialban bioparziale onlyfans` | Aggiunge una regola di specialban | admin del gruppo | gruppo |
| `/unspecialban bioparziale onlyfans` | Toglie quella regola | admin del gruppo | gruppo |
| `/setspecialbanreplymessage` | In risposta a un media, lo salva: il bot lo manderà dopo ogni specialban | admin del gruppo | gruppo |
| `/unsetspecialbanreplymessage` | Toglie il media salvato | admin del gruppo | gruppo |
| `/setuscitibanreplymessage` | Lo stesso, per i ban di chi esce | admin del gruppo | gruppo |
| `/unsetuscitibanreplymessage` | Toglie il media salvato | admin del gruppo | gruppo |

### Esclusioni

Ogni automatismo si può disattivare per una persona sola. Il comando funziona in
risposta a un suo messaggio, con `@username` o con l'ID numerico.

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/specialbanescludi @utente` | Quella persona non verrà mai bannata dalle regole di specialban | admin del gruppo | gruppo |
| `/unspecialbanescludi @utente` | Toglie l'esclusione | admin del gruppo | gruppo |
| `/disinoltraescludi @utente` | I suoi inoltri dai canali restano come sono | admin del gruppo | gruppo |
| `/undisinoltraescludi @utente` | Toglie l'esclusione | admin del gruppo | gruppo |
| `/spamlimitescludi @utente` | Il limite giornaliero non vale per lei | admin del gruppo | gruppo |
| `/unspamlimitescludi @utente` | Toglie l'esclusione | admin del gruppo | gruppo |
| `/uscitibanescludi @utente` | Può entrare e uscire quanto vuole senza essere bannata | admin del gruppo | gruppo |
| `/unuscitibanescludi @utente` | Toglie l'esclusione | admin del gruppo | gruppo |

### Moderazione manuale

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/listmuted` | Elenca tutti i membri con restrizioni attive | admin del gruppo | gruppo |
| `/kmute` | Caccia dal gruppo tutti i membri mutati | admin del gruppo | gruppo |
| `/allmute` | Muta tutti i membri che non sono admin o bot | admin del gruppo | gruppo |
| `/allunmute` | Ridà la parola a tutti i membri mutati che non sono admin | admin del gruppo | gruppo |
| `/minattivi 30` | Cerca chi non scrive da quel numero di giorni (senza numero, 20) e propone di cacciarli o bannarli | admin del gruppo | gruppo |
| `/addtitle @utente Moderatore` | Dà un titolo personalizzato a un amministratore | admin del gruppo | gruppo |
| `/deltitle @utente` | Toglie i poteri di amministratore, titolo compreso | admin del gruppo | gruppo |

### Cancellazione a tempo

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/setdickcmd sera notte` | Definisce le parole che marcano un media da cancellare. Senza parole, disattiva la funzione | admin del gruppo | gruppo |
| `/setdickhours 2.5` | Dopo quante ore cancellare (2.5 vuol dire due ore e mezza) | admin del gruppo | gruppo |

Chi manda un media scrive `#sera` nella didascalia, oppure risponde al proprio
media con `/sera`. Per cambiare il tempo solo per quel media si scrive
`#sera1h` o `#sera30m`.

### Unsplash

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/enableunsplash` | Abilita `/unsplash` nel gruppo | admin del gruppo | gruppo |
| `/disableunsplash` | Lo disabilita | admin del gruppo | gruppo |
| `/unsplash frase da mettere` | Trasforma la frase in un'immagine in stile citazione. In risposta a un messaggio usa il testo di quel messaggio | tutti | privato, e nei gruppi dove è abilitato |

### Log

| Comando | Cosa fa | Chi | Dove |
|---|---|---|---|
| `/canalelog` | Spiega come collegare il canale di log e ti dà il messaggio da inoltrare | admin del gruppo | gruppo |
| `/setlogchannel` | È il messaggio da inoltrare nel canale: fa partire la richiesta di conferma | admin del gruppo | nel canale di log |

## Regole di specialban

Una regola dice al bot che aspetto ha un profilo da bannare. Si aggiungono con
`/specialban <tipo> <valore>`, oppure dal pannello, che per le stesse cose fa le
domande in italiano. Le regole valgono solo nel gruppo dove le scrivi.

| Tipo | Cosa banna | Esempio |
|---|---|---|
| `nome` | Il nome, o nome e cognome insieme, è esattamente quel testo (maiuscole e minuscole non contano) | `/specialban nome Anna` |
| `nomeparziale` | Il nome contiene quel testo come parola intera, senza distinzione fra maiuscole e minuscole: `escort` non prende `escortgirl` | `/specialban nomeparziale escort` |
| `nomealfabeto` | Il nome contiene caratteri di un alfabeto: ARABIC, CYRILLIC, GREEK, HEBREW, LATIN | `/specialban nomealfabeto CYRILLIC` |
| `nomewildcard` | Il nome corrisponde a un modello con l'asterisco come jolly | `/specialban nomewildcard *bitcoin*` |
| `lang` | La persona usa Telegram in quella lingua (codice di due lettere) | `/specialban lang ru` |
| `bio` | La bio è esattamente quel testo (maiuscole e minuscole non contano) | `/specialban bio cerco amici` |
| `bioparziale` | La bio contiene quel testo come parola intera | `/specialban bioparziale onlyfans` |
| `bioalfabeto` | La bio contiene caratteri di quell'alfabeto | `/specialban bioalfabeto ARABIC` |
| `biotemplate` | La bio rientra in una categoria pronta: LINK (qualsiasi link), TELEGRAMLINK (link a Telegram), CAM (profili cam) | `/specialban biotemplate CAM` |
| `biowildcard` | La bio corrisponde a un modello con l'asterisco come jolly | `/specialban biowildcard *t.me/*` |
| `age` | L'età dichiarata nel profilo è sotto quel numero di anni | `/specialban age 18` |
| `channel` | La persona ha un canale personale collegato al profilo. Non vuole nessun valore | `/specialban channel` |

Le regole sul nome e sulla lingua si applicano subito. Quelle che guardano la
bio, l'età e il canale personale richiedono di leggere il profilo completo, cosa
che Telegram concede a ritmo limitato: qualche secondo di ritardo è normale.
La regola `age` funziona solo se la persona ha impostato il compleanno nel
profilo.

Per togliere una regola si usa lo stesso tipo e lo stesso valore
(`/unspecialban bioparziale onlyfans`), oppure il cestino accanto alla regola
nel pannello.

## Bottoni e automatismi

Quando qualcuno entra nel gruppo, il bot lo confronta con le regole di
specialban. Se una regola corrisponde, lo banna, cancella tutti i messaggi che
gli ha già visto scrivere, manda il media che hai salvato con
`/setspecialbanreplymessage` e scrive l'accaduto nel canale di log. Il controllo
si ripete anche sui messaggi normali, quindi prende anche chi era già dentro
prima che la regola esistesse, o chi cambia nome e bio dopo essere entrato.

Il pannello di `/msettings` è tutto a bottoni: la spunta verde o la croce
indicano se un'impostazione è accesa, le voci con un numero girano fra i valori
disponibili a ogni tocco, e le sezioni **Timed delete** e **Specialbans** si
aprono in un sottomenu. Le regole di specialban si aggiungono da lì rispondendo
a domande, e si cancellano con l'icona del cestino.

`/minattivi` risponde con l'elenco degli inattivi e due bottoni, **Kikka tutti**
e **Banna tutti**. La lista arriva in privato, quindi la chat con il bot deve essere già
aperta: se il bot non riesce a scriverti, ti dà un bottone per aprirla.
Se l'elenco è troppo lungo per un messaggio, il bot manda un link al testo
completo.

Nel canale di log, ai messaggi di ingresso il bot aggiunge da solo il datacenter
di chi è entrato, e mette in evidenza quelli fuori dall'Europa.

Il resto lavora senza comandi: i messaggi di servizio spariscono, gli inoltri dai
canali vengono ripubblicati puliti, chi supera il limite giornaliero si vede
cancellare il messaggio con un avviso, chi entra viene mutato, i media marcati
spariscono allo scadere del tempo.

## Domande frequenti

### Meglio i comandi o il pannello?

Il pannello, perché ti mostra com'è messo il gruppo adesso. I comandi servono
quando sai già cosa vuoi, o quando devi impostare qualcosa che il pannello non
chiede, come un'espressione regolare lunga o un titolo da amministratore.

### Ho aggiunto una regola ma i profili spam sono ancora dentro

Le regole non ripuliscono il gruppo da sole. Vengono applicate a chi entra e a
chi scrive: i profili già dentro che restano zitti non vengono toccati.

### Il bot non banna

Controlla il permesso **Blocca utenti**. Se il permesso c'è, guarda se la persona
è fra le esclusioni (`/specialbanescludi` la mette al riparo da tutte le regole)
o se è amministratore: gli admin non vengono mai toccati dagli automatismi.

### Perché non cancella i messaggi vecchi?

Telegram permette a un bot di cancellare i messaggi altrui solo entro 48 ore.
Vale per la cancellazione a tempo dei media e per la pulizia dopo un ban.

### Il canale di log resta vuoto

Il bot deve essere amministratore nel canale, con il permesso di scrivere, e il
collegamento va confermato con il bottone **Sì** che arriva nel gruppo dopo aver
inoltrato il messaggio di `/setlogchannel`.

### `/unsplash` non funziona nel gruppo

Va abilitato una volta per gruppo con `/enableunsplash`. In privato con il bot
funziona sempre.

### Conviene clonare?

Sì. Un clone dedicato al tuo gruppo non divide i limiti di Telegram con tutte le
altre chat, quindi ban e cancellazioni arrivano prima.
