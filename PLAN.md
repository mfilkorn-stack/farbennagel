# PLAN — SEO- und AI-Search-Optimierung Farben Nagel

Stand: 26.08.2026 · Grundlage: vollständige Lesung von `index.html` (475 Zeilen,
31,9 KB), `LIESMICH.txt`, `.github/workflows/static.yml`, `assets/`.

Dieser Plan beschreibt, **was** geändert werden soll, **warum**, und welche
**Annahmen** dafür nötig wären. Es ist noch kein Code geschrieben. Die offenen
Fragen stehen gebündelt in Abschnitt 9 — bitte diese zuerst beantworten.

---

## 1. Ausgangslage

**Was gut ist und bleibt**

| Punkt | Befund |
|---|---|
| Struktur | Eine Datei, CSS und JS inline, keine Abhängigkeiten. Funktioniert per Doppelklick. |
| Überschriften | Genau eine `h1`. Hierarchie h1 → h2 → h3 ist bereits sauber. |
| Bilder | Alle drei haben aussagekräftige `alt`-Texte. |
| Interaktion | WhatsApp-Deeplink, Sortiment-Kacheln, Öffnungsstatus — alles clientseitig, kein Tracking. |
| Marke | Reim, Slogan, Logo, Farbwerte. Wird nicht angefasst. |

**Was fehlt oder blockiert**

| Nr. | Befund | Wirkung |
|---|---|---|
| B1 | Keine strukturierten Daten (kein JSON-LD) | Google/Bing erkennen den Betrieb nicht als lokales Geschäft. Kein Rich Result, keine Öffnungszeiten in der Suche. |
| B2 | Kein `canonical`, keine Open-Graph-/Twitter-Tags, kein Favicon | Kein Vorschaubild beim Teilen. Duplicate-Content-Risiko über verschiedene URL-Varianten. |
| B3 | Google Fonts wird von `fonts.googleapis.com` geladen | **DSGVO-Verstoß.** Übermittelt IP-Adressen in die USA. Abmahnrisiko (LG München I, 3 O 17493/20). |
| B4 | Kein Impressum, keine Datenschutzerklärung | **Rechtlich zwingend (§ 5 DDG, Art. 13 DSGVO).** Die Seite darf so nicht online. |
| B5 | Formular sendet an `https://formspree.io/f/FORMULAR-ID` | Platzhalter — das Formular **funktioniert aktuell nicht**. Zusätzlich: US-Dienstleister, DSGVO-relevant. |
| B6 | Keine `robots.txt`, keine `sitemap.xml`, keine `404.html` | Crawler bekommen keine Wegweisung. KI-Crawler haben keine explizite Erlaubnis. |
| B7 | Bilder unoptimiert: 1,06 MB in `assets/` | `laden.jpg` 368 KB bei 1600×1034, angezeigt auf max. ~600 CSS-px. `logo.png` 305 KB bei 864×477, angezeigt auf max. 258 CSS-px. Bremst Mobile-Performance deutlich. |
| B8 | Kein `width`/`height` an zwei von drei Bildern | Layout-Shift (CLS), kostet Lighthouse-Punkte. |
| B9 | Kein `<main>`, Anschrift nicht als `<address>` | Schwächere semantische Signale für Crawler und Screenreader. |
| B10 | Kein Fließtext, der eine konkrete Frage beantwortet | Antwortmaschinen zitieren Absätze. Aktuell gibt es keinen zitierfähigen Absatz. |
| B11 | `logo-sand.png` (250 KB) wird von `index.html` nicht verwendet | Toter Ballast im Deployment. |

---

## 2. Leitplanken, an die ich mich halte

- **Statisch.** Kein Build-Step, kein Framework, kein Server. Hochladen genügt.
- **Design unverändert.** Farbwerte, Logo, Layout, Typografie, Abstände bleiben.
  Neue Inhalte (FAQ, Faktenblock) verwenden **ausschließlich die bereits
  vorhandenen Bausteine** (`.cols`, `.cell`, `.sec-head`, `section.rule`,
  `section.dark`). Es entsteht keine neue visuelle Sprache.
- **Eine Ausnahme, die ich vorab nenne:** Das `<address>`-Element hat im
  Browser-Standard `font-style: italic`. Damit die Fußzeile *exakt* so aussieht
  wie heute, kommt eine Regel `address{font-style:normal}` dazu. Das ist eine
  Neutralisierung, keine Gestaltungsänderung.
