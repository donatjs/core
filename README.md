# DonatJS Core

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20282077.svg)](https://doi.org/10.5281/zenodo.20282077)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/donatjs/core)
[![HKI](https://img.shields.io/badge/HKI-EC00202414144-orange.svg)](https://dgip.go.id)
[![Live Demo](https://img.shields.io/badge/demo-live%20preview-blueviolet.svg)](https://donatjs.github.io/core/)


A zero-dependency, JSON-driven client-side router and UI rendering engine for modern web portals.

---

## Description

DonatJS Core (`script.js`) is an ultra-lightweight client-side rendering (CSR) engine that transforms structured data (JSON) into dynamic web interfaces without any build step. It implements a declarative component architecture where page layout and content are defined as plain JavaScript objects (`pages.*`), then rendered to the DOM via a polymorphic dispatch system (`ui.render`). Designed for high-efficiency, zero-dependency deployment in Indonesian educational and institutional web environments where external framework dependencies are a liability.

---

## Key Features

- **Zero dependency** — pure vanilla JavaScript, no npm, no bundler, no build step
- **JSON-driven architecture** — all UI defined as structured data (`pages.*` objects), not markup
- **Micro routing system** — query-string-based dynamic routing with History API support and automatic fallback resolution
- **Polymorphic component dispatch** — `components[section](data)` pattern renders any registered component from data alone
- **Integrated engines** — built-in Quiz Engine, Certificate Verifier, Slide Viewer (PREP-structured), and Dataset Editor
- **Markdown-like line renderer** — supports code blocks, headers, skill bars, timeline steps, tables, and inline forms via `lineRenderer`
- **SVG.js integration** — auto-reinjects icons after dynamic route transitions via `svg.di()`

---

## Prerequisites

No installation required. Any modern browser supporting ES6+ is sufficient.

| File         | Role                                               |
|--------------|----------------------------------------------------|
| `script.js`  | Core engine — router, UI renderer, components      |
| `dataset.js` | Page loader — dynamically injects `pages/*.js`     |
| `svg.js`     | Icon engine — inline SVG injection (optional)      |
| `style.css`  | Base layout and component styles                   |

---

## Quick Start

### 1. Include the files

```html
<link rel="stylesheet" href="style.css">
<link rel="stylesheet" href="svg.css">
<script src="svg.js"></script>
<script src="script.js"></script>
```

### 2. Define a page dataset

```javascript
pages.home = [
    {
        section: 'titleHero',
        title: 'Halo Dunia',
        description: 'Ini adalah konten berbasis JSON-driven.'
    }
];
```

### 3. Initialize navigation

```html
<div id="content"></div>
<script>
  window.addEventListener('load', () => web.navigate());
  window.addEventListener('popstate', () => web.navigate());
</script>
```

---

## Usage

### `web.navigate(slug?)`

Resolves the current route, dispatches to the appropriate resolver or content lookup, and renders into `#content`.

```js
// Navigate programmatically
web.navigate('home');

// Navigate with sub-ID
web.navigate('learn/module-01');
```

### `ui.render(id, dataArray)`

Renders an array of section objects into a DOM element by ID.

```js
ui.render('content', pages.home);
```

### `components[section](data)`

Each section key maps to a render function. Built-in sections:

| Section         | Description                              |
|-----------------|------------------------------------------|
| `hero`          | Full-width hero with badges and CTA      |
| `features`      | Icon + title + description card grid     |
| `article`       | Two-column layout with `lineRenderer`    |
| `titleHero`     | Simple title + description block         |
| `learningModule`| Sidebar + content learning panel         |
| `quizEngine`    | Protected multiple-choice quiz           |
| `certificate`   | Printable certificate display            |
| `slideViewer`   | PREP-structured slide deck               |
| `editor`        | Live dataset editor with preview         |

### Route Resolvers

| Route    | Resolver                  | Behavior                               |
|----------|---------------------------|----------------------------------------|
| `home`   | `resolveContent`          | Renders `pages.home`                   |
| `cert`   | `resolveCertificate`      | Lookup by ID or show verification form |
| `learn`  | `resolveLearningModule`   | Sidebar navigation learning module     |
| `editor` | `resolveEditor`           | Live JSON editor for dataset           |

---

## File Structure

```
donat/
├── script.js     # Core engine — router, components, UI renderer
├── dataset.js    # Page manifest loader
├── svg.js        # SVG icon engine (companion library)
├── svg.css       # SVG icon styles
├── style.css     # Base layout styles
├── index.html    # Entry point
├── pages/
│   ├── index.js  # Page file manifest (pageFiles array)
│   └── home.js   # Home page dataset
├── README.md     # This file
├── CITATION.cff  # Citation metadata (Zenodo / Google Scholar)
└── LICENSE       # MIT License
```

---

## How to Cite

If you use DonatJS Core in academic work, please cite it as:

```bibtex
@software{sismadi_donatjs_2024,
  author    = {Sismadi, Wawan},
  title     = {{DonatJS Core: A Zero-Dependency JSON-Driven Client-Side Router and UI Rendering Engine}},
  year      = {2024},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.20282077},
  url       = {https://github.com/donatjs/core}
}
```

See [`CITATION.cff`](CITATION.cff) for full metadata including related works and references.

---

## License

MIT License © 2024 Wawan Sismadi / PT Sismadi Langit Solusi

---

## Author

**Wawan Sismadi**
NIDN: 0816087703 · SINTA ID: 6848496 · ORCID: [0009-0007-2685-5663](https://orcid.org/0009-0007-2685-5663)
Lecturer, Universitas IPWIJA · Doctoral Candidate, Universitas Ahmad Dahlan
Founder, PT Sismadi Langit Solusi · [sismadi.com](https://sismadi.com)
