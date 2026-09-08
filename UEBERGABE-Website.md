# rundok.de — hochladefertig

**Stand 08.09.2026 · Ingenieurbüro Wildmoser (IBW), München**

Die Seite ist fertig. Was im Repo liegt, kann so auf den Server. Dieses Blatt sagt in
Abschnitt 1, wie das geht, und in Abschnitt 3, was noch offen ist — nichts davon hält den
Upload auf.

---

## 1. Hochladen (drei Schritte)

**Diese Dateien und Ordner:**

```
index.html  impressum.html  datenschutz.html  legal.css
.htaccess  robots.txt  sitemap.xml
fonts/  logo/  screens/
```

**Nicht hochladen:** `README.md`, `UEBERGABE-Website.md`, `.git/`. Falls doch der ganze
Ordner hochgeht, fängt die `.htaccess` sie ab — im README stehen Vertragsnummer und
SFTP-Zugang.

**So:** IONOS Webspace Explorer oder SFTP (Server `home690905809.1and1-data.host`, Benutzer
`u89952178`) in den Ordner `/rundok`.

**Danach zwei Proben:**

1. `https://rundok.de/` lädt, im Kopf steht ein echtes Telefonbild mit den Kacheln.
2. `https://rundok.de/README.md` liefert 403 oder 404, nicht den Dateiinhalt.

Kommt bei Probe 2 die ganze Seite mit Fehler 500 zurück, versteht der Server die
Apache-2.4-Schreibweise nicht: dann in der `.htaccess` `Require all denied` durch
`Order allow,deny` und `Deny from all` ersetzen.

---

## 2. Was heute fertig geworden ist

**Die vier echten App-Screenshots sind eingebaut**, die gezeichnete Attrappe ist weg:

- Kopf der Seite: die Kachelwand der Sofort-Meldung im Telefonrahmen, Stempel bleibt.
- Abschnitt „Die Kette": ein Bild und der Absatz „Aus der Ziffer wird die Meldung."
- Reiter „Feld-App": Prüfliste und Objektansicht nebeneinander.

Geprüft mit Chrome: bei 1440 px und bei 390 px Telefonbreite, `scrollWidth` gleich
`clientWidth` (kein waagrechtes Scrollen), alle vier Bilder laden, HTML sauber verschachtelt.

**Texte und Zahlen:**

- Kontakt-Überschrift jetzt „30 Minuten, Ihr eigenes Objekt, Ihre eigenen Mängel."
  Die Seite argumentiert positiv; ein Vorwurf wird nicht verneint, sondern gar nicht erst
  aufgemacht.
- Zahlenwiderspruch behoben: 103 Prüfpunkte mit „64 Punkte" gegen 75 an anderer Stelle.
  Richtig sind **114** (75 + 39), in den Prüfplan-Vorlagen nachgezählt.
- Stand-Zeile im Kontaktkasten: App iOS 1.11, Android 0.48, Cockpit 1.60.
- Prüfstand-Kachel aus dem Cockpit-Reiter in den Abschnitt „Mitarbeiten" verschoben.
- „Angebot binnen 48 Stunden" → „Angebot innerhalb weniger Tage".

**Technik:**

- **HTTPS wird jetzt erzwungen.** Das Zertifikat ist geprüft: Sectigo OV, gültig bis
  06.03.2027, `https://rundok.de/` antwortet mit 200. Vorher war `http://` im Klartext
  erreichbar, obwohl die Datenschutzerklärung reines HTTPS zusagt. Jetzt stimmt der Satz.
