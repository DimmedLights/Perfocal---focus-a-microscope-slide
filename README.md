# Parfocal

A daily microscope game. Find the specimen at low power, swing in the next objective, add oil for the last one, and lock focus as close to the right plane as you can. Scoring is measured against each objective's real depth of field.

## Modes

- **Brightfield**: Gram- and Ziehl–Neelsen-stained bacterial smears (six organisms). Watch for dust on the coverslip, 170 µm above the smear.
- **Fluorescence**: cultured cells labelled with DAPI, Alexa 488 (tubulin) and phalloidin-568 (actin). Pick the right filter cube for each target and close the shutter to limit photobleaching.
- **Confocal**: thick epithelial organoids with nuclear, membrane-GFP and lysosome layers at different depths. Out-of-focus planes go dark; the pinhole trades brightness against section thickness.

Each mode has a shared daily slide plus random practice slides, timed or timeless play, and a guided tutorial round.

## Optics

| Mode | Objectives |
|---|---|
| Brightfield | 10x/0.25 · 40x/0.65 · 100x/1.25 oil |
| Fluorescence | 10x/0.30 · 40x/0.75 · 100x/1.40 oil |
| Confocal | 10x/0.40 · 40x/0.95 · 63x/1.40 oil |

- Depth of field (widefield): λn / NA²
- Optical section (confocal, 1 AU): 0.88 λ / (n − √(n² − NA²))
- Defocus blur: blur-disc diameter 2·Δz·tan θ, with sin θ = NA / n
- Coarse focus moves 20 µm per tick, fine focus 0.25 µm.

## Running it

It is a single static page with no build step. Open `index.html` in a browser, or deploy the folder to any static host (for example Vercel).

## Photographic plates (optional)

Specimens are drawn in code. If you add the photographs listed in `images/manifest.json` at the paths given there (for example `images/saureus-gram-01.jpg`), the 100x brightfield view uses the real micrograph and credits it automatically. Check each image's licence on its source page before adding it; CC BY-SA images must stay under the same licence when modified.
