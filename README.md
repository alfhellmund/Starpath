# Starpath — Website

Statische Webseite für die App **Starpath** (App Store): Datenschutzerklärung, Support-Kontakt, Impressum.

Gehostet via **GitHub Pages**: <https://alfhellmund.github.io/Starpath/>

## Repository

Dieses Repository enthält nur die Website.
Der Quellcode der App liegt getrennt davon und wird nicht veröffentlicht.
Jeder Push auf `main` veröffentlicht über `.github/workflows/pages.yml`.

## Seiten

Jeder Seitentyp hat eine deutsche Quelle (von Hand gepflegt), Sprachfassungen (erzeugt) und eine Sprachauswahl (erzeugt, nicht von Hand):

| Typ | Quelle | Sprachfassungen | Sprachauswahl |
|---|---|---|---|
| Startseite | `index-de.html` | `index-<code>.html`, beginnend mit `index-en.html` | `index.html` |
| Support | `support-de.html` | `support-<code>.html`, beginnend mit `support-en.html` | `support.html` (mit Kontaktadresse) |
| Datenschutzerklärung | `privacy-de.html` | `privacy-<code>.html`, beginnend mit `privacy-en.html` | `privacy.html` |
| Impressum | `impressum.html` (maßgeblich) | `impressum-en.html` (Übersetzung) | keine |

- `style.css` — Gestaltung, dazu die Klasse `.pruefen` für Entwurfsmarker; erzeugt aus `Tools/website_style.css` im App-Repository (nicht von Hand ändern)

Deutsche Texte in der Sie-Form, englische neutral mit „you“.

## Änderungen an den Seiten

**Gestaltung:** Die eine Quelle von `style.css` ist `Tools/website_style.css` im App-Repository, gemeinsam mit der Website von BaroWatch. Geändert wird nur die Quelle; jedes `bauen` (auch `--nur-auswahl`) schreibt `style.css` daraus, und `pruefen` meldet jede Abweichung (Prüfpunkt r).

**Datenschutzerklärung:** Ändert die App Berechtigungen, Speicherung oder Datenwege, wird `privacy-de.html` gegen den Code nachgezogen und Fassung und Stand im Kopf
der Seite und in der Fassungszeile erhöht. In der App verweist „Über“ → „Rechtliches“ auf die Datenschutzerklärung in der Sprache der App
(`LegalLinks.swift`).

Ablauf bei einer neuen Fassung einer deutschen Quelle (Werkzeug `Tools/website_l10n.py` im App-Repository):

1. Die deutsche Quelle ändern (bei `privacy-de.html` zusätzlich Fassung und Stand erhöhen).
2. `python3 Tools/website_l10n.py pruefen Website` meldet je Datei und Typ die veralteten Einheiten (`data-quelle` weicht vom aktuellen deutschen Text ab).
3. Veraltete Einheiten nachübersetzen, die Seiten mit `bauen` neu erzeugen (`bauen` baut alle Typen einer Sprache und schreibt die Auswahlen neu), bis `pruefen` Exit 0 liefert und 0 veraltet meldet.
4. Marker-Suche (unten) leer, dann Push.

Regeln:

- Die Dateinamen `index-<code>.html`, `support-<code>.html` und `privacy-<code>.html` werden nicht umbenannt (App Store Connect: Privacy Policy URL und Support URL sind nicht editierbar). `<code>` ist die Sprachkennung der App in Kleinbuchstaben (`pt-br`, `zh-hans`). Dasselbe gilt für `index.html`, `support.html`, `privacy.html`, `impressum.html` und `impressum-en.html`.
- Erst die Seiten veröffentlichen, dann die Sprache in der App freischalten: Eine Sprache kommt erst in `LocaleHelper.supportedLanguages` und `CFBundleLocalizations`, wenn ihre `privacy-<code>.html` (bei einer Einreichung mit lokalisierter Support- und Marketing-URL auch `support-<code>.html` und `index-<code>.html`) veröffentlicht ist.
- Die Sprachauswahlen (`index.html`, `support.html`, `privacy.html`) entstehen nur über `python3 Tools/website_l10n.py bauen Website --nur-auswahl`.
- Das Impressum gibt es deutsch (`impressum.html`, maßgeblich) und englisch (`impressum-en.html`); die Fußzeilen der übrigen Sprachen verweisen auf die englische Fassung mit dem Zusatz „(English)“.

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
