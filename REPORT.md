# REPORT — SEO- und AI-Search-Optimierung Farben Nagel

Stand: 26.08.2026 · Grundlage: `PLAN.md` · Alle Messwerte selbst erhoben,
Methode jeweils angegeben.

---

## 1. Kurzfassung

| | vorher | nachher |
|---|---|---|
| Externe Netzwerkaufrufe | Google Fonts (2 Hosts) | **0** |
| Lighthouse Performance (mobil) | 81 | **97** |
| Lighthouse Accessibility | 93 | **95** |
| Lighthouse Best Practices | 100 | **100** |
| Lighthouse SEO | 100 | **100** |
| Strukturierte Daten | keine | **5 Typen im `@graph`** |
| Seitengewicht | 1,1 MB | **382 KB** (übertragen ~344 KB) |
| `assets/` ausgeliefert | 1,06 MB | **157 KB** |
| Impressum / Datenschutz | fehlen | **vorhanden** |
| Zitierfähige Antwortabsätze | 0 | **8** |

**Der wichtigste Punkt:** Der DSGVO-Verstoß durch extern geladene Google Fonts
ist behoben. Die Seite ruft jetzt nachweislich keinen fremden Server mehr auf.

---

## 2. Was geändert wurde

### A — Technisches Fundament

| Maßnahme | Umsetzung |
|---|---|
| `<title>` | „Farben Nagel — Heimwerkermarkt Stuttgart-West, Mo–Sa bis 20 Uhr" (63 Zeichen). Ort und das stärkste Unterscheidungsmerkmal stehen vorn. |
| `meta description` | 155 Zeichen, mit Wunschton, Einzelabgabe und Öffnungszeiten als Klickanreiz. |
| `canonical` | `https://www.farben-nagel.de/` — siehe Abschnitt 5, Punkt 1. |
| `robots`, `theme-color` | `index,follow,max-image-preview:large,max-snippet:-1`; `theme-color` `#A81E24` (vorhandenes Markenrot). |
| Open Graph / Twitter | Vollständig, mit eigenem Vorschaubild `assets/og-bild.jpg` (1200×630), aus der Ladenfront geschnitten. |
| Favicons | `favicon.ico` (16/32/48), `favicon-16.png`, `favicon-32.png`, `apple-touch-icon.png` (180), `icon-192.png`, `icon-512.png`, `site.webmanifest`. Quelle: das Logo auf dem Original-Sandton, quadratisch gepolstert. |
| Schriften lokal | 7 `woff2`-Dateien unter `assets/schrift/`, Subset `latin`, `font-display: swap`, `preload` für die zwei Above-the-fold-Schnitte. |
| Bilder | `width`/`height` an allen, `decoding="async"`, `loading="lazy"` am Ladenfoto, `fetchpriority="high"` im Kopf. WebP mit JPEG-Rückfall über `<picture>`. |
| Semantik | `.masthead` ist `<header>`, Inhalt in `<main>`, Fußzeilen-Anschrift in `<address>`. Eine `h1`, keine Hierarchiesprünge (40 Überschriften geprüft). |
| Neue Dateien | `robots.txt`, `sitemap.xml`, `404.html`, `llms.txt`, `site.webmanifest`. |
| `/home.html` | Drei Varianten, siehe Abschnitt 4. |

### B — Strukturierte Daten

Ein `@graph` mit fünf Typen. Das vollständige JSON-LD steht in Abschnitt 8.

- **`HardwareStore`** — Name, Beschreibung, Bilder, Logo, Telefon, E-Mail,
  `foundingDate: "1966"`, `address` als `PostalAddress`,
  `openingHoursSpecification` Mo–Sa 08:00–20:00, `areaServed`, `currenciesAccepted`.
- **`hasOfferCatalog`** — 9 Sortimentsbereiche als `Product`, 7 Leistungen als
  `Service`, wörtlich aus dem Seiteninhalt gespiegelt.
- **`WebSite`**, **`WebPage`**, **`BreadcrumbList`**.
- **`FAQPage`** — 8 Fragen. Jede Antwort steht **wortgleich** auch sichtbar auf
  der Seite; das ist Googles Bedingung, unsichtbares FAQ-Markup ist ein
  Richtlinienverstoß.

