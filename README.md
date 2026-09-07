# rundok.de

Website der Begehungs-App RUNDOK (Ingenieurbüro IBW). Statische Seite, gehostet auf dem IONOS Webhosting Premium (Ordner /rundok, Vertrag 66145799).

- `index.html` – Startseite (CSS/JS inline)
- `impressum.html`, `datenschutz.html`, `legal.css`
- `fonts/` – Geist und Geist Mono lokal (OFL 1.1), kein Google-Fonts-Aufruf
- `logo/` – Wortmarke und Icon als SVG
- `.htaccess` – erzwingt https://rundok.de, leitet www/.app/.info um, setzt Sicherheits-Header

## Veröffentlichen

Dateien per IONOS Webspace Explorer oder SFTP (Server home690905809.1and1-data.host, Benutzer u89952178) in den Ordner `/rundok` laden. rundok.de ist im IONOS Domain Center auf `/rundok` verbunden, rundok.app und rundok.info leiten per Domain-Weiterleitung auf https://rundok.de.

## Offen

- USt-IdNr. in `impressum.html` eintragen (gelb markiert)
- Echte App-Screenshots statt der Kachel-Attrappe im Hero
