# Auftrag: rundok.de fertig bauen

Stand 08.09.2026 · Ingenieurbüro Wildmoser · Grundlage: Abgleich der Website gegen den
echten Funktionsstand (Cockpit v1.60, iPhone-App Build 156, Android v0.48), geprüft im
Quelltext, nicht aus Erinnerung. Dieses Blatt ist die Arbeitsanweisung für den nächsten
Bau-Durchgang. Alles, was hier unter „erledigt“ steht, ist bereits in `index.html`.

---

## 0. Die eine Regel

**Auf dieser Seite steht nur, was die Software heute wirklich kann.** Sie wirbt gegenüber
Kirchenstiftungen, Kommunen und Hausverwaltungen. Eine Zusage, die im Piloten nicht hält,
kostet den Kunden. Wer eine Funktion ergänzen will, belegt sie vorher im Code, im Handbuch
(`BEDIENUNG.md`) oder in der Versionsliste des Cockpits (`VERSIONS_LOG` in `index.html`).
Im Zweifel weglassen.

Zweite Regel: **Der Kunde bekommt nie das Cockpit.** Er bekommt die App und Blätter. Keine
Formulierung darf klingen, als bediene er die Zentrale selbst.

---

## 1. Erledigt (Commits 44d25c6, 947dc7a)

### 1.1 Korrigierte Fehlaussagen (16)

| Was stand da | Warum falsch | Jetzt |
|---|---|---|
| „Kein Hosting, keine US-Cloud“ (Hero) und „Keine US-Cloud …“ (Datenhoheit) | Alle KI-Funktionen rufen einen US-Anbieter ohne zugesicherte EU-Region auf | „Kein Portal, kein Fremd-Hosting“ + neue Kachel „Wo KI mitläuft und wo nicht“ |
| Kontrollgang-Quittung: „wann, wo (GPS), **durch wen**“ | Es wird keine Person gespeichert | „wann, wo, wie viele Befunde, auf Wunsch mit Kommentar“ |
| „Personen werden **automatisch** verpixelt“ | Knopf je Foto, keine Automatik | „je Foto auf Knopfdruck, Original bleibt gesichert“ |
| „Kontakte, **Leads**, Stammliste … alles lokal“ | Lead-Tafel ist IBWs eigene Vertriebsakte; die Foto-Erkennung läuft extern | „Kontakte und Stammliste“, Hinweis auf den externen Dienst |
| „Nachweis-Paket: Monats- oder Jahresbericht“ | Als Programmfunktion nicht vorhanden | Als **Leistung der Zentrale** gekennzeichnet |
| „Berichte … dann trägt **der Bericht** den Stempel“ | Stempel und Briefkopf gibt es bei der SiGe-Aktennotiz | präzisiert auf die Aktennotiz |
| „Jede Fassung ist nummeriert“ | Nummeriert wird nur die Aktennotiz | präzisiert |
| „welcher **Rechtstext**, das steckt in der Kachel“ | Das Feld ist redaktionell, keine App zeigt es | „Die Rechtsgrundlage steht am Prüfpunkt und im Bericht“ |
| Termin-Agent „… oder **Mail an die Feld-App**“ | Es geht keine Mail an die App | „Aufträge reisen mit dem Projekt auf die Geräte“ |
| Austausch „(iCloud, **OneDrive**, Google Drive)“ | Der Android-Ordnerwähler zeigt OneDrive nicht an | „iCloud für iPhone, Google Drive für Android“ |
| „Zustandsblatt **je Raum**“ | Es ist die Matrix Prüfpunkte × Begehungen | „jeder Prüfpunkt über alle Begehungen“ |
| „Mangel, **Hinweis** oder Empfehlung, mit Dringlichkeit“ | Die Stufe heißt **Info**; dringlich gibt es nur am Mangel | korrigiert |
| „LiDAR und AR nur iPhone **Pro**“ | AR läuft auf jedem aktuellen iPhone | „Messfoto und Raum-Scan nur iPhone mit LiDAR“ |
| Sechs Funktionen ohne Gerätehinweis | Gibt es nur auf dem iPhone | Hinweis gesetzt (Sprachbefehl, Verorten im Panorama, Sensorik, Anlagen, Visitenkarten) |
| „Prüfplan mit **64** Punkten“ | Sind 75 | korrigiert |
| „60 bis 90 Sekunden je Meldung“ (2×) | Nirgends gemessen | „gut eine Minute“ als Erfahrungswert |

