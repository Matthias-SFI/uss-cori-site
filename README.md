USS Cori Website

Multilingual Astro-based website project for the USS Cori, a chapter within STARFLEET International Region 9.

This project is designed as a modern, Starfleet-inspired website with:

multilingual landing pages
clickable department subpages
structured JSON-based content
department logos
configurable ship status profiles
room for later expansion such as reports, events, leadership info, and department-maintained content
Project Goals

The website is meant to serve as:

a public-facing home for the USS Cori
an introduction for interested visitors
a structured base for future department pages
a maintainable project that can grow without turning into chaos

The design direction is:

modern sci-fi
Starfleet-inspired wording and atmosphere
not a strict LCARS clone
clean, modular, and expandable
Tech Stack
Astro
Astro components
JSON-based content
CSS inside layout/components
Static assets in public/
Project Structure

/
├── public/
│ └── images/
│ └── departments/
│ ├── engineering.png
│ ├── science.png
│ ├── operations.png
│ └── medical.png
│
├── src/
│ ├── components/
│ │ ├── AboutOverview.astro
│ │ ├── DepartmentPage.astro
│ │ ├── Departments.astro
│ │ ├── Footer.astro
│ │ ├── Header.astro
│ │ ├── Hero.astro
│ │ ├── ReadyRoom.astro
│ │ ├── RegionNine.astro
│ │ ├── StatsGrid.astro
│ │ └── TranslationNote.astro
│ │
│ ├── data/
│ │ ├── lang/
│ │ │ ├── de.json
│ │ │ ├── en.json
│ │ │ └── departments/
│ │ │ ├── engineering-de.json
│ │ │ ├── engineering-en.json
│ │ │ ├── science-de.json
│ │ │ ├── science-en.json
│ │ │ ├── operations-de.json
│ │ │ ├── operations-en.json
│ │ │ ├── medical-de.json
│ │ │ └── medical-en.json
│ │ │
│ │ ├── ship-status.json
│ │ │── ship-status-profiles.json
│ │ └── ship-status.README.txt
│ │
│ ├── layouts/
│ │ └── BaseLayout.astro
│ │
│ └── pages/
│ ├── index.astro
│ ├── [lang].astro
│ └── [lang]/
│ └── departments/
│ └── [department].astro
│
├── docs/
│ ├── PROJECT_DOCS_DE.md
│ └── PROJECT_DOCS_EN.md
│
├── package.json
└── README.md

Language Routing

Current main routes:

/de
/en

Department examples:

/de/departments/engineering
/en/departments/engineering
/de/departments/medical
/en/departments/medical
Content Management

Main landing page text is stored in:

src/data/lang/de.json
src/data/lang/en.json

Department-specific page content is stored in:

src/data/lang/departments/

The current ship state is controlled through:

src/data/ship-status.json
src/data/ship-status-profiles.json

ship-status.json defines the active profile and optional location override.

Department Logos

Department logo files are stored in:

public/images/departments/

Important:

tightly crop logo PNGs
too much transparent padding makes logos appear too small
if a logo looks tiny, the problem is often inside the image file, not in the CSS

Logo assignment is currently handled inside:

src/pages/[lang]/departments/[department].astro
Ship Status Profiles

The status panel on the landing page uses predefined profiles such as:

mission
drydock
standby
patrol
transit
orbit
systemcheck
diplomatic

These are defined in:

src/data/ship-status-profiles.json

The currently active state is defined in:

src/data/ship-status.json

Example:
{
"activeProfile": "mission",
"locationOverride": {
"de": "Nahe Deep Space 9",
"en": "Near Deep Space 9"
}
}

If locationOverride is empty, the default profile location will be used.

Development Commands

Run all commands from the project root:

npm install → Install dependencies
npm run dev → Start local development server
npm run build → Build the site for production
npm run preview → Preview the production build locally
npm run astro -- --help → Show Astro CLI help
Current Priorities

Current focus areas for the project:

refine department pages
expand Engineering as the reference page
bring Medical, Science, and Operations to the same level
add real targets to buttons
prepare future support for department-maintained content
keep documentation up to date
Documentation

Detailed project documentation is stored in:

docs/PROJECT_DOCS_DE.md
docs/PROJECT_DOCS_EN.md

The main README should stay relatively short.
Detailed explanations belong in the docs folder.

Notes

This project is intentionally being built in a modular way.

Goals:

avoid giant single-file chaos
keep content editable
make future expansion easier
allow later maintenance without breaking the whole site

The focus of the site is the USS Cori.
Region 9 is part of the context, but should not visually overpower the main identity of the project.

The long-term direction includes:

richer department pages
optional leadership visibility
later department-maintained reports, logs, and project entries
better admin comfort for status handling
a consistent Starfleet-inspired tone across all pages