- `.htaccess` sperrt `*.md`, `*.patch` und `/.git`.
- `fonts/OFL.txt` nachgelegt (Originaltext, Copyright „The Geist Project Authors"). Die
  Lizenz verlangt, dass er mit den Schriftdateien mitgeht; er fehlte.
- `legal.css`: tote Platzhalter-Klasse `.todo` entfernt. `sitemap.xml`: Datum nachgezogen.
- `index.html` auf Dateirechte 644 gesetzt — stand auf 600, was nach dem Upload einen
  403 auf die Startseite hätte geben können.

**Screenshots:** aufgenommen am 08.09. auf dem iPhone-Simulator mit Build 157 und dem
Demo-Projekt „BV Musterstraße". Ein eigener Prüflauf hat alle vier Bilder durchgesehen: kein
Kundenname, keine Firma, keine Adresse, keine E-Mail, kein Personenname, kein reales Objekt.

---

## 3. Was noch offen ist — hält den Upload nicht auf

1. **Drei Schönheitsfehler in den Bildern.** In `05-projekt.png` liegt das Etikett „S4" auf
   einer Wandlinie, und über dem Grundriss steht ein leerer grauer Block. In `01` und `03`
   läuft der Reiter „Betreiberpflichten Gew…" in den rechten Bildrand. Entschieden: bleibt
   erst einmal drin, lässt sich jederzeit durch eine neue Aufnahme ersetzen (Abschnitt 4
   sagt wie).
2. **Impressum, berufsrechtlicher Teil** (Kammer, Berufsbezeichnung, Haftpflicht) fehlt.
   Entschieden: so in Ordnung.
3. **Zugangsdaten im README.** IONOS-Vertragsnummer, SFTP-Server und Benutzername stehen in
   einer Datei, die im selben Ordner liegt wie die Website. Die `.htaccess` sperrt sie; besser
   aufgehoben wären sie im Passwortspeicher.
4. **Domäne:** `info@3DLaser.de` bleibt vorerst die Anbieteradresse, `tickets@wildmoser-ing.de`
   das Ticket-Postfach. Nichts zu tun.

---

## 4. Wenn die Seite später geändert wird

**Die eine Regel:** Auf dieser Seite steht nur, was die Software heute wirklich kann. Sie
wirbt gegenüber Kirchenstiftungen, Kommunen und Hausverwaltungen; eine Zusage, die im Piloten
nicht hält, kostet den Kunden. Zweite Regel: Der Kunde bekommt nie das Cockpit, sondern die
App und einzelne Blätter. Dritte Regel: `index.html` bleibt eine Datei mit inline CSS und JS,
ohne Framework, ohne CDN, ohne Analyse-Skript — sonst stimmt `datenschutz.html` nicht mehr.

**Wo die Wahrheit steht** (alles auf dem Rechner des Ingenieurbüros):

| Thema | Quelle |
|---|---|
| Cockpit, Chronik jeder Version | `begehung/BEDIENUNG.md`, `VERSIONS_LOG` in `begehung/index.html` |
| iPhone-App | `IBWBegehung/IBWBegehung/Ansichten/HilfeView.swift`, Module in `AppKonfig.swift` |
| Android-App | `IBWBegehungAndroid/BAUPLAN.md` |
| Kataloge und Kacheln | `begehung/meldekataloge.json` |
| Prüfpunkte | `begehung/pruefplaene/*.json` |
| Meldungstypen | `begehung/serve.py` (`TICKET_TITEL`) — nicht aus dem Katalog zählen |

Die Zahlen der Seite, am 08.09. nachgezählt: 12 Kataloge, 191 Meldekacheln, davon 164 mit
Rechtsgrundlage, 6 Meldungstypen, 114 Prüfpunkte (75 + 39). Beim nächsten Durchgang neu
zählen, nicht abschreiben.

**Neue Screenshots:** App für den Simulator bauen, dann
`xcrun simctl launch <UDID> de.wildmoser.IBWBegehung --demo-projekt --demo-pruefplan --demo-kamera`
und `xcrun simctl io <UDID> screenshot`. Wege durch die Oberfläche stehen als Testszenen in
`IBWBegehungUITests/DemoVideoTests.swift`. Achtung: Der Startbildschirm zeigt noch den alten
Namen „IBW Begehung", und der Projekt-Auswahldialog zeigt echte Projekte — beides darf nicht
auf die Seite. Der Simulator hat keine Kamera, im Foto-Schritt „Kein Foto möglich — ohne Foto
weiter" nehmen.

**Bildeinbau, falls jemand daran arbeitet:** Die Bildkarten sind `<figure>`-Elemente und
brauchen `margin:0` — der Browser gibt ihnen sonst 40 px Rand. Der Zuschnitt des Hero-Bildes
(`aspect-ratio:1206/2470`) liegt in einer leeren Zeile des Screenshots zwischen Bildzeile 2427
und 2474; jeder andere Wert schneidet Text waagrecht durch.
