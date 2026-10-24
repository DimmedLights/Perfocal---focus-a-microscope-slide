# Parfocal

Play it at **https://parfocal.vercel.app**

A daily microscope game. Find the specimen at low power, swing in the next objective, add oil for the last one, and lock focus as close to the right plane as you can. Scoring is measured against each objective's real depth of field. A fourth microscope, a scanning electron microscope, runs at its own workstation.

Designed by Destiny, coded with Claude (Anthropic) as a collaborator.

## Modes

- **Brightfield**: Gram- and Ziehl–Neelsen-stained smears of twelve organisms, from *S. aureus* clusters to *Candida* pseudohyphae and gonococci inside neutrophils. Six of them show a real micrograph at 100x. Watch for dust on the coverslip, 170 µm above the smear.
- **Fluorescence**: drawn cultured cells labelled with DAPI, Alexa 488 (tubulin) and phalloidin-568 (actin), or a real three-channel field of HT29 cells (DNA, phospho-histone H3, cell body). Pick the right filter cube for each target and close the shutter to limit photobleaching.
- **Confocal**: thick epithelial organoids with nuclear, membrane-GFP and lysosome layers at different depths. Out-of-focus planes go dark; the pinhole trades brightness against section thickness.

- **SEM**: a scanning electron microscope at its workstation: a monitor running the control software (live scan, data bar, vacuum and column status, histogram) beside a manual control panel. Pump the chamber, choose the beam voltage, turn the beam on, then focus, correct astigmatism and set contrast on each of three fields before a slow-scan photo. Five stubs, each modelled in 3D: mixed pollen, a blood clot, diatom frustules, *S. aureus* on a filter, and a fruit fly's compound eye. Some stubs come uncoated and charge unless the voltage is low.

Each mode has a shared daily slide plus random practice slides, timed or timeless play, and a guided tutorial round.

## Controls

- Title menu: ↑ ↓ to choose, Enter to open, Q / E to switch microscope, T for timed or timeless, M for sound, B for music.
- In a round: hold ↑ ↓ for fine focus (it speeds up the longer you hold), Shift + ↑ ↓ for coarse, Enter to lock, O for oil, Esc to pause. The knob's outer ring is coarse and its centre is fine; turning fast travels further.
- The timer sits on the eyepiece: a draining arc on the rim and a plate with the seconds. The last five seconds tick out loud.
- On a phone the knob becomes two drag strips (Coarse and Fine).
- SEM: ↑ ↓ fine focus, Shift + ↑ ↓ coarse, ← → stigmator X, Shift + ← → stigmator Y, − + magnification, 1–4 scan speed, R reduced area, A auto contrast, Enter photo. On the image, drag sideways to focus, Shift-drag to stigmate, scroll to zoom. The panel's Focus knob has a coarse outer ring and a fine centre.

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

### The SEM

- Magnification is quoted against a 127 mm wide image, rendered at 768 × 576 pixels.
- Beam: a 30 µm final aperture at 5 mm working distance gives a convergence half-angle α = 3 mrad. A surface Δz from the beam crossover is blurred by a spot about 2αΔz across, so the depth of field is roughly ±(1.4 × pixel size)/α: about ±154 µm at ×500 and ±1.5 µm at ×50 000.
- Astigmatism splits the focus into two line foci; the spot is an ellipse whose long axis flips by 90° through focus. The stigmators (X at 0°/90°, Y at 45°/135°) cancel it.
- Focus steps scale with the field width, as on real instruments, so a turn is finer at higher magnification. Focus does not shift with magnification, so you can zoom in to focus and step back.
- Each image is built from a 3D model of the stub. Every pixel's secondary-electron signal follows the secant law (yield rises as the surface tilts), the edge effect (spread over a fraction of the Kanaya–Okayama electron range, so it widens with kV), electrons trapped in crevices, and shadowing toward a side-mounted Everhart–Thornley detector. The GPU then applies the beam's spot at each pixel's height, shot noise for the dwell time, and the detector's contrast and brightness, painting the frame line by line.
- Uncoated insulators charge above about 2 kV (the E2 crossover): bright glow, torn scan lines and drift.

## Scoring

Focus is graded by what you can see, not by raw distance from a target. Each plane of the target is scored by the extra blur it shows on screen (on the confocal, by how much it dims): under 0.7 px of added blur is invisible and costs nothing, and credit halves by 2.2 px. Planes are weighted by how much specimen sits in them, and the total is compared with the sharpest plane that field allows, so a thick patch of smear isn't held to a standard no plane could meet. The verdict draws that sharpness curve with where you locked. Time bonus and technique penalties (coarse above 10x, no oil, wrong cube, bleaching) apply on top.

The SEM uses the same rule on the electron spot: each height in the middle of the field is weighted by how much visible detail sits there, both astigmatic axes are graded by their extra blur, and the photo is compared with the best focus that field allows, with the stigmators corrected. Contrast is read off the photo's histogram (clipped or flat images lose points), and charging or a needlessly high voltage on a coated stub costs points too.

## Running it

It is a single static page with no build step. Open `index.html` in a browser, or deploy the folder to any static host. The live site deploys from `main` on Vercel.

## Photographs

`images/` holds the real micrographs, and `images/manifest.json` lists each one's author, licence, source page and the edits made (cropping, scale bars painted out). The modified CC BY-SA images are shared under the same licence. Everything else is drawn in code.

## Music

The soundtrack, "Coverslip Lounge", is an original generative jazz loop synthesised live in the browser (electric piano, bass, brushes, vibraphone and a pad). It turns down and muffles while you focus, opens up in menus, and ducks under the victory tune.

## Inspiration

The one-slide-a-day format comes from [dialed.gg](https://dialed.gg). The menus take their energy from *Persona 3 Reload* (Atlus), borrowing ideas only: tilted type, a highlight that slides between choices, and diagonal screen cuts. No Atlus art, type or sound is used.
