# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A birthday ecard for Dad — a single-page web app (HTML/CSS/JS) featuring a photo montage filmstrip slideshow with a WebGL2 animated vortex hero background, personal message section, and embedded video.

## Architecture

**Single HTML file** (`index.html`) with all CSS and JS embedded inline. No build tools, no bundler, no framework — pure vanilla HTML/CSS/JS for maximum portability. The card is opened directly in a browser via `file://` or any static server.

### Key Sections in index.html
- **WebGL2 Vortex Hero** — GLSL fragment shader rendered on a `<canvas>`, warm gold/amber palette, with dark overlay for text readability. Pauses rendering when scrolled off-screen.
- **Filmstrip Slideshow** — 18 photo slides + 1 video slide with crossfade transitions, auto-advance, keyboard/swipe/arrow/dot navigation. Film sprocket design elements.
- **Personal Message** — Typography section with Google Fonts (Playfair Display, Lora, Dancing Script).
- **Footer**

### Design System (CSS Custom Properties)
- Colour palette: warm dark bg (`#1A1510`), golds (`#FFD054`, `#FFC22E`), burgundy (`#8B1A1A`), cream text (`#FFF8E8`)
- Fonts: Playfair Display (display headings), Lora (body), Dancing Script (decorative accents)
- All defined in `:root` variables at the top of `<style>`

### File Structure
```
birthday-card-re-write/
├── index.html          ← the ecard (single self-contained file)
├── photos/             ← 18 family photos (JPG/PNG, mostly portrait)
└── video/              ← 1 video (MOV)
```

## Tools Installed

- **ImageMagick** (`brew install imagemagick`) — for photo resizing/processing via CLI
- **Designer Skills** — Claude Code slash commands copied to `~/.claude/commands/`:
  - `/color-palette` — generate colour systems
  - `/design-screen` — design screen layouts
  - `/type-system` — create typography systems
  - `/design-interaction` — plan animations/transitions
  - `/build-presentation` — structure presentations

## Development

To preview: open `index.html` in any browser, or run a local server:
```bash
cd "/Users/athenoula/claude things/birthday card re-write"
python3 -m http.server 8000
# Then open http://localhost:8000
```

A local server is needed if the browser blocks local `file://` access for video/images (CORS).

## Key Decisions

- **No React/framework** — keeps it as a single shareable HTML file, no build step
- **WebGL2 shader** — extracted from a React `psychedelic-vortex-hero` component, converted to vanilla JS. Uses IntersectionObserver to pause when off-screen.
- **Portrait aspect ratio (3:4)** for slideshow — most photos are portrait orientation
- **Filmstrip max-width 600px** — prevents the portrait slideshow from being excessively tall on desktop
- **Google Fonts via CDN** — requires internet connection to load fonts

## Phase 2 Plans

The next phase will add:
1. **In-browser editor** — edit text, captions, add/remove/reorder photos without touching HTML
2. **Collaborative sharing** — share an editable link so others can contribute photos and edit text
3. **Publish/share** — generate a shareable link to the finished (read-only) ecard
