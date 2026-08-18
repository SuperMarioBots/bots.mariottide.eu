+++
title = "Permessi Telegram"
description = "Quali permessi dare al bot nel gruppo o nel canale, e cosa succede se mancano."
weight = 2
+++

Telegram non dice mai a un bot "ti manca un permesso" prima che provi a fare
qualcosa: il bot se ne accorge quando fallisce. Per questo quasi tutti i
problemi ("non banna", "non cancella", "non fissa") sono un permesso mancante.

## Come si promuove un bot

Nel gruppo: **Info gruppo**, poi **Amministratori**, poi **Aggiungi
amministratore**, scegli il bot e spunta i permessi. Nei canali il percorso è
lo stesso.

Se cambi i permessi a un bot già promosso, il bot lo vede subito: non serve
rimuoverlo e riaggiungerlo.

## Quali permessi servono, bot per bot

| Permesso | Serve a | Bot |
|---|---|---|
| Elimina messaggi | Cancellare media a tempo, messaggi di servizio, messaggi di chi finisce in blocklist | Cazzinator, Master Control Program, Blocklist, AnonyMedia |
| Blocca utenti | Bannare e mutare | Blocklist, Master Control Program, CAM Manager |
| Invita utenti con link | Generare i link di invito | CAM Manager, Networks |
| Fissa messaggi | Fissare la lista pubblicata | Networks |
| Aggiungi amministratori | Dare un titolo personalizzato a un admin, o togliergli i poteri | Master Control Program (`/addtitle` e `/deltitle`) |
| Nessuno, ma promosso | Vedere la lista dei membri in un gruppo che la tiene nascosta | Tagga |
| Nessuno | Il bot lavora da utente normale, se la lista dei membri è visibile a tutti | Tagga |

## Modalità privacy

Di default un bot non legge tutti i messaggi del gruppo, ma solo comandi e
risposte dirette. I bot che devono leggere tutto (per esempio per contare i
messaggi o per cancellare quelli di un utente bannato) hanno la privacy già
disattivata dalla mia parte.

Se cloni un bot, la modalità privacy del **tuo** clone la imposti tu su
@BotFather: `/mybots`, scegli il bot, **Bot Settings**, **Group Privacy**,
**Turn off**. Poi togli e rimetti il bot nel gruppo, perché Telegram applica
la modifica solo alla riaggiunta.

## Gruppi con i topic (forum)

Nei gruppi forum molti bot vanno configurati **dentro il topic giusto**:
il comando registra la coppia gruppo più topic, non solo il gruppo. Vale per
la chat staff di Blocklist e AnonyMedia e per le chat operatore di Better
Limitati. Se sbagli topic, il bot scrive nel posto sbagliato: rilancia il
comando dal topic corretto.

## Lista dei membri nascosta

Un gruppo può nascondere la lista dei membri (nelle impostazioni del gruppo,
alla voce che decide chi può vedere gli iscritti). Telegram allora mostra
quella lista solo agli amministratori, bot compresi.

Vuol dire che un bot che deve nominare o contare i membri, come Tagga, in quel
gruppo vede soltanto gli amministratori e nomina solo loro. La soluzione è
promuovere il bot amministratore lasciando tutte le caselle dei permessi
spente: gli serve il ruolo, non i poteri.

## Limiti di Telegram che non dipendono dal bot

- Un bot può cancellare i messaggi altrui solo entro **48 ore**.
- Le menzioni multiple sono limitate: Tagga può nominare al massimo
  **5 persone per messaggio**.
- Un bot non vede i membri che non hanno mai scritto e non ha modo di
  elencare tutti gli iscritti di un gruppo.
- I ban sui gruppi dove il bot è appena entrato richiedono qualche minuto:
  vengono eseguiti in coda, non tutti insieme.
