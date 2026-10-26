# Starpath — Website

Statische Webseite für die App **Starpath** (App Store): Datenschutzerklärung, Support-Kontakt, Impressum.

Gehostet via **GitHub Pages**: <https://alfhellmund.github.io/Starpath/>

## Repository

Dieses Repository enthält nur die Website — wie bei BaroWatch (`github.com/alfhellmund/BaroWatch`).
Der Quellcode der App liegt getrennt davon und wird nicht veröffentlicht.
Jeder Push auf `main` veröffentlicht über `.github/workflows/pages.yml`.

## Seiten

- `index.html` — Startseite
- `privacy.html` — Datenschutzerklärung (DE + EN, deutsche Fassung maßgeblich)
- `support.html` — Support-Kontakt + FAQ (DE + EN)
- `impressum.html` — Anbieterkennzeichnung (§ 5 DDG / § 18 MStV)
- `style.css` — aus der BaroWatch-Website übernommen, ergänzt um die Klasse `.pruefen`

Deutsche Texte in der Sie-Form, englische neutral mit „you“.

## Änderungen an der Datenschutzerklärung

Ändert die App Berechtigungen, Speicherung oder Datenwege (z. B. das Lesen der BaroWatch-Druckwerte
über eine App-Gruppe), wird `privacy.html` gegen den Code nachgezogen und Fassung und Stand im Kopf
der Seite erhöht. In der App verweist „Über“ → „Rechtliches“ auf diese Seite (`LegalLinks.swift`).

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
