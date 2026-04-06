# USS Cori Website Dokumentation

## Zweck dieser Doku

Diese Datei dokumentiert den aktuellen Aufbau der USS-Cori-Webseite, damit Änderungen später nicht im Chaos enden.

Ziele:
- Überblick über die Projektstruktur
- verstehen, welche Datei wofür zuständig ist
- schnell sehen, wo Inhalte geändert werden
- spätere Erweiterungen sauber planen
- anderen Leuten das Projekt verständlich machen

---

## Technik-Stack

Die Seite basiert aktuell auf:

- **Astro** für Routing und Seitenaufbau
- **JSON-Dateien** für Sprachinhalte und Abteilungsdaten
- **Astro-Komponenten** für Layout und wiederverwendbare Bereiche
- **CSS direkt im Layout** für das Design

Warum Astro:
- sauberer als eine einzige HTML-Datei
- einfache Struktur für mehrsprachige Seiten
- gut für statische Webseiten
- später leicht erweiterbar

---

## Projektstruktur

```text
src/
  components/
    AboutOverview.astro
    DepartmentPage.astro
    Departments.astro
    Footer.astro
    Header.astro
    Hero.astro
    ReadyRoom.astro
    RegionNine.astro
    StatsGrid.astro
    TranslationNote.astro

  data/
    lang/
      en.json
      de.json
      departments/
        engineering-en.json
        engineering-de.json
        science-en.json
        science-de.json
        operations-en.json
        operations-de.json
        medical-en.json
        medical-de.json

    ship-status.json
    ship-status-profiles.json
    ship-status.README.txt

  layouts/
    BaseLayout.astro

  pages/
    index.astro
    [lang].astro
    [lang]/
      departments/
        [department].astro

public/
  images/
    departments/
      engineering.png
      science.png
      operations.png
      medical.png
```

---

## Routing

### Startseite

- `src/pages/index.astro`
- leitet Besucher je nach Sprache weiter
- aktuell auf `/de` oder `/en`

### Sprachseiten

- `src/pages/[lang].astro`
- zentrale Sprachseite für Deutsch und Englisch
- lädt die passenden Sprachdateien
- setzt die Hauptkomponenten zusammen

Beispiele:
- `/de`
- `/en`

### Abteilungsseiten

- `src/pages/[lang]/departments/[department].astro`
- erzeugt die klickbaren Unterseiten der Abteilungen

Beispiele:
- `/de/departments/engineering`
- `/en/departments/engineering`
- `/de/departments/medical`

---

## Hauptdateien und ihre Aufgaben

### `src/layouts/BaseLayout.astro`

Das Grundlayout der Seite.

Zuständig für:
- `<html>` und `<head>`
- globale Styles
- Hintergrund
- Sterneffekt / Weltraumoptik
- allgemeine Layoutklassen
- Stil der Department-Seiten

Wenn etwas optisch global geändert werden soll, ist dies meistens die richtige Datei.

---

### `src/pages/[lang].astro`

Die zentrale Sprachseite.

Aufgaben:
- lädt `en.json` und `de.json`
- entscheidet, welche Sprache aktiv ist
- setzt die sichtbaren Hauptkomponenten zusammen

Diese Datei sollte möglichst sauber bleiben und vor allem aus:
- Imports
- Sprachlogik
- Komponentenaufrufen
bestehen.

---

### `src/components/Header.astro`

Obere Navigationsleiste.

Enthält:
- USS Cori Titel
- Navigation
- Sprachumschalter

---

### `src/components/Hero.astro`

Der große Einstiegsbereich oben auf der Startseite.

Enthält:
- Haupttitel
- Untertitel
- Einführungstext
- Buttons
- rechter Medienbereich

---

### `src/components/AboutOverview.astro`

Der Überblicksbereich der Hauptseite.

Enthält:
- Überschrift des Überblicks
- Beschreibung
- StatsGrid
- TranslationNote

---

### `src/components/StatsGrid.astro`

Die kleinen Status-/Info-Karten im Überblicksbereich.

Beispiele:
- Kennung
- Klasse
- Format
- Schwerpunkt

---

### `src/components/TranslationNote.astro`

Hinweis zur Mehrsprachigkeit und zu Übersetzungsvorschlägen.

---

### `src/components/RegionNine.astro`

Region-9-Bereich auf der Startseite.

Enthält:
- kurze Erklärung zu Region 9
- ein- und ausklappbare Länderliste

Hinweis:
Region 9 soll klein bleiben. Fokus der Seite bleibt die Cori.

---

### `src/components/Departments.astro`

Die Abteilungskarten auf der Hauptseite.

Aktuell:
- klickbar
- verlinken auf Unterseiten

Abteilungen:
- Engineering
- Science
- Operations
- Medical

---

### `src/components/ReadyRoom.astro`

Der untere Einstiegsbereich auf der Hauptseite.

Aktuell:
- Andockschleuse-Text
- Buttons
- Statuspanel der Cori

---

### `src/components/DepartmentPage.astro`

Das gemeinsame Layout für alle Abteilungsseiten.

Enthält:
- Breadcrumbs
- Titelbereich
- Logo oder Platzhalter
- Karten für Schwerpunkte
- typische Einsatzfelder
- Kulturtext
- optionale Zusatzbereiche wie Systeme, Projekte, Leitbild

Wird von allen Abteilungen gemeinsam genutzt.

---

## Sprachdateien der Hauptseite

