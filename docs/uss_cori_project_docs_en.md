# USS Cori Website Documentation

## Purpose of this document

This file documents the current structure of the USS Cori website so later changes do not turn into chaos.

Goals:
- keep an overview of the project structure
- understand which file is responsible for what
- quickly see where content should be edited
- plan future expansions cleanly
- make the project understandable for other people

---

## Tech stack

The site currently uses:

- **Astro** for routing and page structure
- **JSON files** for language content and department data
- **Astro components** for layout and reusable sections
- **CSS inside the layout** for the visual design

Why Astro:
- cleaner than one giant HTML file
- good structure for multilingual pages
- well suited for static websites
- easy to expand later

---

## Project structure

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

### Landing page

- `src/pages/index.astro`
- redirects visitors depending on language
- currently to `/de` or `/en`

### Language pages

- `src/pages/[lang].astro`
- central language page for German and English
- loads the correct language files
- assembles the main page components

Examples:
- `/de`
- `/en`

### Department pages

- `src/pages/[lang]/departments/[department].astro`
- creates the clickable department subpages

Examples:
- `/de/departments/engineering`
- `/en/departments/engineering`
- `/de/departments/medical`

---

## Main files and responsibilities

### `src/layouts/BaseLayout.astro`

The global page layout.

Responsible for:
- `<html>` and `<head>`
- global styles
- background
- stars / space effects
- shared layout classes
- department page styling

If something visual should change globally, this is usually the right file.

---

### `src/pages/[lang].astro`

The central language page.

Responsibilities:
- loads `en.json` and `de.json`
- decides which language is active
- assembles the visible main components

This file should stay as clean as possible and mainly contain:
- imports
- language logic
- component calls

---

### `src/components/Header.astro`

Top navigation bar.

Contains:
- USS Cori title
- navigation
- language switcher

---

### `src/components/Hero.astro`

The large entry section at the top of the landing page.

Contains:
- main title
- subtitle
- intro text
- buttons
- right media area

---

### `src/components/AboutOverview.astro`

Overview section of the landing page.

Contains:
- overview heading
- description
- StatsGrid
- TranslationNote

---

### `src/components/StatsGrid.astro`

Small info cards in the overview section.

Examples:
- registry
- class
- format
- focus

---

### `src/components/TranslationNote.astro`

Note about multilingual support and translation suggestions.

---

### `src/components/RegionNine.astro`

Region 9 section on the landing page.

Contains:
- short explanation of Region 9
- collapsible country list

Note:
Region 9 should stay compact. The Cori remains the main focus of the site.

---

### `src/components/Departments.astro`

Department cards on the landing page.

Currently:
- clickable
- link to department subpages

Departments:
- Engineering
- Science
- Operations
- Medical

---

### `src/components/ReadyRoom.astro`

The lower entry section on the landing page.

Currently:
- Docking Bay text
- buttons
- Cori status panel

---

### `src/components/DepartmentPage.astro`

The shared layout for all department pages.

Contains:
- breadcrumbs
- title area
- logo or placeholder
- focus cards
- typical mission areas
- culture text
- optional extra sections such as systems, projects, doctrine

Used by all departments.

---

## Main language files

### `src/data/lang/de.json`
### `src/data/lang/en.json`

These files contain the main page text.

This includes:
- title
- navigation
- hero text
- overview
- Region 9
- departments
- Docking Bay
- status panel labels

If text on the landing page should change, it will usually happen here.

---

## Department language files

### Folder

```text
src/data/lang/departments/
```

### Current files

- `engineering-de.json`
- `engineering-en.json`
- `science-de.json`
- `science-en.json`
- `operations-de.json`
- `operations-en.json`
- `medical-de.json`
- `medical-en.json`

### Purpose

These files contain the content for department subpages.

Example fields:
- `title`
- `subtitle`
- `intro`
- `focusTitle`
- `focusItems`
- `missionExamplesTitle`
- `missionExamples`
- `cultureTitle`
- `cultureText`
- optional extras such as `systemsTitle`, `projectsTitle`, `noteTitle`

---

## Images

### Department logos

Path:

```text
public/images/departments/
```

Examples:
- `public/images/departments/engineering.png`
- `public/images/departments/science.png`

Important:
- logos should be tightly cropped
- too much transparent padding makes them look smaller than they really are
- the real issue is often inside the PNG, not in the CSS

Logo assignment is currently handled in:

```text
src/pages/[lang]/departments/[department].astro
```

Inside the `departmentLogos` object.

---

## Cori status system

### Purpose

The status panel on the landing page shows the current condition of the ship.

Current fields:
- hull integrity
- warp core status
- long-range sensors
- ship status
- current location

---

### `src/data/ship-status-profiles.json`

Contains all available status profiles.

Current profiles:
- `mission`
- `drydock`
- `standby`
- `patrol`
- `transit`
- `orbit`
- `systemcheck`
- `diplomatic`

Each profile contains:
- a German value set
- an English value set

---

### `src/data/ship-status.json`

Controls the currently active state.

Changed here:
- `activeProfile`
- optional `locationOverride.de`
- optional `locationOverride.en`

Example:

```json
{
  "activeProfile": "mission",
  "locationOverride": {
    "de": "Nahe Deep Space 9",
    "en": "Near Deep Space 9"
  }
}
```

If `locationOverride` stays empty, the website uses the default location from the chosen profile.

---

### `src/data/ship-status.README.txt`

Documentation for the status system.

Contains:
- which fields may be changed
- which profile values are valid
- example configurations

---

## Current design state

The site is currently:
- multilingual
- modular
- Starfleet-inspired in tone
- visually modern instead of strict LCARS
- using a subtle animated space background

Important design decisions:
- LCARS inspired, not copied 1:1
- focus on calm sci-fi aesthetics
- clickable department pages
- logos as strong visual markers

---

## Open or later points

### Landing page
- assign real targets to buttons
- improve the hero media area further
- maybe make the status panel admin-friendly with a dropdown later

### Departments
- show department leadership only if wanted
- department-specific reports, projects, and events
- later content maintenance by department heads

### Crew
- opt-in only
- no unwanted public display
- profile image can be chosen individually
- admin enters the content

### Region 9
- keep it compact
- the Cori remains the main focus

### Future ideas
- Klingon easter egg mode
- admin-friendly status selection
- maintainable department logs
- more real content, less structure work

---

## Working principle for future changes

When adding new things, follow this order:

1. keep the structure clean first
2. then add content
3. keep language and tone consistent
4. avoid unnecessary overengineering
5. finish one thing properly before starting the next

In short:
Do not touch everything at once.
First functional, then pretty, then comfortable.

---

## Recommended next steps

Sensible order:

1. continue building Engineering as the reference page
2. bring Medical, Science, and Operations up to the same standard
3. assign real button targets
4. prepare areas for leadership, projects, and logs
5. plan later content maintenance by department heads

---

## Note

This document is intentionally meant to stay alive.
It should grow with the project instead of being written once and then forgotten.

