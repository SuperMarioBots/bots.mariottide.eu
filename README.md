# bots.mariottide.eu

Sito di documentazione utente dei bot Telegram del progetto. Italiano di
default, inglese come lingua secondaria.

Generatore: [Zola](https://www.getzola.org/) 0.23. Tema scritto a mano, nessuna
risorsa esterna, nessuna dipendenza JavaScript.

## Sviluppo

```bash
zola serve     # anteprima su http://127.0.0.1:1111
zola check     # link interni ed esterni
zola build     # output in public/
```

## Struttura

```
content/_index.md         home
content/bot/<slug>/       una pagina per bot pubblico
content/guida/            clonazione, permessi, FAQ, contatti
templates/                base, index, section, page
sass/style.scss           tutto il CSS
static/CNAME              dominio per GitHub Pages
```

Le traduzioni inglesi sono file affiancati: `index.md` e `index.en.md`. Se la
traduzione manca, il selettore di lingua rimanda alla home inglese.

## Regole di contenuto

Le pagine documentano il **software**, non le singole istanze: la maggior
parte di questi bot vive come flotta di cloni con username diversi, e quegli
username non vanno elencati qui.

Front matter obbligatorio per una pagina bot:

```toml
[extra]
emoji = "🚷"
repo = "BlocklistBots"   # nome esatto della directory del repo
username = "NomeBot"     # solo se esiste un bot pubblico principale
clonable = true
```

Il campo `repo` viene verificato da `just contracts` (check
`docs-site-coverage`): ogni repo di bot deve avere almeno una pagina.

## Aggiornamento

Vedi la sezione "User documentation site" in `../AGENTS.md`: il sito si
aggiorna nella stessa change che cambia il bot, non dopo.

## Deploy

Push su `master`, GitHub Actions builda e pubblica su GitHub Pages.