### 1.2 Ergänzte Kacheln (13)

Feld-App: **Prüfliste zum Abhaken**, **Pläne und Plan-Pin**, **Rückweg mit einem Tipp**,
**Versand-Nachweis**. Cockpit: **Alle Objekte auf einem Schirm**, **Zustandsblatt über die
Jahre**. Berichte: **Amtliche Baucheckliste der Erzdiözese**, **Zustandsbericht mit
Vorjahresvergleich**. Kataloge: **Ein Prüfplan, mehrere Sichten**, **Alte Runden bleiben
alt**. Datenhoheit: **Kein Datenbank-Gefängnis**, **Wo KI mitläuft und wo nicht**,
**Ortsdaten: eng gefasst**.

### 1.3 Neuer Abschnitt „Mitarbeiten“ (`#mitarbeiten`)

Überschrift „Sie bekommen kein Programm, sondern ein Blatt.“ Vier Karten: Befunde prüfen,
Pläne nachlegen, Freimelden ohne Zugang, Berichte im Word korrigieren. Alle vier Wege
existieren heute. Konzept dahinter: `begehung/KONZEPT-Service-Blaetter.md`.

---

## 2. Offen — bitte im nächsten Durchgang erledigen

### 2.1 Screenshots statt Attrappe (Hauptpunkt)

Im Hero steht heute eine gezeichnete Telefon-Attrappe mit sechs Kacheln. Die Kacheln gibt
es einzeln wirklich, in dieser Zusammenstellung aber in keinem Katalog. **Ersetzen durch
echte Screenshots** aus `screens/` (siehe Abschnitt 3). Vorschlag:

- **Hero:** `screens/01-kacheln.png` im Telefonrahmen, statt der gezeichneten Kacheln.
- **Reiter Feld-App:** kleine Bildstreifen über den Kacheln — `02-pruefliste.png` und
  `05-projekt.png`.
- **Abschnitt „Die Kette“:** `03-meldung.png` neben Schritt 1 bis 3.

Bildregeln: dunkler Rahmen wie die Karten, `max-width:100%`, `loading="lazy"`, `alt`-Text
beschreibend („Kachelwand der Sofort-Meldung mit 18 Symptom-Kacheln“). Keine Schatten
über die Kartenkante hinaus. Die Bilder sind 1206 × 2622 Pixel; auf der Seite auf 300 bis
420 Pixel Breite einbinden, damit nichts flimmert.

### 2.2 Drei Entscheidungen von Bernd

1. **Name und Domain.** Im Repo steht durchgehend `rundok.de`, das Logo ist RUN + DOK.
   Bernd spricht von „run-dog.de“. Solange das nicht entschieden ist: nichts umbenennen.
   Fällt die Entscheidung auf Run-Dog, sind Domain, Logo-SVGs, `.htaccess`, `README.md`,
   `sitemap.xml`, Impressum und alle Fließtexte anzupassen.
2. **„Angebot binnen 48 Stunden“** im Preisteil ist eine Selbstverpflichtung ohne
   Vorbehalt. Entweder halten wollen oder auf „innerhalb weniger Tage“ ändern.
3. **Prüfstand-Kachel** steht im Reiter „Cockpit“, obwohl der Kunde dort klickt. Seit es
   den Abschnitt „Mitarbeiten“ gibt, gehört sie inhaltlich dorthin (im Cockpit-Reiter kann
   ein Satz stehen bleiben: „Das Blatt dafür erzeugt die Zentrale“).

### 2.3 Kleinigkeiten

- `README.md`: USt-IdNr. im Impressum ist als offen vermerkt — prüfen, ob erledigt.
- Nach dem Einbau der Screenshots die Zeile „Echte App-Screenshots statt der
  Kachel-Attrappe im Hero“ aus der Offen-Liste des README streichen.
- `sitemap.xml` um den neuen Abschnitt nicht erweitern (Anker, keine eigene Seite).

---

## 3. Screenshots: was geliefert wird

