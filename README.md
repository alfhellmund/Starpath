# Starpath — Website

Statische Webseite für die App **Starpath** (App Store): Datenschutzerklärung, Support-Kontakt, Impressum.

Gehostet via **GitHub Pages**: <https://alfhellmund.github.io/Starpath/>

## Repository

Dieses Repository enthält nur die Website.
Der Quellcode der App liegt getrennt davon und wird nicht veröffentlicht.
Jeder Push auf `main` veröffentlicht über `.github/workflows/pages.yml`.

## Seiten

- `index.html` — Startseite
- `privacy.html` — Sprachauswahl der Datenschutzerklärung (ohne Erklärungstext; erzeugt, nicht von Hand)
- `privacy-de.html` — Datenschutzerklärung Deutsch (maßgeblich, von Hand gepflegt)
- `privacy-<code>.html` — Datenschutzerklärung je weitere Sprache, beginnend mit `privacy-en.html` (erzeugt)
- `support.html` — Support-Kontakt + FAQ (DE + EN)
- `impressum.html` — Anbieterkennzeichnung (§ 5 DDG / § 18 MStV)
- `style.css` — Gestaltung, dazu die Klasse `.pruefen` für Entwurfsmarker

Deutsche Texte in der Sie-Form, englische neutral mit „you“.

## Änderungen an der Datenschutzerklärung

Ändert die App Berechtigungen, Speicherung oder Datenwege, wird `privacy-de.html` gegen den Code nachgezogen und Fassung und Stand im Kopf
der Seite und in der Fassungszeile erhöht. In der App verweist „Über“ → „Rechtliches“ auf die Datenschutzerklärung in der Sprache der App
(`LegalLinks.swift`).

Ablauf bei einer neuen Fassung (Werkzeug `Tools/privacy_l10n.py` im App-Repository):

1. `privacy-de.html` ändern, Fassung und Stand erhöhen.
2. `python3 Tools/privacy_l10n.py pruefen Website` meldet je Sprache die veralteten Einheiten (`data-quelle` weicht vom aktuellen deutschen Text ab).
3. Veraltete Einheiten nachübersetzen, die Seite mit `bauen` neu erzeugen, bis `pruefen` Exit 0 liefert und 0 veraltet meldet.
4. Marker-Suche (unten) leer, dann Push.

Regeln:

- Die Dateinamen `privacy-<code>.html` werden nicht umbenannt (App Store Connect, Privacy Policy URL nicht editierbar). `<code>` ist die Sprachkennung der App in Kleinbuchstaben (`pt-br`, `zh-hans`).
- Erst die Seite veröffentlichen, dann die Sprache in der App freischalten: Eine Sprache kommt erst in `LocaleHelper.supportedLanguages` und `CFBundleLocalizations`, wenn ihre `privacy-<code>.html` veröffentlicht ist.
- `privacy.html` entsteht nur über `python3 Tools/privacy_l10n.py bauen Website --nur-auswahl`.

Offene Punkte in einem Entwurf werden mit `<span class="pruefen">…</span>` markiert. Vor jedem Push
muss diese Suche leer sein:

```sh
grep -n 'class="pruefen"' *.html
```

## Lokal testen

```sh
cd Website
python3 -m http.server 8000
open http://localhost:8000
```
