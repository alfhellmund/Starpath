# Starpath — Website

Statische Webseite für die App **Starpath** (App Store): Datenschutzerklärung, Support-Kontakt, Impressum.

Hosting über **GitHub Pages**: <https://alfhellmund.github.io/Starpath/> — **noch nicht eingerichtet.**

## Repository

Dieser Ordner wird — wie bei BaroWatch (`~/Development/BaroWatch/Website/` =
`github.com/alfhellmund/BaroWatch`) — ein **eigenes Git-Repository, das nur die Website enthält**.
Ziel-Repository: `github.com/alfhellmund/Starpath` (enthält bisher nur `LICENSE`).
Das App-Repository bleibt davon getrennt; der Quellcode der App wird nicht veröffentlicht.

Noch nicht angelegt: `git init` und die Anbindung an das Ziel-Repository macht die
Projektleitung nach Freigabe. Für die Veröffentlichung wie bei BaroWatch zusätzlich
`.github/workflows/pages.yml` (Actions `configure-pages`, `upload-pages-artifact`, `deploy-pages`)
übernehmen; `.nojekyll` liegt schon bereit.

## Seiten

- `index.html` — Startseite
- `privacy.html` — Datenschutzerklärung (DE + EN, deutsche Fassung maßgeblich), Fassung 1.0, Stand 2026-10-26
- `support.html` — Support-Kontakt + FAQ (DE + EN)
- `impressum.html` — Anbieterkennzeichnung (§ 5 DDG / § 18 MStV)
- `style.css` — aus der BaroWatch-Website übernommen, ergänzt um die Klasse `.pruefen`

Deutsche Texte in der Sie-Form (wie BaroWatch), englische neutral mit „you“.

## Vor der Veröffentlichung

1. Alle Entwurfsmarker abarbeiten und entfernen:
   ```sh
   grep -n 'class="pruefen"' *.html
   ```
   Die Ausgabe muss leer sein.
2. Datenschutzerklärung gegen den dann aktuellen App-Stand prüfen. Abschnitt 3 beschreibt den
   Code-Stand vom 2026-10-26; der iCloud-Abgleich ist darin bereits als entfernt angenommen.
   Kommt das Lesen der BaroWatch-Druckwerte über eine App-Gruppe hinzu, braucht Abschnitt 3.2
   einen Nachtrag.
3. Link zur Datenschutzerklärung in der App und in App Store Connect eintragen
   (App Store Review Guideline 5.1.1(i)).

## Lokal testen

```sh
cd Website
python3 -m http.server 8000
open http://localhost:8000
```