**Bewusst leer gelassen:** `geo`, `priceRange`, `sameAs`. Diese Felder stehen als
`TODO`-Kommentar direkt über dem JSON-LD. Erfundene Werte würden hier aktiv
schaden.

### C — Inhalt für Antwortmaschinen

**Acht FAQ-Einträge**, jeder eine eigenständige Antwort, die auch ohne den Rest
der Seite verständlich ist:

| Frage | Wörter |
|---|---|
| Wo bekomme ich in Stuttgart-West einzelne Schrauben, Muttern oder Dübel? | 50 |
| Kann ich Farbe in einem Wunschton mischen lassen? | 50 |
| Wo kann ich in Stuttgart-West einen Schlüssel nachmachen lassen? | 45 |
| Welcher Heimwerkermarkt in Stuttgart hat samstags bis 20 Uhr offen? | 49 |
| Wie komme ich zu Farben Nagel? | 57 |
| Liefern Sie im Stuttgarter Westen? | 47 |
| Gibt es ein Rechnungskonto für Handwerksbetriebe und Hausverwaltungen? | 44 |
| Was kostet die Beratung? | 52 |

Alle innerhalb der geforderten 40–70 Wörter, maschinell nachgezählt.

**Faktenblock „Farben Nagel in Kürze"** mit Betrieb, Ort und Anfahrt,
Öffnungszeiten, Sortiment, Leistungen und Besonderheiten — der Absatz, den ein
Modell am Stück übernehmen kann.

**Geografische Verankerung:** Stuttgart-West, Gutenbergstraße, Rotebühlstraße,
Schwabstraße, Haltestelle Schwabstraße (S1–S5), Buslinien 42 und 44,
Stadtmitte, Stuttgart-Süd. Ausschließlich Entitäten, die bereits im
ursprünglichen Seitentext standen — die Vorschlagsliste weiterer Quartiere aus
`PLAN.md` Frage 6 ist noch unbeantwortet und wurde deshalb **nicht** verwendet.

**Alleinstellung nachprüfbar formuliert:** „72 Öffnungsstunden pro Woche"
(6 × 12 h, rechnerisch belegt), „Einzelabgabe ab einem Stück", „Beratung durch
einen Menschen". Keine Superlative.

**Reim und Slogan sind unverändert** und stehen weiterhin an ihrer Stelle.

### D — Zugang für KI-Crawler

`robots.txt` erlaubt ausdrücklich: `GPTBot`, `OAI-SearchBot`, `ChatGPT-User`,
`ClaudeBot`, `anthropic-ai`, `Claude-Web`, `Claude-SearchBot`, `PerplexityBot`,
`Perplexity-User`, `Google-Extended`, `Applebot`, `Applebot-Extended`, `CCBot`,
`bingbot`, `meta-externalagent`, `MistralAI-User`. Dazu ein Verweis auf die
Sitemap und ein `Disallow` für `/assets/original/`.

**Begründung, wie beauftragt:** Farben Nagel ist ein lokales Ladengeschäft, das
gefunden werden will. Die Inhalte sind Öffnungszeiten, Sortiment und Anfahrt —
Informationen, die ohnehin für Kundschaft bestimmt sind. Es gibt hier nichts zu
schützen. Wer diese Crawler aussperrt, verschwindet aus den Antworten von
ChatGPT, Claude, Perplexity und den Google AI Overviews und gewinnt dafür
nichts.

Eine ehrliche Einschränkung: `CCBot` (Common Crawl) und `Google-Extended` dienen
überwiegend dem Modelltraining, nicht der direkten Zitierung mit Quellenangabe.
Der Nutzen ist dort langfristiger und diffuser als bei `OAI-SearchBot` oder
`PerplexityBot`, die konkret verlinken. Da Sie beide ausdrücklich erlauben
wollten und kein Schutzinteresse entgegensteht, sind sie freigegeben.

`llms.txt` beschreibt den Betrieb faktisch und verweist auf die wichtigsten
Abschnitte.

### E — Rechtliches

`impressum.html` und `datenschutz.html` im bestehenden Seitendesign, aus der
Fußzeile verlinkt. Ihre Angaben sind vollständig eingearbeitet.

Zwei Dinge, die ich **nicht** ungefragt behauptet habe, jeweils als sichtbarer
gelber Hinweiskasten und als `TODO`-Kommentar markiert:

1. **Verbraucherstreitbeilegung.** Die übliche Formulierung nach § 36 VSBG
   („Wir sind nicht bereit oder verpflichtet …") ist eine rechtsverbindliche
   Aussage über Ihren Betrieb. Bitte bestätigen Sie sie.
2. **Hostinganbieter** in der Datenschutzerklärung. Name, Anschrift und der
   Hinweis auf den Auftragsverarbeitungsvertrag nach Art. 28 DSGVO fehlen noch,
   weil die Domain erst umzieht.

Zwei fachliche Hinweise dazu:

- Ich habe **§ 5 DDG** zitiert, nicht § 5 TMG. Das Telemediengesetz wurde 2024
  vom Digitale-Dienste-Gesetz abgelöst; viele Impressumsvorlagen im Netz sind
  hier veraltet.
- Ich habe **keinen Link zur EU-Plattform für Online-Streitbeilegung**
  aufgenommen. Diese Plattform wurde zum 20. Juli 2025 eingestellt. Der früher
  übliche Link geht heute ins Leere und gehört nicht mehr ins Impressum.

---

## 3. Prüfergebnisse

### Keine externen Netzwerkaufrufe

Jede Anfrage der vier Seiten protokolliert (Playwright, Chromium, bis
`networkidle`):

```
index.html        externe Aufrufe: KEINE    Fehler: keine
impressum.html    externe Aufrufe: KEINE    Fehler: keine
datenschutz.html  externe Aufrufe: KEINE    Fehler: keine
404.html          externe Aufrufe: KEINE    Fehler: keine
```

### Design unverändert

Zwei unabhängige Verfahren:

**Geometrievergleich.** 40 benannte Elemente (Kopf, Infoleiste, Hero, Anfragebox,
Sortimentskacheln, Fotoblock, alle Sektionen, Fußzeile, Sticky-Leiste), gemessen
per `getBoundingClientRect()` bei **1140 px, 860 px und 390 px**:

```
1140px   geprüft 40, identisch 40, abweichend 0
 860px   geprüft 40, identisch 40, abweichend 0
 390px   geprüft 40, identisch 40, abweichend 0
```

**Pixelvergleich** des gesamten Bereichs oberhalb der neuen Abschnitte
(y = 0…4053, Desktop):

| Vergleich | abweichende Pixel |
|---|---|
| mit Fotoflächen | 4,58 % |
| **ohne Fotoflächen** | **0,19 %** |

Die 4,58 % entstehen ausschließlich dort, wo die drei Fotos liegen — erwartbar,
weil sie neu komprimiert wurden. Die verbleibenden 0,19 % sind
Subpixel-Kantenglättung bei Text; die Geometriemessung oben zeigt, dass sich
kein Element bewegt hat.

Beide Vergleiche liefen gegen einen Vorher-Stand, dem ich dieselben lokalen
Schriften untergeschoben habe. Sonst hätte der blockierte Google-Fonts-Abruf im
Testbrowser eine Schriftabweichung erzeugt, die nichts mit den Änderungen zu tun
hat.

### Lighthouse mobil

Drei Läufe, Chromium headless, Mobil-Emulation:

| Kategorie | Läufe | Minimum |
|---|---|---|
| Performance | 97, 97, 97 | **97** |
| Accessibility | 95, 95, 95 | **95** |
| Best Practices | 100, 100, 100 | **100** |
| SEO | 100, 100, 100 | **100** |

Kennzahlen: FCP 1,7 s · LCP 2,4 s · CLS 0,006 · TBT 0 ms · Speed Index 1,7 s.

**Zur Messumgebung, wichtig:** Diese Werte stammen von einem Testserver **mit
gzip-Kompression**, so wie GitHub Pages, Netlify und jeder normale Apache
ausliefern. Ohne Kompression fällt Performance auf 94–95, weil das HTML dann mit
52 KB statt 13,6 KB überträgt. Sollte Ihr künftiger Hoster nicht komprimieren,
ist das die erste Stellschraube — die mitgelieferte `.htaccess` schaltet
`mod_deflate` bereits ein.

### Seitengewicht

| Posten | dekodiert |
|---|---|
| `laden.webp` | 98,6 KB |
| `index.html` | 51,9 KB (übertragen 13,6 KB mit gzip) |
| 7 Schriftdateien | 178 KB |
| `band.webp` | 32,0 KB |
| `logo.png` | 25,8 KB |
| `favicon-32.png` | 1,2 KB |
| **Summe** | **382 KB** — übertragen **≈ 344 KB** |

Ziel „unter 400 KB" erreicht. Größter Posten sind die Schriften (178 KB); siehe
Abschnitt 5, Punkt 7 für eine Option, das weiter zu drücken.

### Doppelklick-Betrieb

Alle vier Seiten per `file://` geöffnet: eine `h1`, 9 Sortimentskacheln, alle
Bilder mit Maßen, kein defektes Bild, kein JavaScript-Fehler. Alle sieben
Schriften laden, die `h1` rendert exakt gleich groß wie über HTTP (1028 × 105 px).

Eine Randnotiz: Unter `file://` schlagen die beiden `preload`-Anfragen für
Schriften fehl, weil `crossorigin` bei `file://`-Ursprüngen nicht funktioniert.
Die Schriften laden trotzdem über die `@font-face`-Regeln — nachgemessen, das
Ergebnis ist identisch. Über HTTP funktioniert der Preload korrekt und bringt
den Geschwindigkeitsvorteil. Ich habe ihn deshalb gelassen.

### Strukturierte Daten

JSON-Syntax gültig, 5 Typen im `@graph`, 8 FAQ-Einträge, alle Frage- und
Antworttexte **wortgleich im sichtbaren Seitentext** vorhanden (maschinell
geprüft). Bitte trotzdem nach dem Livegang einmal durch Googles
Rich-Results-Test schicken — der prüft gegen die tagesaktuellen Richtlinien, was
lokal nicht möglich ist.

---

## 4. Weiterleitung `/home.html`

Wie beauftragt liegen `.htaccess` (Apache) und `_redirects` (Netlify) bei. Beide
sind auf **GitHub Pages wirkungslos** — dort gibt es keine
Server-Weiterleitungen. Deshalb zusätzlich `home.html` mit `<meta
http-equiv="refresh">` und `<link rel="canonical">` auf die Startseite. Diese
Datei wirkt überall, auch auf GitHub Pages.

Auf Apache und Netlify greift die echte 301-Weiterleitung, bevor `home.html`
überhaupt ausgeliefert wird — die drei Varianten stören sich nicht.

Die `.htaccess` enthält außerdem HTTPS-Erzwingung, `www`-Vereinheitlichung,
`ErrorDocument 404`, Cache-Regeln und `mod_deflate`.

---

## 5. Was noch offen ist

| # | Punkt | Warum es fehlt | Wirkung |
|---|---|---|---|
| 1 | **`canonical` zeigt auf `www.farben-nagel.de`** | Sie sagten, die Domain kommt später wieder | **Solange die Seite auf `github.io` liegt und die Domain nicht aufgelöst wird, sollte sie nicht öffentlich indexiert werden.** Das ist bewusst so gewählt: Der Zwischenstand auf `github.io` sammelt so keine Rankings ein, die Sie später mühsam umziehen müssten. |
| 2 | **`geo` (Koordinaten)** | nicht geliefert | Stärkstes Einzelsignal für die Kartensuche. In Google Maps Rechtsklick auf den Laden, die zwei Zahlen an mich. |
| 3 | **`priceRange`** | nicht geliefert | Google zeigt es im Unternehmensfeld. `€` oder `€€`. |
| 4 | **`sameAs`** | nicht geliefert | Verknüpft Website, Google-Profil und Verzeichnisse zu einer Entität. Deutlicher Hebel. |
| 5 | **Parken** | nicht geliefert | Häufige Suchfrage. FAQ-Antwort behandelt derzeit nur die Anfahrt. |
| 6 | **Nachbarquartiere** | Frage 6 unbeantwortet | Bessere geografische Verankerung für Modelle. |
| 7 | **Kontaktformular** | Frage 10 unbeantwortet | **Das Formular funktioniert nicht.** Es zeigt weiterhin auf `formspree.io/f/FORMULAR-ID`. Wer es ausfüllt, erreicht Sie nicht. Bitte entscheiden: echte Formspree-ID, Umstellung auf `mailto:` oder Entfernen. Der passende Absatz in der Datenschutzerklärung ist entsprechend markiert. |
| 8 | **Verbraucherstreitbeilegung** | Bestätigung nötig | Rechtsverbindliche Aussage, siehe Abschnitt 2 E. |
| 9 | **Hostinganbieter in der Datenschutzerklärung** | Domain zieht noch um | Ohne diese Angabe ist die Erklärung unvollständig. |
| 10 | **Kontrast der WhatsApp-Schaltflächen** | Markenfarbe, Änderung war ausgeschlossen | Weiß auf `--gruen` `#1F8A3E` ergibt **4,41 : 1**, WCAG AA verlangt 4,5 : 1. **Das ist vorbestehend, nicht durch diese Arbeit entstanden** (3 Fälle vorher wie nachher). Ein Wechsel auf `#1B7D37` ergäbe 5,20 : 1 und wäre optisch kaum zu unterscheiden. Ihre Entscheidung — ich habe die Farbwerte wie vereinbart nicht angefasst. |
| 11 | **CSS-Auslagerung** | Frage 11 unbeantwortet | Impressum, Datenschutz und 404 tragen derzeit jeweils ein eigenes, gekürztes CSS. Das ist redundant. Ich habe bewusst **nicht** umgebaut, weil eine gemeinsame Datei die Struktur von `index.html` ändert und Sie das nicht entschieden hatten. Falls gewünscht, hole ich das nach. |
| 12 | **Telefon-Schreibweise** | Kleinigkeit | Ihr Impressumstext schreibt „0711 61 50 120", die Seite „0711 615 01 20". Dieselbe Nummer, andere Gruppierung. Ich habe Ihren Text im Impressum wörtlich übernommen. Für Verzeichniseinträge sollten Sie sich auf **eine** Schreibweise festlegen. |

Eine Angabe habe ich abgeleitet, ohne dass Sie sie ausdrücklich genannt haben:
`addressRegion: "Baden-Württemberg"` im JSON-LD. Das ist keine Aussage über den
Betrieb, sondern die Landeszugehörigkeit von Stuttgart. Sagen Sie Bescheid,
falls es raus soll.

---

## 6. Maßnahmen außerhalb der Datei, nach Wirkung je Aufwand sortiert

Die Reihenfolge ist bewusst so gewählt: Punkt 1 bringt für einen lokalen Laden
mehr als alles, was im Code steht.

### Sofort, sehr hohe Wirkung

**1 — Google-Unternehmensprofil vollständig einrichten und pflegen**
*Aufwand: 2–3 Stunden einmalig, danach 15 Minuten im Monat · Wirkung: sehr hoch*

Für ein Ladengeschäft ist das Unternehmensprofil wichtiger als die Website. Es
speist Google Maps, die lokale Suche und zunehmend auch die KI-Antworten.
Vollständig heißt: exakte Kategorie („Eisenwarenhandlung" als Haupt-, dazu
„Farbenfachgeschäft", „Baumarkt", „Schlüsseldienst" als Nebenkategorien), alle
Öffnungszeiten inklusive Feiertagsregelung, sämtliche Leistungen als Attribute,
Fotos, und die Antwortfunktion aktiviert. Verifizierung per Postkarte dauert
ein bis zwei Wochen — deshalb heute anstoßen.

**2 — Widersprüchliche Öffnungszeiten in den Verzeichnissen bereinigen**
*Aufwand: 2–4 Stunden · Wirkung: sehr hoch*

Sie erwähnten, dass Yelp, Das Örtliche und Google unterschiedliche Zeiten
führen. Das ist der schädlichste Einzelposten in der ganzen Liste: Widersprüche
untergraben das Vertrauen der Suchmaschinen in **alle** Ihre Angaben, und
Kundschaft, die vor verschlossener Tür steht, kommt nicht wieder. Legen Sie eine
Referenzfassung fest — Name, Anschrift, Telefon, Zeiten, exakt wie im Impressum —
und ziehen Sie jedes Verzeichnis darauf nach. Die Reihenfolge: Google, Apple,
Bing, Das Örtliche, Gelbe Seiten, Yelp, 11880.

**3 — Bewertungen einsammeln**
*Aufwand: gering, aber dauerhaft · Wirkung: sehr hoch*

Anzahl und Aktualität von Bewertungen gehören zu den stärksten Faktoren im
lokalen Ranking. Ein kleines Schild an der Kasse mit QR-Code zum Bewertungslink
und die Bitte an zufriedene Stammkundschaft genügen. Zwanzig echte Bewertungen
verändern die Sichtbarkeit spürbar. Antworten Sie auf jede — auch das wird
gewertet.

### Diese Woche, hohe Wirkung

**4 — Bing Places einrichten**
*Aufwand: 1 Stunde · Wirkung: hoch*

Bing speist Microsoft Copilot und über Umwege weitere Antwortsysteme. Der
Eintrag lässt sich weitgehend aus dem Google-Profil importieren.

**5 — Apple Business Connect**
*Aufwand: 1 Stunde · Wirkung: hoch*

Versorgt Apple Karten und Siri. Für Fußkundschaft im Viertel relevanter, als die
Nutzerzahlen vermuten lassen — auf dem iPhone ist Apple Karten Vorgabe.

**6 — Domain umziehen und Seite live nehmen**
*Aufwand: 1–2 Stunden · Wirkung: hoch*

Bis `www.farben-nagel.de` auf diese Seite zeigt, wirkt nichts davon. Danach:
Google Search Console und Bing Webmaster Tools einrichten, Sitemap einreichen.

### Diesen Monat, mittlere Wirkung

**7 — OpenStreetMap-Eintrag prüfen und ergänzen**
*Aufwand: 30–60 Minuten · Wirkung: mittel, aber unterschätzt*

OSM speist zahllose Karten-Apps und Navigationsgeräte — und wird von
Sprachmodellen als Quelle für Ortsangaben herangezogen. Relevante Tags:
`shop=hardware`, `name`, `opening_hours=Mo-Sa 08:00-20:00`, `phone`, `website`,
`addr:*`. Kostenlos und dauerhaft.

**8 — Fotos**
*Aufwand: 2 Stunden · Wirkung: mittel bis hoch*

`LIESMICH.txt` hält fest, dass das Ladenfoto aus einem Bildschirmfoto stammt und
entsprechend begrenzt ist. Ein Satz ordentlicher Aufnahmen — Ladenfront im
Querformat bei diffusem Licht mit Auslage, die Schubladenwand, die
Farbmischmaschine, ein Porträt — hebt Website und Unternehmensprofil zugleich.
Profile mit vielen Fotos werden messbar häufiger angeklickt.

**9 — Die restlichen Angaben aus Abschnitt 5 nachliefern**
*Aufwand: 30 Minuten · Wirkung: mittel*

Koordinaten, Preisspanne, Profil-URLs, Parken. Danach trage ich sie in einem
Durchgang nach.

### Laufend, geringer Aufwand

**10 — Feiertagszeiten pflegen**
*Aufwand: 10 Minuten je Feiertag · Wirkung: gering, aber ärgerlich, wenn es fehlt*

Google fragt vor Feiertagen aktiv nach. Wer nicht antwortet, bekommt den Hinweis
„Öffnungszeiten könnten abweichen" — genau die Unsicherheit, die einen Besuch
verhindert.

**11 — Lokale Verlinkung**
*Aufwand: unregelmäßig · Wirkung: mittel, langfristig*

Handelsverein, Stadtteilportale, Handwerkerlisten, Nachbarschaftsinitiativen.
Ein Link von einer echten Stuttgart-West-Seite wiegt für die lokale Suche mehr
als zehn beliebige Branchenverzeichnisse.

---

## 7. Was ich bewusst nicht getan habe

- Keine Änderung an Farbwerten, Layout, Typografie oder Abständen. Nachgewiesen
  durch die Geometriemessung an 40 Elementen bei drei Breiten.
- Keine erfundenen Koordinaten, Preisspannen, Zahlungsarten, Parkangaben oder
  Profile.
- Kein Umbau des Kontaktformulars ohne Ihre Entscheidung.
- Keine Änderung an Reim und Slogan.
- Keine Tracker, keine Analytik, kein Cookie-Banner — es gibt nichts zu
  banneren, und das ist ein Vorzug, kein Mangel.
- Die einzige CSS-Zeile, die ich hinzugefügt habe und die kein neues Element
  betrifft, ist `address{font-style:normal}`. Sie neutralisiert den kursiven
  Browser-Standard, damit die Fußzeile aussieht wie zuvor.

---

## 8. Das vollständige JSON-LD zur Kontrolle

Steht in `index.html` unmittelbar vor `</body>`. Hier zur Durchsicht:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "HardwareStore",
      "@id": "https://www.farben-nagel.de/#betrieb",
      "name": "Farben Nagel",
      "alternateName": "Farben Nagel Heimwerkermarkt",
      "description": "Inhabergeführter Heimwerkermarkt in Stuttgart-West seit 1966. Farben, Lacke und Lasuren nach Wunschton gemischt, Eisenwaren mit Einzelabgabe ab einem Stück, Werkzeug, Sanitär, Elektro, Boden und Tapete, Garten, Haushalt und Schlüsseldienst.",
      "url": "https://www.farben-nagel.de/",
      "logo": "https://www.farben-nagel.de/assets/logo.png",
      "image": [
        "https://www.farben-nagel.de/assets/og-bild.jpg",
        "https://www.farben-nagel.de/assets/laden.jpg",
        "https://www.farben-nagel.de/assets/band.jpg"
      ],
      "telephone": "+49 711 6150120",
      "email": "info@farben-nagel.de",
      "foundingDate": "1966",
      "currenciesAccepted": "EUR",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "Gutenbergstraße 65",
        "postalCode": "70176",
        "addressLocality": "Stuttgart",
        "addressRegion": "Baden-Württemberg",
        "addressCountry": "DE"
      },
      "openingHoursSpecification": [{
        "@type": "OpeningHoursSpecification",
        "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"],
        "opens": "08:00",
        "closes": "20:00"
      }],
      "areaServed": [
        {"@type":"Place","name":"Stuttgart-West"},
        {"@type":"Place","name":"Stuttgart-Mitte"},
        {"@type":"Place","name":"Stuttgart-Süd"}
      ],
      "knowsLanguage": "de",
      "hasOfferCatalog": {
        "@type": "OfferCatalog",
        "name": "Sortiment und Leistungen",
        "itemListElement": [
          { "@type": "OfferCatalog", "name": "Sortiment", "itemListElement": [
            "Farben & Lacke", "Eisenwaren", "Werkzeug", "Sanitär", "Elektro",
            "Boden & Tapete", "Garten & Balkon", "Haushalt", "Schlüssel"
          ]},
          { "@type": "OfferCatalog", "name": "Leistungen", "itemListElement": [
            "Farbe mischen", "Nachschlüssel", "Zuschnitt", "Lieferung im Viertel",
            "Bestellservice", "Reservierung", "Rechnungskonto für Betriebe"
          ]}
        ]
      }
    },
    { "@type": "WebSite",  "@id": "…/#website" },
    { "@type": "WebPage",  "@id": "…/#startseite" },
    { "@type": "BreadcrumbList", "@id": "…/#breadcrumb" },
    { "@type": "FAQPage",  "@id": "…/#fragen", "mainEntity": "8 Fragen mit Antworten" }
  ]
}
```

> **Hinweis zur Darstellung:** In dieser Übersicht sind die Katalogeinträge und
> die vier hinteren Knoten verkürzt wiedergegeben, damit die Struktur lesbar
> bleibt. In `index.html` steht die vollständige, ausgeschriebene Fassung — dort
> ist jeder Sortimentsbereich ein `Offer` mit `Product` und Beschreibung, jede
> Leistung ein `Offer` mit `Service`, und jede der acht Fragen ein `Question` mit
> vollständigem `acceptedAnswer`.

---

## 9. Nächster Schritt

Kurzfassung: Beantworten Sie die Punkte 2 bis 7 aus Abschnitt 5, dann trage ich
sie in einem Durchgang nach. Unabhängig davon können Sie mit Punkt 1 der Liste
in Abschnitt 6 — dem Google-Unternehmensprofil — sofort anfangen; das braucht
mich nicht und wirkt am stärksten.

Bevor die Seite öffentlich geht, müssen zwingend erledigt sein: der
Hostinganbieter in der Datenschutzerklärung, die Bestätigung zur
Verbraucherstreitbeilegung und eine Entscheidung zum Kontaktformular. Alles
andere lässt sich später nachziehen.
