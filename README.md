# Emoji2ASCII

Turn any emoji into a glowing field of ASCII characters, right in your browser.

Type or pick an emoji and Emoji2ASCII rasterizes it, then "paints" the shape with
randomized text — in the emoji's real colors or a single Matrix-style hue. You can
hide words inside the noise, crank the contrast, and export a shareable image that
stays under 1 MB.

It's a single, dependency-free HTML file. No build step, no server, no tracking.

## Demo

Open [`index.html`](index.html) in any modern browser — that's it.

## Features

- **Any emoji** — a built-in emoji keyboard (10 categories) plus a text box so you
  can paste anything your system font can render.
- **Two color modes** — use the emoji's real colors, or switch to a single picked
  color with an automatically derived light→dark palette.
- **Contrast control** — pushes the dark areas darker (with a gentle lift on the
  brights) so shapes read with more punch.
- **Hidden text** — three text modes:
  - *Random characters* — classic Matrix noise.
  - *Spell out words* — your message flows through the shape, readable.
  - *Hidden words* — mostly random, with your words woven in horizontally.
- **Tunable look** — letter size, density, aura/glow strength, canvas size, and a
  seed for reproducible results (same seed → same image).
- **Auto-centered** — the emoji is recentered on its actual pixels, so every glyph
  lands dead-center regardless of its font metrics.
- **Export under 1 MB** — downloads a JPEG, stepping quality (and finally scale)
  down until it fits, so the file is always easy to share.

## Usage

1. Open `index.html` in a browser.
2. Pick an emoji from the ⌨️ keyboard or paste one into the box.
3. Adjust the sliders to taste; toggle **Use emoji colors** for color vs. mono.
4. (Optional) Set a **Text mode** and type a message to embed words.
5. Click **Download JPG** to save the image (always < 1 MB).

> Color and detail look best on systems with a color emoji font (e.g. Apple Color
> Emoji on macOS). On monochrome-emoji systems, the single-color mode works great.

## How it works

1. The chosen emoji is drawn to a small offscreen canvas and its pixels are read.
2. A tight bounding box of the non-transparent pixels is used to recenter and scale
   it into the main canvas.
3. The canvas is walked on a character grid; each cell samples the emoji bitmap —
   covered cells become glyphs colored from the pixel (or the palette), and a
   blurred copy of the silhouette drives a soft, shape-following glow and the
   scattered outer "aura" characters.

All rendering is plain Canvas 2D with a small seeded PRNG (`mulberry32`) for
reproducibility.

## License

[MIT](LICENSE)
