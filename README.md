# <img src="https://raw.githubusercontent.com/OstinUA/Image-storage/main/Gear-silhouette-of-the-Factorio-logo.png" width="32" valign="middle"> FCT Blueprints Decoder/Encoder <a href="https://github.com/OstinUA"><img align="right" src="https://img.shields.io/badge/OstinUA-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"></a>

![Factorio: 2.0+](https://img.shields.io/badge/Factorio-2.0%2B%20%2F%20Space%20Age-orange?style=for-the-badge)

![Platform: Web](https://img.shields.io/badge/Platform-Web_App-0ea5e9?style=for-the-badge)
[![Frontend: Vanilla JS](https://img.shields.io/badge/Frontend-Vanilla%20JS-F7DF1E?style=for-the-badge&logo=javascript&logoColor=111111)](script.js)
[![Styles: CSS3](https://img.shields.io/badge/Styles-CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](style.css)
[![Markup: HTML5](https://img.shields.io/badge/Markup-HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](index.html)
![Status: Active](https://img.shields.io/badge/Status-Active-22c55e?style=for-the-badge)
![Coverage: Manual](https://img.shields.io/badge/Coverage-Manual%20Validation-lightgrey?style=for-the-badge)
[![i18n](https://img.shields.io/badge/i18n-multi--language-2ea44f?style=for-the-badge)](#features)

A production-practical, zero-backend utility for Factorio players who need to inspect blueprint payloads, tweak JSON, update blueprint book metadata, and ship the encoded string back into the game loop fast.

> [!IMPORTANT]
> This project is designed as a client-side tool. All transformations happen in your browser session.

## Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Technical Notes](#technical-notes)
  - [Project Structure](#project-structure)
  - [Key Design Decisions](#key-design-decisions)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Testing](#testing)
- [Deployment](#deployment)
- [Usage](#usage)
- [Configuration](#configuration)
- [License](#license)
- [Community and Support](#community-and-support)
- [Support the Development](#support-the-development)

## Features

- **Blueprint decode/encode pipeline**: transforms Factorio blueprint strings into readable JSON and back.
- **In-browser JSON editing** via CodeMirror, including syntax-aware editing and readable formatting.
- **Search/replace workflow** for large JSON payload surgery.
- **Blueprint book support** with dedicated metadata editing (label, description, active icon set).
- **Icon tooling** with selectable icon data mapped to game entities/items.
- **Local history cache** for recently processed blueprint payloads.
- **Clipboard export path** for encoded results to quickly paste back into Factorio.

> [!TIP]
> If you’re iterating on megabase templates, use history + search/replace together to do bulk JSON edits with less copy-paste churn.

## Technology Stack

- **Languages**: HTML5, CSS3, JavaScript (ES6+)
- **Editor component**: CodeMirror 5 (CDN delivered)
- **Execution model**: pure client-side browser runtime (no Node.js service, no backend API)
- **Data handling**: browser memory + local persistence for history
- **UI style**: custom Factorio-inspired theme and layout

## Technical Notes

### Project Structure

```text
.
├── index.html            # App shell, UI sections, tabbed layout
├── style.css             # Theme, layout, and component styling
├── script.js             # Decode/encode logic, editor behavior, history, book metadata tooling
├── README.md             # Project documentation
├── CONTRIBUTING.md       # Contribution process and engineering rules
├── CODE_OF_CONDUCT.md    # Community behavior expectations
└── LICENSE               # GPL-3.0 license
```

### Key Design Decisions

- **Static-first architecture**: the app runs from plain static files, so contributors can debug quickly without complex setup.
- **Client-side processing**: blueprint strings are transformed locally, reducing operational overhead.
- **Single-script orchestration**: core logic is concentrated in `script.js` for direct maintainability in a lightweight repo.
- **CDN-hosted dependencies**: fast bootstrap, but contributors should be aware of third-party availability assumptions.

> [!NOTE]
> Because dependencies are CDN-based, fully offline usage requires vendoring those assets manually.

## Getting Started

### Prerequisites

You only need:

- A modern browser (Chrome, Edge, Firefox, or Safari latest stable).
- Optional for local serving: Python 3.x or any static file server.
- Optional for contribution workflows: Git.

### Installation

```bash
# 1) Clone repository
git clone https://github.com/<your-org-or-username>/blueprints-book-rich_text.git
cd blueprints-book-rich_text

# 2) Quick-start: open directly (works for most local use-cases)
# macOS:
open index.html
# Linux:
xdg-open index.html
# Windows (PowerShell):
start index.html

# 3) Recommended: run via local static server (avoids browser policy edge-cases)
python -m http.server 8080
# Then open http://localhost:8080
```

## Testing

This repo currently has no dedicated automated test suite, so validation is execution-based.

```bash
# Basic syntax sanity check
node --check script.js

# Serve and run manual QA checklist
python -m http.server 8080
# 1) Decode sample blueprint
# 2) Edit JSON and re-encode
# 3) Validate blueprint book metadata editing
# 4) Verify copy/export behavior
```

> [!WARNING]
> If you make parser-related changes, always test both single blueprints and blueprint books. They exercise different paths.

## Deployment

This project is deployable as static assets.

### Option A: GitHub Pages

1. Push repository to GitHub.
2. Enable Pages from repository settings.
3. Select branch and root folder.
4. Publish.

### Option B: Static hosting (Netlify, Cloudflare Pages, Vercel static)

- Build step: **none**
- Publish directory: repository root
- Cache policy: default static caching is usually fine

### Option C: Containerized static serving

```bash
# Example minimal nginx-based static deployment flow
# (Dockerfile not included in this repo by default)
docker build -t fct-blueprints-web .
docker run -p 8080:80 fct-blueprints-web
```

## Usage

```text
# Decode/Encode Flow
1) Paste blueprint string into "Blueprint Decode/Encode" input.
2) Click Decode.
3) Patch JSON in the editor (or run search/replace).
4) Click Encode.
5) Copy encoded output and import into Factorio.

# Blueprint Book Flow
1) Switch to the blueprint book tab.
2) Paste encoded book string.
3) Click Decode Book.
4) Edit label/description/icons.
5) Re-encode and copy result.
```

> [!CAUTION]
> Invalid JSON edits will block re-encoding. Keep JSON structurally valid after modifications.

## Configuration

This project does **not** require a `.env` file out of the box.

Runtime behavior is currently configured by:

- Values hardcoded in `script.js` (icons catalog, metadata handling rules).
- UI/layout definitions in `index.html` and `style.css`.
- Browser runtime context (storage, permissions, clipboard support).

If your team needs environment-specific behavior, add a config layer (for example `config.json`) and load it during app bootstrap.

## License

This project is distributed under the **GNU GPL v3.0** license. See [`LICENSE`](LICENSE) for legal details.

## Community and Support

Project created with the support of the FCTostin community.

[![YouTube](https://img.shields.io/badge/YouTube-Channel-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@FCT-Ostin)
[![Telegram](https://img.shields.io/badge/Telegram-Join_Chat-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/FCTostin)
[![Steam](https://img.shields.io/badge/Steam-Join_Group-1b2838?style=for-the-badge&logo=steam&logoColor=white)](https://steamcommunity.com/groups/FCTgroup)

## Support the Development

[![Patreon](https://img.shields.io/badge/Patreon-Support-F96854?style=for-the-badge&logo=patreon&logoColor=white)](https://www.patreon.com/c/OstinFCT)
[![Boosty](https://img.shields.io/badge/Boosty-Donate-F15F2C?style=for-the-badge&logo=boosty&logoColor=white)](https://boosty.to/ostinfct)

## Contacts

- GitHub: [OstinUA](https://github.com/OstinUA)
- Team page: [FCTostin-team](https://github.com/FCTostin-team)
- Contribution process: see [`CONTRIBUTING.md`](CONTRIBUTING.md).