- **Keine erfundenen Fakten.** Alles, was Sie mir nicht bestätigt haben, wird
  nicht geschrieben, sondern als `TODO`-Kommentar markiert und in Abschnitt 9
  erfragt. Erfundene NAP-Daten (Name/Adresse/Telefon) schaden aktiv, weil sie
  die Konsistenz über Verzeichnisse hinweg zerstören.
- **Kein Keyword-Stuffing.** Jeder neue Satz muss für einen Menschen lesbar sein.
- **Deutsch, durchgehend Sie-Form.**

---

## 3. Was ich als bestätigt betrachte

Aus Ihrem Auftrag und aus dem bestehenden Seitentext:

| Angabe | Wert | Quelle |
|---|---|---|
| Name | Farben Nagel | Auftrag |
| Betriebsart | Heimwerkermarkt / Mini-Baumarkt | Auftrag |
| Gegründet | 1966 | Auftrag + Seitentext |
| Straße | Gutenbergstraße 65 | Auftrag |
| PLZ / Ort | 70176 Stuttgart | Auftrag |
| Stadtteil | Stuttgart-West | Auftrag |
| Telefon | 0711 615 01 20 → `+4971161 50120` | Auftrag |
| Öffnungszeiten | Mo–Sa 08:00–20:00, So geschlossen | Auftrag + Seite |
| 72 Stunden/Woche | 6 Tage × 12 h = 72 — rechnerisch belegt | abgeleitet |
| Sortiment | 9 Bereiche | Auftrag + Seite |
| Leistungen | Farbe mischen, Zuschnitt, Nachschlüssel, Lieferung im Viertel, Bestellservice, Reservierung | Auftrag + Seite |
| Anfahrt | Rotebühlstraße → Schwabstraße (REWE); S-Bahn S1–S5 Schwabstraße; Bus 42 und 44 | bestehender Seitentext |
| Zielgruppen | Anwohner Stuttgart-West, Handwerk, Hausverwaltung, Gastronomie | Auftrag |

**Nicht bestätigt und daher gesperrt:** Geokoordinaten, E-Mail-Adresse, Inhaber
und Rechtsform, Umsatzsteuer-ID, Preisspanne, Zahlungsarten, Parkmöglichkeiten,
Barrierefreiheit, Social-Media-Profile, Domain.

---

## 4. Geplante Änderungen — Aufgabe A bis E

### A — Technisches Fundament (`index.html`)

| Maßnahme | Details |
|---|---|
| `<title>` | Auf Suchintention geschnitten, ~60 Zeichen. Vorschlag: *„Farben Nagel — Heimwerkermarkt Stuttgart-West, Mo–Sa bis 20 Uhr"*. Rückt Ort und das stärkste Unterscheidungsmerkmal (lange Öffnungszeiten) nach vorn. |
| `meta description` | ~155 Zeichen, mit Einzelabgabe und Öffnungszeiten als Klickanreiz. |
| `canonical`, `robots`, `theme-color` | `theme-color` = `#A81E24` (vorhandenes Markenrot, keine neue Farbe). `canonical` **braucht die endgültige Domain** → Frage 1. |
| Open Graph + Twitter Card | `og:title`, `og:description`, `og:image` (1200×630), `og:url`, `og:type=business.business`, `og:locale=de_DE`, `twitter:card=summary_large_image`. |
| Favicon-Set | Aus `logo-sand.png` erzeugt (Logo auf dem Original-Sandton, quadratisch gepolstert): `favicon.ico` (16/32/48), `favicon-32.png`, `favicon-16.png`, `apple-touch-icon.png` (180×180), `site.webmanifest`. |
| Bilder | `width`/`height` an alle drei, `decoding="async"`, `loading="lazy"` an `laden.jpg`, `fetchpriority="high"` am Kopfbild. `alt`-Texte werden geschärft (Ort und Betriebsart hinein, ohne Stuffing). |
| Schriften lokal | 7 `woff2`-Dateien (Fira Sans 400/500/600/700, Fira Sans Condensed 600/700, Lobster 400), Subset `latin`, `font-display: swap`, `preload` für die zwei Above-the-fold-Schnitte. **Danach null externe Netzwerkaufrufe.** |
| Semantik | `.masthead` wird `<header>`, Inhalt kommt in `<main>`, Fußzeilen-Anschrift wird `<address>`. Überschriftenhierarchie bleibt (weiter genau eine `h1`). |
| Bildoptimierung | `laden.jpg` 1600→1200 px, `band.jpg` 2772→1800 px, `logo.png` 864→560 px. Ziel: `assets/` von 1,06 MB auf **unter 250 KB**. |
| Neue Dateien | `robots.txt`, `sitemap.xml`, `404.html` (im Seitendesign). |
| Weiterleitung `/home.html` | `.htaccess` (Apache) **und** `_redirects` (Netlify) wie beauftragt. **Hinweis:** Auf GitHub Pages wirkt keins von beiden — dort braucht es zusätzlich eine echte `home.html` mit `<meta http-equiv="refresh">` und `<link rel="canonical">`. Ich liefere alle drei Varianten, damit die Seite auf jedem Hoster richtig weiterleitet. |