### `src/data/lang/de.json`
### `src/data/lang/en.json`

Diese Dateien enthalten die Texte der Hauptseite.

Dazu gehören unter anderem:
- Titel
- Navigation
- Hero-Texte
- Überblick
- Region 9
- Abteilungen
- Andockschleuse
- Statuspanel-Beschriftungen

Wenn Texte auf der Hauptseite geändert werden sollen, wird das meistens hier gemacht.

---

## Sprachdateien der Abteilungen

### Ordner

```text
src/data/lang/departments/
```

### Aktuelle Dateien

- `engineering-de.json`
- `engineering-en.json`
- `science-de.json`
- `science-en.json`
- `operations-de.json`
- `operations-en.json`
- `medical-de.json`
- `medical-en.json`

### Zweck

Diese Dateien enthalten die Inhalte der Abteilungsseiten.

Beispiele für Felder:
- `title`
- `subtitle`
- `intro`
- `focusTitle`
- `focusItems`
- `missionExamplesTitle`
- `missionExamples`
- `cultureTitle`
- `cultureText`
- optionale Zusatzbereiche wie `systemsTitle`, `projectsTitle`, `noteTitle`

---

## Bilder

### Department-Logos

Pfad:

```text
public/images/departments/
```

Beispiele:
- `public/images/departments/engineering.png`
- `public/images/departments/science.png`

Wichtig:
- Logos sollten möglichst knapp beschnitten sein
- zu viel transparenter Rand macht das Logo optisch kleiner
- das Problem sitzt oft nicht im CSS, sondern im PNG selbst

Die Zuweisung der Logos passiert aktuell in:

```text
src/pages/[lang]/departments/[department].astro
```

Im Objekt `departmentLogos`.

---

## Statussystem der Cori

### Zweck

Das Statuspanel auf der Hauptseite zeigt den aktuellen Schiffszustand.

Aktuell mögliche Felder:
- Hüllenintegrität
- Warpkernstatus
- Langstreckensensoren
- Schiffsstatus
- aktuelle Position

---

### `src/data/ship-status-profiles.json`

Enthält alle verfügbaren Statusprofile.

Aktuelle Profile:
- `mission`
- `drydock`
- `standby`
- `patrol`
- `transit`
- `orbit`
- `systemcheck`
- `diplomatic`

Jedes Profil enthält:
- deutschen Wertesatz
- englischen Wertesatz

---

### `src/data/ship-status.json`

Steuert den aktuell aktiven Zustand.

Dort wird geändert:
- `activeProfile`
- optional `locationOverride.de`
- optional `locationOverride.en`

Beispiel:

```json
{
  "activeProfile": "mission",
  "locationOverride": {
    "de": "Nahe Deep Space 9",
    "en": "Near Deep Space 9"
  }
}
```

Wenn `locationOverride` leer bleibt, wird der Standardort aus dem Profil verwendet.

---

### `src/data/ship-status.README.txt`

Dokumentation für das Statussystem.

Enthält:
- welche Felder geändert werden dürfen
- welche Profilwerte gültig sind
- Beispielkonfigurationen

---

## Aktueller Designstand

Die Seite ist aktuell:
- mehrsprachig
- modular aufgebaut
- sternenflottennah im Ton
- visuell modern statt streng LCARS
- mit dezent animiertem Hintergrund

Wichtige Designentscheidungen:
- LCARS nur inspiriert, nicht 1:1
- Fokus auf ruhige Sci-Fi-Ästhetik
- klickbare Department-Seiten
- Logos als starke visuelle Marker

---

## Offene oder spätere Punkte

### Hauptseite
- Buttons noch mit echten Zielen versehen
- obere Hero-Rechte-Seite langfristig weiter veredeln
- Statuspanel später ggf. adminfähig per Dropdown

### Abteilungen
- Abteilungsleitung sichtbar machen, aber nur bei Wunsch
- eigene Berichte, Projekte, Events pro Abteilung
- spätere redaktionelle Pflege durch Bereichsleiter

### Crew
- nur opt-in
- keine ungefragte Darstellung
- Profilbild wählbar
- Admin pflegt Inhalte ein

### Region 9
- bewusst klein halten
- Fokus bleibt auf der Cori

### Zukunftsideen
- Klingonischer Easter-Egg-Modus
- Adminfreundliche Statusauswahl
- Pflegbare Abteilungslogs
- Mehr echte Inhalte statt Strukturarbeit

---

## Arbeitsprinzip für weitere Änderungen

Wenn neue Inhalte gebaut werden, gilt:

1. erst Struktur sauber halten
2. dann Inhalte ergänzen
3. Sprache und Ton einheitlich halten
4. keine unnötige Übertechnik bauen
5. erst eine Sache sauber, dann die nächste

Kurz:
Nicht alles gleichzeitig anfassen.
Erst funktionsfähig, dann hübsch, dann komfortabel.

---

## Empfehlung für die nächsten Schritte

Sinnvolle Reihenfolge:

1. Engineering als Referenzseite weiter ausbauen
2. Medical, Science und Operations im selben Stil nachziehen
3. echte Ziele für Buttons setzen
4. Bereich für Leitung / Projekte / Logs vorbereiten
5. spätere Pflege durch Abteilungsleiter planen

---

## Notiz

Diese Doku ist absichtlich lebendig gedacht.
Sie soll mit dem Projekt mitwachsen und nicht einmal geschrieben und dann vergessen werden.

