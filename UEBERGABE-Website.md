# Übergabe: rundok.de fertig bauen

**Für CoWork · Stand 08.09.2026 · Ingenieurbüro Wildmoser (IBW), München**

Dieses Blatt ist die vollständige Arbeitsanweisung. Alles darin ist im Quelltext nachgeprüft,
nicht aus Erinnerung geschrieben, und von drei unabhängigen Prüfläufen gegengelesen. Sie
brauchen keine Rückfrage, um anzufangen: Auftrag A liegt als fertiger Patch bei, Auftrag B
ist eine Liste mit Datei und Zeile, Abschnitt 4 sind die fünf Dinge, die **nicht** Sie
entscheiden.

Repo: `vf4cfxtnvs-stack/rundok-website` (privat) · Domain rundok.de · Hosting IONOS, statisch.

**Ausgangsstand: Commit `a527c16` auf `main`.** Der beiliegende Patch setzt genau
diesen Stand voraus. Ist Ihr Arbeitsbaum weiter, prüfen Sie mit `git apply --check`, bevor
Sie anwenden.

---

## 0. In drei Sätzen

Die Seite steht inhaltlich. Was fehlt, sind die echten App-Screenshots im Kopf der Seite —
dort klebt noch eine gezeichnete Telefon-Attrappe. Die vier Bilder liegen in `screens/`,
der Einbau liegt als `screens-einbau.patch` bei und ist in Chrome gerendert und angesehen
worden; danach bleiben Kleinigkeiten und fünf Fragen an den Auftraggeber.

---

## 1. Drei Regeln, die über allem stehen

**Erstens: Auf dieser Seite steht nur, was die Software heute wirklich kann.** Sie wirbt
gegenüber Kirchenstiftungen, Kommunen und Hausverwaltungen. Eine Zusage, die im Piloten
nicht hält, kostet den Auftraggeber den Kunden. Wer eine Funktion ergänzen will, belegt sie
vorher im Code oder im Handbuch (Abschnitt 6 sagt, wo). Im Zweifel weglassen.

**Zweitens: Der Kunde bekommt nie das Cockpit.** Er bekommt die App und einzelne Blätter.
Keine Formulierung darf klingen, als bediene er die Zentrale selbst. Das Cockpit läuft beim
Ingenieurbüro IBW in München und bleibt dort.

**Drittens: eine Datei bleibt eine Datei.** `index.html` trägt HTML, CSS und JS inline. Kein
Framework, kein Build-Schritt, kein CDN, kein Analyse-Skript, keine externe Schrift — die
Schrift Geist liegt in `fonts/`. Das ist kein Geschmack, sondern die Grundlage der
Datenschutz-Aussagen auf der Seite. Wer daran rührt, bricht `datenschutz.html`.