Ordner `screens/` im Repo. Aufgenommen auf dem iPhone-Simulator (iPhone 17 Pro, iOS 26.5)
mit dem **Demo-Projekt „BV Musterstraße“** (Start der App mit `--demo-projekt
--demo-pruefplan`) — erfundene Daten, kein Kundenname, keine echten Objekte, keine echten
Firmen, keine Personen auf Fotos. Statusleiste auf 09:41 gesetzt, voller Akku, kein
Netzbetreibername. Der Prüfplan heißt dort „Demo Zustandsabfrage“, das Gebäude „Demohaus“.

| Datei | Zeigt | Verwendung |
|---|---|---|
| `01-kacheln.png` | Kachelwand der Sofort-Meldung: 18 Symptom-Kacheln des SiGeKo-Katalogs, darüber die Reiter der hinterlegten Kataloge, darunter Frist, Schalter „dringlich“ und „wird Ticket“ | **Hero statt Attrappe** |
| `02-pruefliste.png` | Prüfliste am Objekt: Prüfpunkt mit Hinweis, Schadensziffern 0 bis 4 in Ampelfarben, Fortschritt „0 / 2“ | Reiter Feld-App, Kachel „Prüfliste zum Abhaken“ |
| `03-meldung.png` | Die Kette in einem Bild: aus Ziffer 2 wird die Meldung — Kachel vorgewählt, Frist 14 Tage mit Datum, Text „Prüfpunkt A1 … Schadensziffer 2“ schon eingetragen | Abschnitt „Die Kette“, Schritt 1–3 |
| `05-projekt.png` | Projektübersicht: Grundriss mit Standpunkten, darunter Prüfliste, Rundgang, Sofort-Meldung | frei verwendbar |

Eine Ticketliste ist **nicht** dabei: Das Demo-Projekt hat keine Tickets, und eine leere Liste
taugt nicht als Werbebild. Wer sie braucht, sendet im Simulator einmal eine Meldung und
fotografiert die Liste danach.

Werden Screenshots neu gebraucht: App für den Simulator bauen, dann
`xcrun simctl launch <UDID> de.wildmoser.IBWBegehung --demo-projekt --demo-pruefplan` und
`xcrun simctl io <UDID> screenshot`. Die Wege durch die Oberfläche stehen als Testszenen in
`IBWBegehungUITests/DemoVideoTests.swift`; `werkzeuge/demovideos.sh` setzt den Simulator auf
(Statusleiste, Rechte). Achtung: Der Simulator hat keine Kamera — im Foto-Schritt „Kein Foto
möglich — ohne Foto weiter“ nehmen.

---

## 4. Belegte Funktionen als Nachschlagewerk

Wer Text ändert, prüft hier: **Cockpit** `~/Documents/Claude/Projects/begehung` —
`BEDIENUNG.md` (Handbuch), `VERSIONS_LOG` in `index.html` (Chronik jeder Version),
`serve.py` (Endpunkte). **iPhone** `~/Entwicklung/IBWBegehung` — `HilfeView.swift`
beschreibt jede Funktion in Bernds Worten, `AppKonfig.swift` listet die freischaltbaren
Module. **Android** `~/Entwicklung/IBWBegehungAndroid` — `BAUPLAN.md`, `HilfeView.kt`.
Konzepte und Strategie: Obsidian-Vault, „02 Projekte/Begehung & Bauverfolgung“ und
„02 Projekte/Strategie & Vertrieb“.

Häufige Stolperstellen aus dem Abgleich:

- Was auf dem iPhone läuft, läuft nicht automatisch auf Android. Der Gleichschritt ist die
  Ausnahme, nicht die Regel — immer beide Repos prüfen.
- „KI“ nur schreiben, wo wirklich ein Sprachmodell arbeitet: Bericht veredeln, Plankopf,
  Typenschild, Zeitstand-Vergleich, Firmenliste aus Foto. Alles andere sind Listen und Regeln.
- Rechtsgrundlagen gehören an den Prüfpunkt und in den Bericht, nicht an die Kachel.
- Fristen, Kataloge und Prüfpläne ändern sich. Zahlen auf der Seite (Punkte, Kacheln,
  Kataloge) beim nächsten Durchgang nachzählen, nicht abschreiben.