### B — Strukturierte Daten (JSON-LD)

Ein `<script type="application/ld+json">` mit `@graph`:

1. **`HardwareStore`** (gültiger Untertyp von `LocalBusiness`) — `name`, `image`,
   `logo`, `url`, `telephone`, `address` als `PostalAddress`, `geo` *(braucht
   Frage 2)*, `openingHoursSpecification` Mo–Sa 08:00–20:00, `priceRange`
   *(Frage 3)*, `areaServed`, `foundingDate: "1966"`, `sameAs` *(Frage 4)*.
2. **`hasOfferCatalog`** — 9 Sortimentsbereiche + 6 Serviceleistungen, exakt
   aus dem bestehenden Seiteninhalt gespiegelt.
3. **`FAQPage`** — dieselben Fragen und Antworten, die sichtbar auf der Seite
   stehen (Google verlangt Deckungsgleichheit; unsichtbare FAQ-Markup ist ein
   Richtlinienverstoß).
4. **`WebSite`** und **`BreadcrumbList`**.

Validierung gegen Rich-Results-Test und schema.org, Ausgabe des vollständigen
JSON-LD im REPORT zur Kontrolle.

### C — Inhalt für Antwortmaschinen

Zwei neue Abschnitte, gebaut aus vorhandenen Bausteinen:

**C1 — Faktenblock** („Farben Nagel in Kürze"), kompakt und übernehmbar:
Betriebsart, Ort, Zeiten, Sortiment, Besonderheiten. Genau der Absatz, den ein
Modell als Ganzes zitiert.

**C2 — FAQ-Abschnitt.** Je Frage eine `h3` und **eine eigenständige Antwort von
40–70 Wörtern**, die auch ohne den Rest der Seite verständlich ist. Geplante
Fragen:

1. Wo bekomme ich in Stuttgart-West einzelne Schrauben, Muttern oder Dübel?
2. Kann ich Farbe in einem Wunschton mischen lassen?
3. Wo kann ich in Stuttgart-West einen Schlüssel nachmachen lassen?
4. Welcher Baumarkt in Stuttgart hat samstags bis 20 Uhr offen?
5. Wie komme ich zu Farben Nagel — und wo kann ich parken? *(Parken → Frage 5)*
6. Liefern Sie im Stuttgarter Westen?
7. Gibt es ein Rechnungskonto für Handwerksbetriebe und Hausverwaltungen?

**C3 — Geografische Verankerung.** Damit Modelle den Betrieb im Raum verorten,
werden reale Umgebungsentitäten benannt: Stuttgart-West, Gutenbergstraße,
Rotebühlstraße, Schwabstraße, S-Bahn-Haltestelle Schwabstraße (S1–S5), Buslinien
42 und 44, Stuttgart-Mitte, Stuttgart-Süd. Weitere Quartiersnamen nur nach Ihrer
Freigabe → Frage 6.

**C4 — Alleinstellung nachprüfbar statt werblich.** „72 Öffnungsstunden pro
Woche", „Einzelabgabe ab einem Stück", „Beratung durch eine Person" — jeweils
belegbar. Keine Superlative.

**Reim und Slogan bleiben unverändert.** Sie sind Markenkern und werden zusätzlich
maschinenlesbar in den Faktenblock eingebettet.

### D — Zugang für KI-Crawler

- **`robots.txt`** mit ausdrücklicher Erlaubnis für `GPTBot`, `ClaudeBot`,
  `anthropic-ai`, `PerplexityBot`, `Google-Extended`, `CCBot`,
  `Applebot-Extended` plus Verweis auf die Sitemap. Begründung kommt in den
  REPORT.
- **`llms.txt`** im Wurzelverzeichnis: der Betrieb in wenigen faktischen Sätzen,
  plus Verweise auf die wichtigsten Inhalte.

### E — Rechtliches

- **`impressum.html`** und **`datenschutz.html`** im Seitendesign, verlinkt aus
  der Fußzeile. Mit klar markierten Platzhaltern für alles, was ich nicht habe
  (Fragen 7–9).
- Die Datenschutzerklärung muss außerdem den Formularversand abdecken → Frage 10.

---

## 5. Reihenfolge der Umsetzung

1. Schriften lokal einbinden (behebt den DSGVO-Verstoß B3 — höchste Dringlichkeit)
2. Bilder optimieren, Favicons und OG-Bild erzeugen
3. `<head>` neu: Meta, Canonical, OG/Twitter, Icons
4. Semantik: `<main>`, `<header>`, `<address>`, Bildattribute
5. Neue Inhalte: Faktenblock, FAQ, geografische Verankerung
6. JSON-LD ergänzen und validieren
7. `robots.txt`, `sitemap.xml`, `llms.txt`, `404.html`, Weiterleitungen
8. `impressum.html`, `datenschutz.html`, Fußzeilen-Verlinkung
9. Prüfung: Screenshot-Vergleich vorher/nachher, Lighthouse mobil, Validierung
10. `REPORT.md`

---

## 6. Prüfung vor Abgabe

| Kriterium | Methode |
|---|---|
| Doppelklick auf `index.html` funktioniert | `file://`-Aufruf im Browser, alle Pfade relativ |
| Keine externen Netzwerkaufrufe | Playwright protokolliert jeden Request; erwartet: nur eigene Assets |
| JSON-LD fehlerfrei | Strukturprüfung + Rich-Results-Test |
| Lighthouse ≥ 95 in allen vier Kategorien (mobil) | Lighthouse CLI headless gegen lokalen Server |
| Design unverändert | Pixelvergleich der gerenderten Seite vorher/nachher, Desktop 1140 px und Mobil 390 px |
| Barrierefreiheit nicht schlechter | Kontrastprüfung der neuen Textfarben, Fokus-Sichtbarkeit, Überschriftenhierarchie |
| Seitengewicht | Summe HTML + CSS + Schriften + Icons, Ziel < 400 KB |

---

## 7. Risiken, die ich sehe

| Risiko | Umgang |
|---|---|
| **Lokale Schriften kosten ~140 KB.** Das ist der größte Posten im Budget. | Nur `latin`-Subset, nur benötigte Schnitte, `preload` für zwei. Falls das Budget kippt, schlage ich vor, `Fira Sans 500` zu streichen (wird nur an einer Stelle genutzt) — vorher frage ich. |
| **Lighthouse-Performance hängt am Hoster.** Ich messe lokal; GitHub Pages liefert typischerweise vergleichbar. | Messwerte im REPORT mit Hinweis auf die Messumgebung. |
| **FAQ-Rich-Results zeigt Google seit 2023 nur noch eingeschränkt an.** | Das Markup bleibt trotzdem sinnvoll: Antwortmaschinen und Bing nutzen es weiterhin. Ich sage im REPORT, was realistisch zu erwarten ist. |
| **`og:image` ist ein neues Gestaltungsartefakt.** | Ich schneide es aus dem bestehenden Ladenfoto (1200×630), erfinde keine neue Bildsprache. Sie sehen es vor dem Commit. |
| **Ohne die Antworten aus Abschnitt 9 bleiben Lücken** (Geo, Impressum, Domain). | Diese Felder bleiben als `TODO` markiert und sind im REPORT einzeln aufgeführt. |

---

## 8. Was ich *nicht* tue

- Keine Änderung an Farbwerten, Layout, Typografie, Abständen.
- Keine erfundenen Geokoordinaten, keine erfundene E-Mail, keine erfundenen
  Zahlungsarten, keine erfundenen Profile.
- Keine Tracker, keine Analytics, keine externen Skripte, keine Cookie-Banner
  (weil es nichts zu banneren gibt).
- Kein Umbau des Formulars ohne Ihre Entscheidung (Frage 10).
- Keine Änderung an Reim und Slogan.

---

## 9. Offene Fragen — bitte gebündelt beantworten

### Fakten, die ich nicht erfinden darf

**1 — Domain.** *(blockierend)* Unter welcher Adresse geht die Seite live? Aktuell deployt der
GitHub-Actions-Workflow nach `https://mfilkorn-stack.github.io/farbennagel/`.
Gibt es eine eigene Domain (z. B. `farben-nagel.de`)? Davon hängen ab:
`canonical`, `sitemap.xml`, `og:url`, `llms.txt` und die `@id` im JSON-LD.
*Falls noch offen: Ich baue mit der GitHub-Pages-URL und markiere jede Stelle,
die beim Domainwechsel angepasst werden muss.*

**2 — Geokoordinaten.** Breiten- und Längengrad des Ladens. Ohne `geo` fehlt dem
`LocalBusiness`-Markup das stärkste Signal für die Kartensuche. Ich erfinde
keine Koordinaten. Sie finden sie in Google Maps per Rechtsklick auf den Laden.

**3 — Preisspanne** (`priceRange`). Schema.org erwartet eine grobe Angabe wie
`€` oder `€€`. Was passt?

**4 — Profile** (`sameAs`). Gibt es ein Google-Unternehmensprofil, Facebook,
Instagram, einen Eintrag bei Das Örtliche oder Yelp? Bitte die URLs — sie
verknüpfen die Einträge miteinander und stärken alle gemeinsam.

**5 — Parken.** Die FAQ-Frage „Anfahrt und Parken" ist eine der meistgesuchten.
Gibt es Kundenparkplätze, Kurzzeitparken vor der Tür, oder nur Anwohnerparken im
Viertel? Ohne Angabe lasse ich das Thema Parken weg.

**6 — Umgebungsentitäten.** Darf ich neben Stuttgart-West auch benachbarte
Quartiere namentlich nennen, damit Modelle den Standort besser verorten? Bitte
streichen, was nicht passt: Rosenbergstraße, Hölderlinplatz, Feuersee,
Vogelsang, Stuttgart-Mitte, Stuttgart-Süd, Botnang.

### Für Impressum und Datenschutz (rechtlich zwingend, alle blockierend)

**7 — Anbieter.** Vollständiger Name des Inhabers oder der Firma, Rechtsform
(z. B. „Max Mustermann e. K." oder „Farben Nagel GmbH"), und wer inhaltlich
verantwortlich ist.

**8 — Registerangaben.** Handelsregisternummer und Registergericht, falls
eingetragen. Umsatzsteuer-Identifikationsnummer nach § 27 a UStG, oder ersatzweise
die Steuernummer.

**9 — E-Mail-Adresse.** Für das Impressum zwingend („schnelle elektronische
Kontaktaufnahme", § 5 DDG). Zusätzlich brauche ich sie für das Kontaktformular.

### Entscheidungen zur Umsetzung

**10 — Kontaktformular.** Das Formular zeigt aktuell auf
`https://formspree.io/f/FORMULAR-ID` — ein Platzhalter, es funktioniert nicht.
Drei Wege:
- **(a) Formspree behalten:** Sie legen ein Konto an und geben mir die echte ID.
  Kostenlos bis 50 Einsendungen/Monat. Braucht einen Absatz in der
  Datenschutzerklärung (US-Dienstleister).
- **(b) Auf `mailto:` umstellen:** Öffnet das Mailprogramm der Besucherin. Keine
  externen Dienste, keine DSGVO-Fragen, aber Dateianhänge funktionieren nicht
  zuverlässig und der Komfort sinkt.
- **(c) Formular entfernen,** WhatsApp und Telefon als Wege belassen.

**11 — CSS-Datei.** Impressum, Datenschutz und 404 brauchen dasselbe Design. Ich
kann das CSS in eine gemeinsame `assets/stil.css` auslegen (sauberer, insgesamt
weniger Bytes, weiterhin per Doppelklick nutzbar) — oder in jeder Datei inline
wiederholen (bleibt exakt bei „eine Datei genügt", aber redundant).
**Meine Empfehlung: gemeinsame Datei.**

**12 — Bildoptimierung.** Ich würde `laden.jpg`, `band.jpg` und `logo.png`
verkleinern und neu komprimieren (1,06 MB → unter 250 KB). Die Originale lege ich
unter `assets/original/` ab, damit nichts verloren geht. Einverstanden?

---

## 10. Nächster Schritt

Sobald Ihre Antworten vorliegen, setze ich in der Reihenfolge aus Abschnitt 5 um
und liefere am Ende `REPORT.md` mit dem vollständigen JSON-LD, den Messwerten und
der priorisierten Maßnahmenliste außerhalb der Datei (Google-Unternehmensprofil,
NAP-Konsistenz, Bewertungen, Bing Places, Apple Business Connect, OpenStreetMap,
Fotos).

Fragen 1, 7, 8 und 9 sind die einzigen echten Blockierer. Die übrigen kann ich
mit `TODO`-Markierungen überbrücken, wenn Sie schnell live gehen wollen.
