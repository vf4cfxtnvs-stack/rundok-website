# rundok.de

Website der Begehungs-App RUNDOK (Ingenieurbüro IBW). Statische Seite, gehostet über GitHub Pages.

- `index.html` – Startseite (CSS/JS inline)
- `impressum.html`, `datenschutz.html`, `legal.css`
- `fonts/` – Geist und Geist Mono lokal (OFL 1.1), kein Google-Fonts-Aufruf
- `logo/` – Wortmarke und Icon als SVG
- `CNAME` – bindet rundok.de an GitHub Pages; `.nojekyll` schaltet Jekyll ab

## Veröffentlichen

Push auf `main` genügt. GitHub Pages: Settings → Pages → Source „Deploy from a branch“, Branch `main`, Ordner `/ (root)`, „Enforce HTTPS“ einschalten, sobald das Zertifikat da ist.

## DNS bei IONOS (rundok.de)

A-Records auf 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153; CNAME `www` auf `vf4cfxtnvs-stack.github.io`. rundok.app und rundok.info als Weiterleitung (301) auf https://rundok.de.

## Offen

- USt-IdNr. in `impressum.html` eintragen (gelb markiert)
- Echte App-Screenshots statt der Kachel-Attrappe im Hero
