# CLAUDE.md

This file provides guidance to AI assistants working with this repository.

## Project Overview

A minimal static web app that displays "Hello!" in the 10 most widely spoken world languages. Users click language buttons to switch the greeting with a smooth fade animation.

**Live site:** https://jared-rebel.github.io/hello-world/

## Repository Structure

```
hello-world/
├── index.html   # Entire application — HTML, CSS, and JS in one file
└── README.md    # Project description and language list
```

There is no build step, no package manager, no dependencies, and no framework. The project is a single self-contained HTML file.

## Architecture

Everything lives in `index.html`:

- **HTML** (lines 1–68): Minimal structure — an `<h1>` for the greeting, a `<p>` for the language name, and a `<div>` that receives dynamically created buttons.
- **CSS** (lines 7–61): Inline `<style>` block. Dark theme (`#0f172a` background). Responsive typography using `clamp()`. Pill-shaped buttons with hover/active states.
- **JavaScript** (lines 69–105): Inline `<script>` block. A `greetings` array holds objects with `lang`, `hello`, and `flag` fields. On page load, buttons are created dynamically via `forEach`. Click handlers fade the `<h1>` out, swap its text, then fade it back in using a 150ms `setTimeout`.

### Data structure

```js
const greetings = [
    { lang: 'English',    hello: 'Hello!',     flag: '🇬🇧' },
    // ... 9 more entries
];
```

Languages (in order): English, Mandarin, Hindi, Spanish, French, Arabic, Bengali, Portuguese, Russian, Japanese.

## Development Workflow

No toolchain is required. To run locally, open `index.html` directly in a browser:

```bash
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

Or serve it with any static file server:

```bash
npx serve .
python3 -m http.server 8080
```

## Deployment

The site is deployed via **GitHub Pages** from the `main` branch root. Pushing to `main` automatically updates the live site. No CI/CD pipeline exists.

## Conventions

- **No build step.** Do not introduce bundlers, transpilers, or package managers unless the project scope meaningfully changes.
- **Single file.** Keep HTML, CSS, and JS together in `index.html`. Do not split into separate files without a clear reason.
- **Vanilla JS only.** No frameworks or libraries. All DOM manipulation uses standard browser APIs.
- **Inline styles.** CSS lives in the `<style>` block within `<head>`. No external stylesheets.
- **Data as a JS array.** Language data is stored in the `greetings` array at the top of the `<script>` block. To add a language, append an entry there.

## Adding a Language

To add a new greeting, append an object to the `greetings` array in `index.html`:

```js
{ lang: 'Swahili', hello: 'Habari!', flag: '🇰🇪' },
```

No other changes are needed — the button is generated automatically.

## Git Branches

- `main` — production branch, powers GitHub Pages
- `master` — legacy default branch
- Feature branches use the `claude/` prefix (e.g., `claude/add-claude-documentation-nd7qd`)
