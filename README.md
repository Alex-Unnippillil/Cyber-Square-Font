# Cyber Square: open source display font

![Cyber Square cover](./assets/specimen/cyber-square-cover.png)

<p align="center">
  <a href="#license"><img alt="License: OFL-1.1" src="https://img.shields.io/badge/License-OFL--1.1-blue.svg"></a>
  <img alt="Status" src="https://img.shields.io/badge/status-active-brightgreen.svg">
</p>

A geometric, cyberpunk square typeface designed for UI chrome, headings, logos, terminals, badges, and retro screens. The design emphasizes right angles, strong rhythm, and clear pixel‑grid alignment at small sizes.

**Repository:** [https://github.com/Alex-Unnippillil/Cyber-Square-Font](https://github.com/Alex-Unnippillil/Cyber-Square-Font)

---

## Contents

* [Preview](#preview)
* [Features](#features)
* [Files](#files)
* [Install](#install)

  * [Web self hosting](#web-self-hosting)
  * [Desktop](#desktop)
* [Usage](#usage)
* [Design goals](#design-goals)
* [Character set](#character-set)
* [Building from sources](#building-from-sources)
* [Contributing](#contributing)
* [Versioning](#versioning)
* [Attribution](#attribution)
* [Google Fonts readiness](#google-fonts-readiness)
* [Specimen generation](#specimen-generation)
* [License](#license)

---

## Preview

> Replace the placeholders below with specimen images located in `assets/specimen/`. The file paths already match the links.

<table>
<tr>
<td align="center"><img alt="Cyber Square pangrams" src="./assets/specimen/cyber-square-pangram.png"><br><sub>Pangrams and sizes</sub></td>
<td align="center"><img alt="Cyber Square character set" src="./assets/specimen/cyber-square-charset.png"><br><sub>Character set and accents</sub></td>
</tr>
<tr>
<td align="center"><img alt="Cyber Square UI examples" src="./assets/specimen/cyber-square-ui.png"><br><sub>Badges, labels, and UI</sub></td>
<td align="center"><img alt="Cyber Square numerals" src="./assets/specimen/cyber-square-numerals.png"><br><sub>Numerals and punctuation</sub></td>
</tr>
</table>

---

## Features

* Square, modular geometry with even stroke weight
* Optimized spacing and metrics for headings and UI labels
* Monospace‑friendly figures set for dense layouts
* Clear shapes for common developer glyphs: `{ } [ ] ( ) < > / \ : ; * + - _ =` and `@ # $ % ^ &`
* Hinting for legibility at small pixel sizes

> Planned: stylistic alternates for A, G, 0, 1, I, l; optional dotted zero; arrows; box drawing; power symbols.

---

## Files

```
fonts/
  CyberSquare-Regular.ttf
  CyberSquare-Regular.woff2
  CyberSquare-Bold.ttf            # optional if provided
  CyberSquare-Bold.woff2          # optional if provided
assets/specimen/
  cyber-square-cover.png
  cyber-square-pangram.png
  cyber-square-charset.png
  cyber-square-ui.png
  cyber-square-numerals.png
```

---

## Install

### Web self hosting

Add the font files to `fonts/` and reference them with `@font-face`.

```css
/* Regular */
@font-face {
  font-family: "Cyber Square";
  src: url("/fonts/CyberSquare-Regular.woff2") format("woff2"),
       url("/fonts/CyberSquare-Regular.ttf") format("truetype");
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}

/* Bold - if included */
@font-face {
  font-family: "Cyber Square";
  src: url("/fonts/CyberSquare-Bold.woff2") format("woff2"),
       url("/fonts/CyberSquare-Bold.ttf") format("truetype");
  font-weight: 700;
  font-style: normal;
  font-display: swap;
}
```

### Desktop

* Windows: right click the `.ttf` file and choose Install
* macOS: open the `.ttf` in Font Book and choose Install
* Linux: copy `.ttf` to `~/.local/share/fonts/` then run `fc-cache -f -v`

---

## Usage

```html
<link rel="preload" as="font" type="font/woff2" href="/fonts/CyberSquare-Regular.woff2" crossorigin>
<style>
  :root { --cyber: "Cyber Square", system-ui, sans-serif; }
  .headline { font-family: var(--cyber); letter-spacing: 0.02em; }
  .label { font-family: var(--cyber); text-transform: uppercase; }
</style>

<h1 class="headline">CYBER SQUARE</h1>
<p class="label">System Ready</p>
```

---

## Design goals

* Readable square forms with consistent counters
* Stable rhythm across Latin basics and punctuation
* Strong grid fit for pixel‑aligned UI and small sizes
* Simple outlines for reliable hinting and low file size

---

## Character set

Latin Basic, Latin-1 Supplement, and punctuation for common developer and UI use. Accents cover English, French, German, Spanish, Portuguese, Italian, and Nordic basics. If you need more accents or symbols, open an issue.

---

## Building from sources

If this repository includes UFO or design files, you can build with \[fontmake] or \[FontForge]. Place the resulting TTF and WOFF2 files in `fonts/`.

* FontForge: open the source, generate `TrueType` and `WOFF2`
* fontTools: `ttx` and `woff2_compress` for postprocessing

> If you want a repeatable build, add a `Makefile` or `scripts/build.sh` and lock tool versions.

---

## Contributing

Issues and pull requests are welcome. Please include screenshots of the glyphs in context, the source you edited, and the build command you used. Keep kerning and spacing changes in separate commits from shape edits.

---

## Versioning

Follow semantic tags: `vMAJOR.MINOR.PATCH` for releases. Record changes in `CHANGELOG.md` with screenshots when shapes change.

---

## Attribution

* Design: **Alex Unnippillil**
* Project: Cyber Square
* Copyright: 2025 The Cyber Square Project Authors

Reserved Font Name: "Cyber Square"

---

## Google Fonts readiness

This project targets OFL-1.1 and a clean name table with the Reserved Font Name. For Google Fonts review, prepare:

* OFL-1.1 with correct copyright holder and Reserved Font Name
* Consistent naming across TTF and WOFF2
* Proper vertical metrics and usWinAscent/Descent to avoid clipping
* Clean outlines, no open contours, no overlapping points where not desired
* Hinting set or autohinted with ttfautohint
* Basic specimen images and README

Open an issue marked `gfonts` if you would like help running the standard checks.

---

## Specimen generation

If you want to recreate the PNGs above locally, you can use Python and Pillow.

```bash
pip install pillow freetype-py
```

```python
# scripts/generate_specimens.py
from PIL import Image, ImageDraw, ImageFont

W, H = 1600, 900
bg = "#0b0f14"; fg = "#e6f1ff"
font = ImageFont.truetype("fonts/CyberSquare-Regular.ttf", 96)
img = Image.new("RGB", (W, H), bg)
d = ImageDraw.Draw(img)
text = "CYBER SQUARE\nThe quick brown fox jumps over 13 lazy dogs."
d.multiline_text((80, 120), text, font=font, fill=fg, spacing=20)
img.save("assets/specimen/cyber-square-pangram.png")
```

---

## License

This font is licensed under the **SIL Open Font License, Version 1.1**. You can use, study, modify, and redis
