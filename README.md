# rundok.de

Website der Begehungs-App RUNDOK (Ingenieurbüro IBW). Statische Seite, gehostet auf dem IONOS Webhosting Premium (Ordner /rundok, Vertrag 66145799).

- `index.html` – Startseite (CSS/JS inline, keine Fremdaufrufe)
- `impressum.html`, `datenschutz.html`, `legal.css`
- `screens/` – vier App-Screenshots (iPhone-Simulator, Demo-Daten, keine Kundendaten)
- `fonts/` – Geist und Geist Mono lokal (OFL 1.1, Lizenztext in `fonts/OFL.txt`), kein Google-Fonts-Aufruf
- `logo/` – `rundok-icon.svg` ist das Favicon der drei Seiten. `rundok-logo.svg` wird von der Website **nicht** benutzt: die Wortmarke steckt als Inline-SVG in `index.html`. Die Datei ist die Vorlage für Briefkopf, Presse und Druck — wer die Wortmarke ändert, ändert beide.
- `robots.txt`, `sitemap.xml`
- `.htaccess` – erzwingt https://rundok.de, leitet www/.app/.info um, setzt Sicherheits-Header, sperrt interne Dateien

## Veröffentlichen

Diese Dateien und Ordner gehören auf den Webspace:

```
index.html  impressum.html  datenschutz.html  legal.css
.htaccess  robots.txt  sitemap.xml
fonts/  logo/  screens/
```

**Nicht hochladen:** `README.md`, `UEBERGABE-Website.md`, `*.patch`, `.git/`. Die `.htaccess` sperrt sie zusätzlich für den Fall, dass der Ordner als Ganzes hochgeladen wird — im README stehen Vertrags- und Zugangsdaten.

Dateien per IONOS Webspace Explorer oder SFTP (Server home690905809.1and1-data.host, Benutzer u89952178) in den Ordner `/rundok` laden. rundok.de ist im IONOS Domain Center auf `/rundok` verbunden, rundok.app und rundok.info leiten per Domain-Weiterleitung auf https://rundok.de.

Nach dem Hochladen zwei Proben: `https://rundok.de/` lädt mit den Screenshots, und `https://rundok.de/README.md` liefert 403 oder 404 statt des Dateiinhalts.
