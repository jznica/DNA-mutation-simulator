# DNA Mutation Simulator

An interactive 3D DNA model in a single HTML file. Set a mutagen (EMS) concentration and exposure time, run one round of exposure and replication, and see:

- which base pairs change on a rotatable 3D double helix
- the new DNA sequence, shown as sequencer-style traces
- what each change does to the protein (silent, missense, nonsense, start lost)
- the probability maths behind every run, with a 5,000-run check against the exact formula

## Run it

No install or build step.

1. Download `index.html`.
2. Open it in Chrome, Edge, Firefox or Safari.

It needs an internet connection the first time, because it loads three.js (the 3D library) from a CDN.

### Host it on GitHub Pages

1. Push `index.html` to the root of your repository.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then save.
4. After a minute the site appears at `https://<your-username>.github.io/<repo-name>/`.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app: layout (HTML), styling (CSS) and logic (JavaScript) |
| `How-It-Works.pdf` | Plain-language guide to the biology, the maths and the code |
| `README.md` | This file |

## How to use it

| Control | What it does |
|---|---|
| Concentration slider | EMS dose in % v/v (0–1%). More violet particles appear around the helix as you raise it. |
| Exposure time slider | Hours of exposure (0–24 h). |
| Display rate | Speeds up mutations for the visual run only (×1 is real). Real rates are about 10⁻⁵ per site, so a short strand would almost never change at ×1. |
| Expose & replicate | Runs one round. Mutagen particles strike the pairs that change. |
| Keep mutant | Makes the mutated strand the new template, so you can run several rounds. |
| Template / Mutant | Switches which strand the 3D model shows. |
| Click a rung | Selects a base pair. Use the A:T / T:A / G:C / C:G buttons to edit it. |
| Sequence box | Paste your own 9–60 base sequence (A, C, G, T). |

Mouse: drag to orbit, scroll to zoom. Touch: drag and pinch. Arrow keys step through base pairs when the 3D view has focus.

## The model in one paragraph

Each base pair gets a hit rate λ. For G:C pairs, λ = μ₀ + k·C·t, where C is concentration, t is time, k = 4.5×10⁻⁶ per (% v/v · h) and μ₀ = 7×10⁻⁹ is the background error rate. A:T pairs only get μ₀, because EMS attacks guanine. The chance a site changes is p = 1 − e^(−λ). EMS hits turn G:C into A:T; background errors follow a 2:1 transition:transversion ratio. k is calibrated so 0.3% EMS for 12 h gives about one mutation per 170 kb, the order of density reported for EMS-treated *Arabidopsis*. Treat it as order-of-magnitude, not a lab constant.
{team of two which is my sister Jerlin which makes this project special}

## Built with

- [three.js r128](https://threejs.org/) for the 3D scene, with its UnrealBloom post-processing pass for the glow
- Plain HTML, CSS and JavaScript (no framework, no build)
