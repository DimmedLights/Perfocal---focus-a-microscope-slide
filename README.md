# Parfocal

Play it at **https://parfocal.vercel.app**

A daily microscope game. Find the specimen at low power, swing in the next objective, add oil for the last one, and lock focus as close to the right plane as you can. Scoring is measured against each objective's real depth of field.

Designed by Destiny, coded with Claude (Anthropic) as a collaborator.

## Modes

- **Brightfield**: Gram- and Ziehl–Neelsen-stained smears of twelve organisms, from *S. aureus* clusters to *Candida* pseudohyphae and gonococci inside neutrophils. Six of them show a real micrograph at 100x. Watch for dust on the coverslip, 170 µm above the smear.
- **Fluorescence**: drawn cultured cells labelled with DAPI, Alexa 488 (tubulin) and phalloidin-568 (actin), or a real three-channel field of HT29 cells (DNA, phospho-histone H3, cell body). Pick the right filter cube for each target and close the shutter to limit photobleaching.
- **Confocal**: thick epithelial organoids with nuclear, membrane-GFP and lysosome layers at different depths. Out-of-focus planes go dark; the pinhole trades brightness against section thickness.

Each mode has a shared daily slide plus random practice slides, timed or timeless play, and a guided tutorial round.

## Controls

- Title menu: ↑ ↓ to choose, Enter to open, Q / E to switch microscope, T for timed or timeless, M for sound, B for music.
- In a round: hold ↑ ↓ for fine focus (it speeds up the longer you hold), Shift + ↑ ↓ for coarse, Enter to lock, O for oil, Esc to pause. The knob's outer ring is coarse and its centre is fine; turning fast travels further.
- The timer sits on the eyepiece: a draining arc on the rim and a plate with the seconds. The last five seconds tick out loud.
- On a phone the knob becomes two drag strips (Coarse and Fine).

## Optics

| Mode | Objectives |
|---|---|
| Brightfield | 10x/0.25 · 40x/0.65 · 100x/1.25 oil |
| Fluorescence | 10x/0.30 · 40x/0.75 · 100x/1.40 oil |
| Confocal | 10x/0.40 · 40x/0.95 · 63x/1.40 oil |

- Depth of field (widefield): λn / NA²
- Optical section (confocal, 1 AU): 0.88 λ / (n − √(n² − NA²))
- Defocus blur: blur-disc diameter 2·Δz·tan θ, with sin θ = NA / n
- The knobs have no steps. Coarse moves 0.8 µm per degree turned slowly and gears up to 6× when you spin fast; fine moves 0.07 µm per degree, up to 4×. A viscous drive (time constant 60–85 ms) delivers each turn to the stage frame by frame, so the image slides continuously through focus.
- Immersion oil sits on the coverslip as a bead about 0.8 mm tall. The front lens wets once the gap is under that, and the column breaks if you lift past 1.6 mm. The loupe zooms out in 3× steps so the lens and bead stay in view.

## Running it

It is a single static page with no build step. Open `index.html` in a browser, or deploy the folder to any static host. The live site deploys from `main` on Vercel.

## Photographs

`images/` holds the real micrographs, and `images/manifest.json` lists each one's author, licence, source page and the edits made (cropping, scale bars painted out). The modified CC BY-SA images are shared under the same licence. Everything else is drawn in code.

## Music

The soundtrack, "Coverslip Lounge", is an original generative jazz loop synthesised live in the browser (electric piano, bass, brushes, vibraphone and a pad). It turns down and muffles while you focus, opens up in menus, and ducks under the victory tune.

## Inspiration

The one-slide-a-day format comes from [dialed.gg](https://dialed.gg). The menus take their energy from *Persona 3 Reload* (Atlus), borrowing ideas only: tilted type, a highlight that slides between choices, and diagonal screen cuts. No Atlus art, type or sound is used.