Nebenregel zur Sprache: Die Seite argumentiert positiv. Verneinungen sind erlaubt, wo sie
eine Tatsache benennen („kein Konto für die Firma"), nicht dort, wo sie einen Vorwurf
verneinen. Der Satz „keine Vertriebsmasche" ist am 08.09. aus genau diesem Grund raus.

---

## 2. Auftrag A: die Screenshots einbauen (Hauptpunkt)

### 2.1 Der fertige Weg

```
git apply screens-einbau.patch
```

Der Patch ändert nur `index.html`:

| Stelle | Was passiert |
|---|---|
| CSS vor `/* hero */` | neue Klassen `.shot`, `.shots`, `.schau` |
| CSS bei den `.phone`-Regeln | `.frame--shot` für das Bild im Telefonrahmen |
| CSS der alten Attrappe | acht tote Regeln fallen weg (`.tile-grid`, `.tile`, `.mail` …) |
| Hero, `<div class="phone">` | die gezeichnete Attrappe weicht `screens/01-kacheln.png` |
| Abschnitt „Die Kette" | neuer Block „Aus der Ziffer wird die Meldung" mit `03-meldung.png` |
| Reiter „Feld-App" | Bildstreifen mit `02-pruefliste.png` und `05-projekt.png` |

`git apply --check screens-einbau.patch` läuft sauber gegen den oben genannten Commit.

**Die Patch-Datei bleibt liegen, bis Abschnitt 8 durch ist** — sie ist die einzige
Rückfahrkarte, wenn der Einbau kippt. Erst danach löschen. Auf den Server gehört sie nie
(Abschnitt 7).

### 2.2 Was der Patch gestalterisch tut, falls Sie ihn nachbauen müssen

- **Der Telefonrahmen bleibt.** Das Bild sitzt im vorhandenen `.frame`, Schatten und der
  schräge Stempel „FREIGEGEBEN · OK" bleiben unverändert. `aria-hidden="true"` fällt weg,
  sonst wäre der alt-Text für Screenreader tot.
- **`.shot` setzt `margin:0`.** Die Bildkarten sind `<figure>`-Elemente, und der
  Browser-Standard für `figure` ist `margin: 1em 40px`. Die Seite setzt `margin:0` nur für
  `p` und `h1`–`h3`. Ohne die Zeile rendern die Karten 240 statt 320 px breit und stehen
  eingerückt neben dem übrigen Inhalt. Das war im ersten Entwurf der Fehler.
- **Der Hero-Zuschnitt liegt in einer Lücke, nicht mitten im Bild.** In `01-kacheln.png`
  (1206 × 2622) endet der Inhalt bei Bildzeile 2426, dann ist bis 2474 nichts; die blaue
  Zeile „Foto nachholen" liegt bei 2475–2519, wieder eine Lücke bis 2568, und ab 2569 steht
  der große blaue Knopf, den das Bild nur noch anschneidet. Gültige Schnittkanten sind also
  **2427–2474** (beides weg, gewählt: `aspect-ratio:1206/2470`) oder **2520–2568**
  („Foto nachholen" bleibt stehen, der Knopf ist weg). Wer einen anderen Wert setzt,
  schneidet Text waagrecht durch.
- **`02-pruefliste.png` ist unten zu 42 % leer**, weil der Demo-Prüfplan nur zwei Punkte hat.
  Deshalb `.shot--kurz` mit `aspect-ratio:1206/1575`; die letzte Inhaltszeile liegt bei 1526.
- **`.shots` hat `align-items:start`** und höchstens 320 px je Spalte (`minmax(0,320px)`,
  darunter schrumpfen sie mit). Ohne `align-items:start` zieht das Raster beide Karten auf
  dieselbe Höhe, und unter der kürzeren klafft ein schwarzes Loch.
- **Die Absätze im Block „Die Kette" sind auf `46ch` gedeckelt.** Ohne Deckel werden die
  Zeilen auf großen Schirmen weit über 100 Zeichen lang und unlesbar. Der Deckel gehört auf
  `.schau p`, nicht auf den umgebenden Kasten — dort wirkt er kaum, weil der Kasten eine
  andere Schriftgröße erbt als der Text.

### 2.3 Wie das geprüft wurde

Gerendert mit Chrome (headless) gegen einen lokalen Server; angesehen wurden der Kopf der
Seite bei 1440 px, der Abschnitt „Die Kette" und der Reiter „Feld-App" je einzeln, dazu
390 px Telefonbreite. Gemessen: `documentElement.scrollWidth` gegen `clientWidth` bei 390 px
ergibt **390/390 vorher wie nachher** — kein waagrechtes Scrollen. Die HTML-Verschachtelung
ist mit einem Parser gegengelesen, keine offenen Tags. Der Patch wurde in einer Wegwerf-Kopie
angewendet und die Abnahmeliste aus Abschnitt 8 daran durchgespielt.

### 2.4 Danach

- `README.md`: die Zeile, die mit „Echte App-Screenshots" beginnt, aus der Offen-Liste
  streichen (siehe B1, gleiche Datei).
- `sitemap.xml`: `lastmod` auf den Tag der Bearbeitung setzen (steht auf 2026-09-07).

---

## 3. Auftrag B: Kleinigkeiten, alle belegt

Alle vier README-Eingriffe (B1 bis B3 und der Punkt aus 2.4) treffen dieselbe Datei. Arbeiten
Sie dort **nach Text, nicht nach Zeilennummer** — jede Einfügung verschiebt die folgenden
Zeilen.

| # | Datei | Was zu tun ist |
|---|---|---|
| B1 | `README.md`, Abschnitt „## Offen" | Beide Punkte streichen: „USt-IdNr. eintragen" ist erledigt (steht seit Commit `0cd10dd` im Impressum, `impressum.html:24`, DE309425223), „Echte App-Screenshots" erledigen Sie mit Auftrag A. Danach ist die Überschrift „## Offen" leer — sie geht mit weg. |
| B2 | `README.md`, Dateiliste | Ergänzen: `screens/`, `robots.txt`, `sitemap.xml`. Wer streng nach der Liste hochlädt, lädt die Screenshots nicht mit — vier tote Bilder auf der Startseite wären die Folge. |
| B3 | `README.md`, Abschnitt „Veröffentlichen" | Die Upload-Liste aus Abschnitt 7 dieses Blattes übernehmen, mit der Zeile, was **nicht** auf den Server gehört. |
| B4 | `.htaccess` | **Ist im Ausgangsstand schon erledigt, bitte nicht rückgängig machen:** eine `FilesMatch`-Sperre für `.md` und `.patch` sowie `RedirectMatch 404 ^/\.git`. Ohne sie wären `rundok.de/README.md` und die ganze Versionsgeschichte öffentlich abrufbar — im README stehen IONOS-Vertragsnummer, SFTP-Server und SFTP-Benutzername. Falls die Seite nach dem Upload plötzlich 500 liefert, kann der Server die Apache-2.4-Syntax nicht: dann `Order allow,deny` / `Deny from all` nehmen. |
| B5 | `legal.css:15`, `impressum.html:25-26` | Klasse `.todo` (gelbe Platzhalter-Markierung) wird nirgends mehr benutzt, raus. Dazu die doppelte Leerzeile im Impressum, wo der Platzhalter stand. |
| B6 | `fonts/` | Es fehlt der Lizenztext. `impressum.html:43` und `README.md:7` nennen die SIL Open Font License 1.1 für die Schrift Geist; die OFL verlangt, dass Copyright-Vermerk und Lizenztext mitgeliefert werden. Legen Sie `fonts/OFL.txt` mit dem **Originaltext und der Copyright-Zeile aus dem Quellprojekt der Schrift** an. In den vier woff2-Dateien steht kein Copyright-Eintrag mehr (Subset), erfinden Sie also nichts — kommen Sie an den Originaltext nicht heran, melden Sie den Punkt als offen zurück. |

---

## 4. Fünf Fragen an den Auftraggeber — nicht selbst entscheiden

1. **HTTPS.** Zwei Stellen behaupten es: `datenschutz.html:45` („wird ausschließlich über
   HTTPS ausgeliefert") und `README.md:9` („erzwingt https://rundok.de"). In `.htaccess:9-10`
   ist die Erzwingung auskommentiert, mit dem Hinweis, sie erst nach aktivem
   IONOS-Zertifikat einzuschalten. Solange das so bleibt, stimmen beide Sätze nicht. Entweder
   Zertifikat prüfen und die zwei Zeilen einkommentieren, oder beide Sätze entschärfen. (Die
   Umleitung fremder Hostnamen in `.htaccess:4-5` schickt schon heute auf `https://` — ohne
   Zertifikat laufen genau diese Besucher in die Warnung.)
2. **Impressum, berufsrechtlicher Teil.** Vorhanden sind Anbieter, Anschrift, Kontakt,
   USt-IdNr. und der Verantwortliche nach § 18 Abs. 2 MStV. Es fehlt jede Rubrik zu Kammer
   oder Aufsichtsbehörde, gesetzlicher Berufsbezeichnung und Berufshaftpflicht. Ob das
   gefordert ist, hängt daran, wie das Büro geführt wird — das ist keine Frage, die CoWork
   beantwortet, und dies ist keine Rechtsberatung. Hier ist nur die Lücke benannt.
3. **Welche Firmen-Domäne führt.** Die Seite zeigt zwei nebeneinander. `3DLaser.de` steht an
   fünf Stellen: `index.html:472` (mailto), `:479` (Schwesterseite), `:491` (Fußzeile),
   `impressum.html:21` (E-Mail und Web in einer Zeile), `datenschutz.html:19`. Daneben
   `tickets@wildmoser-ing.de` in `index.html:480`. Ein Interessent muss raten, wer der
   Anbieter ist. Erst entscheiden, dann alle fünf Stellen gleichziehen.
4. **Das ungenutzte Logo.** `logo/rundok-logo.svg` wird von keiner Seite referenziert; die
   Wortmarke steckt als Inline-SVG in `index.html:164`, und beide laufen schon auseinander
   (unterschiedlicher Fallback-Stack der Schrift). Angleichen oder die Datei als reine
   Vorlage für Briefkopf und Presse führen? Das ist eine Frage an den Markenauftritt.
   Bis zur Antwort: nichts ändern.
5. **Drei Schönheitsfehler in den Screenshots.** In `05-projekt.png` liegt das rote
   Pin-Etikett „S4" auf einer Wandlinie des Grundrisses, und über dem Grundriss steht ein
   leerer grauer Block von rund einem Viertel der Bildhöhe. In `01` und `03` läuft der dritte
   Katalog-Reiter „Betreiberpflichten Gew…" hart in den rechten Bildrand. Das sind echte
   Zustände der App, keine Montagefehler — aber die Bilder stehen groß auf der Startseite.
   Wer so wirbt, entscheidet der Auftraggeber; Abschnitt 6 sagt, wie neue Aufnahmen entstehen.

**Zusatzfrage, technisch:** Im `README.md` stehen IONOS-Vertragsnummer, SFTP-Server und
SFTP-Benutzername. Die `.htaccess`-Sperre verhindert das Ausliefern, aber besser aufgehoben
wären sie im Passwortspeicher statt in einer Datei, die auf dem Webspace landet.

---

## 5. Was schon erledigt ist — bitte nicht doppelt machen

**Am 07. und 08.09.** wurden 16 falsche Aussagen korrigiert (unter anderem: „keine US-Cloud"
war falsch, die KI-Funktionen rufen einen US-Anbieter; die Kontrollgang-Quittung speichert
keine Person; Personen werden nicht automatisch verpixelt; OneDrive erscheint im
Android-Ordnerwähler nicht). 13 Funktionskacheln kamen dazu. Der Abschnitt „Mitarbeiten"
(`#mitarbeiten`) ist neu.

**Zuletzt am 08.09.:**

- Prüfstand-Kachel aus dem Reiter „Cockpit" in den Abschnitt „Mitarbeiten" verschoben; der
  Cockpit-Reiter hat jetzt 13 Kacheln und einen Schlusssatz mit Sprung auf `#mitarbeiten`.
- „Angebot binnen 48 Stunden" → „Angebot innerhalb weniger Tage".
- Überschrift im Kontaktteil: „30 Minuten, Ihr eigenes Objekt, **Ihre eigenen Mängel**."
  (vorher „keine Vertriebsmasche", siehe Regel drei in Abschnitt 1).
- Die Zeile „Stand" in der Kontakt-Karte (`index.html:481`) auf den echten Stand gesetzt:
  App iOS 1.11, Android 0.48, Cockpit 1.60.
- Zahlenwiderspruch behoben: Die Seite nannte an einer Stelle 103 Prüfpunkte mit „64 Punkte"
  für die Kirchenstiftungs-Vorlage und 53 Zeilen später 75. Richtig sind **75 + 39 = 114**,
  in den Vorlagendateien nachgezählt.
- `.htaccess`-Sperre für `.md`, `.patch` und `.git` (siehe B4).
- `screens/01-kacheln.png` neu aufgenommen: die alte Fassung zeigte einen inzwischen
  behobenen Anzeigefehler („14 Ta ge" über drei Zeilen umgebrochen). Jetzt Build 157.

---

## 6. Nachschlagewerk: wo die Wahrheit steht

Diese Quellen liegen auf dem Rechner des Auftraggebers, nicht im Website-Repo. Wer keinen
Zugriff hat, ändert keinen Tatsachensatz auf der Seite, sondern fragt nach.

| Thema | Quelle |
|---|---|
| Cockpit-Funktionen, Chronik jeder Version | `~/Documents/Claude/Projects/begehung` → `BEDIENUNG.md`, `VERSIONS_LOG` in `index.html`, `serve.py` |
| iPhone-App in den Worten des Auftraggebers | `~/Entwicklung/IBWBegehung/IBWBegehung/Ansichten/HilfeView.swift`, freischaltbare Module in `IBWBegehung/AppKonfig.swift` |
| Android-App | `~/Entwicklung/IBWBegehungAndroid` → `BAUPLAN.md`, `.../ansichten/HilfeView.kt` |
| Kataloge, Kacheln, Rechtsgrundlagen | `begehung/meldekataloge.json` |
| Prüfpunkte | `begehung/pruefplaene/*.json` |
| Meldungstypen | `begehung/serve.py` (`TICKET_TITEL`) — **nicht** aus `meldekataloge.json` zählen, dort kommen nur die tatsächlich benutzten vier vor |

Die Zahlen auf der Seite, alle am 08.09. nachgezählt: **12** Kataloge, **191** Meldekacheln,
davon **164** mit Rechtsgrundlage, **6** Meldungstypen, **114** Prüfpunkte in zwei
Prüfplan-Vorlagen (75 + 39). Sie wachsen mit jedem Katalog — beim nächsten Durchgang neu
zählen, nicht abschreiben.

Drei Stolperstellen aus dem Abgleich:

- Was auf dem iPhone läuft, läuft nicht automatisch auf Android. Der Gleichschritt ist die
  Ausnahme, nicht die Regel — immer beide Repos prüfen, bevor eine Funktion ohne
  Geräte-Hinweis auf die Seite kommt.
- „KI" nur schreiben, wo wirklich ein Sprachmodell arbeitet: Bericht veredeln, Plankopf
  lesen, Typenschild lesen, Zeitstände vergleichen, Firmenliste aus Foto. Alles andere sind
  Listen und Regeln.
- Rechtsgrundlagen gehören an den Prüfpunkt und in den Bericht, nicht an die Kachel.

---

## 7. Commit, Upload, und was nicht auf den Server gehört

**Commit.** Ihre Arbeit gehört in einen Commit auf `main`, mit einer Nachricht, die den
Auftrag nennt (etwa „Screenshots im Hero, Reiter Feld-App und Abschnitt Die Kette"). Nichts
verwerfen, was Sie nicht selbst angelegt haben: `git checkout -- .`, `git stash` und
`git clean` sind hier verboten.

**Upload.** Den macht der Auftraggeber; die Zugangsdaten liegen bei ihm. CoWork lädt nicht
hoch, außer er sagt es ausdrücklich. Diese Dateien gehen auf den Webspace:

```
index.html  impressum.html  datenschutz.html  legal.css
.htaccess  robots.txt  sitemap.xml
fonts/  logo/  screens/
```

Nicht auf den Server gehören: `README.md`, `UEBERGABE-Website.md`, `screens-einbau.patch`,
`.git/`. Wird der Ordner als Ganzes hochgeladen — so beschreibt es das README —, fängt die
`.htaccess`-Sperre aus B4 sie ab; verlassen sollte man sich darauf nicht.

---

## 8. Abnahme

**Teil 1 — lokal, das ist Ihre Fertig-Meldung.**

1. Der Kopf der Seite zeigt ein echtes Telefonbild, keine gezeichneten Emoji-Kacheln. Am
   unteren Bildrand ist **kein** angeschnittener blauer Knopf zu sehen.
2. Im Reiter „Feld-App" stehen zwei Bilder nebeneinander, unter jedem eine Bildunterschrift,
   unter dem kürzeren **kein** leerer schwarzer Block. Beide Karten fluchten links mit dem
   übrigen Inhalt des Reiters (das prüft die `margin:0`-Zeile aus 2.2).
3. Im Abschnitt „Die Kette" steht ein Bild links, Text rechts; auf dem Telefon untereinander.
4. Bei 390 px Breite scrollt nichts waagrecht.
5. `grep -c "tile-grid" index.html` liefert **0** — Markup und CSS der Attrappe sind weg.
6. Alle vier Bilder laden, kein 404 in der Netzwerk-Konsole.
7. Der Wortlaut der Seite ist gegenüber dem Ausgangsstand unverändert, bis auf die Absätze,
   die dieses Blatt ausdrücklich verlangt (`git diff` zeigt keine anderen Textänderungen).

**Teil 2 — nach dem Upload, durch den Auftraggeber.**

8. `https://rundok.de/README.md` liefert 403 oder 404, in keinem Fall den Dateiinhalt.
   Dasselbe für `https://rundok.de/.git/config`.
9. Die Startseite lädt (kein 403 durch falsche Dateirechte: `chmod 644 index.html` vor dem
   Hochladen, die Datei steht lokal auf 0600).
10. Punkt 8 setzt ein gültiges Zertifikat voraus — siehe Frage 1 in Abschnitt 4. Solange die
    offen ist, ist eine Zertifikatswarnung kein Fehler der Website.
