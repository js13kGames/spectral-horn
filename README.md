# ✨ Spectral Horn 🦄🔬
> *When theoretical optics, procedural rendering, crystal unicorns, and an unforgiving 13-kilobyte limit collide.*

[![JS13kGames](https://img.shields.io/badge/JS13kGames-2026-ff0055.svg?style=flat-square)](https://js13kgames.com)
[![Bundle Size](https://img.shields.io/badge/size-%E2%89%A4%2013%20KB%20(ZIP)-brightgreen.svg?style=flat-square)](#-how-on-earth-did-this-fit-in-13-kb)
[![Physics](https://img.shields.io/badge/optics-Snell%20%2B%20Cauchy%20%2B%20TIR%20%2B%20Alchemy-blueviolet.svg?style=flat-square)](#-physics-under-the-hood-why-light-is-genuinely-awesome)
[![Levels](https://img.shields.io/badge/levels-17%20puzzles%20%2B%20sandbox-gold.svg?style=flat-square)](#-gameplay--the-17-level-odyssey)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)

---

## 🧐 What's the Big Idea?

In 1666, Sir Isaac Newton stuck a glass prism into a sunbeam and discovered that white light is secretly a chaotic party of rainbow colors combined. 

Naturally, we asked the only logical follow-up question of modern science: **What if, instead of a prism, we used a unicorn horn?**

**Spectral Horn** is a 2D optical physics puzzle game handcrafted for the **[js13kGames](https://js13kgames.com/)** competition. No bloated game engines, zero megabytes of textures, zero pre-recorded audio files, and strictly zero pre-rendered fakery. Every single ray of light—from Cauchy wavelength dispersion to Total Internal Reflection (TIR), Dove prism inversions, and spherical lens focusing—is computed analytically in real time on your CPU and rendered with the pure HTML5 Canvas 2D API.

### 🏆 js13kGames Contest Assets

Both assets are 100% in-game captures rendered in real time by the procedural Canvas 2D engine, optimized strictly within the js13k submission constraints:

| Cover Image (`800 × 500 px`, $\le$ 256 KB) | Thumbnail (`320 × 320 px`, $\le$ 64 KB) |
| :---: | :---: |
| [![Cover](assets/cover.png)](assets/cover.png) | [![Thumbnail](assets/thumbnail.png)](assets/thumbnail.png) |
| *Panoramic hero composition: horn dispersion, mirror reflection, spherical orb focus, and charged sensors*<br>`208 KB` (81% of 256 KB limit) | *Square icon: pure Snell's law refraction, Cauchy dispersion, and the procedural celestial unicorn*<br>`54 KB` (84% of 64 KB limit) |

> [!TIP]
> **Asset Optimization:**  
> To preserve delicate optical dispersion gradients and rainbows without color banding or speckled noise in dark backgrounds, assets are quantized into an optimal 256-color palette using **Atkinson error diffusion** and crushed losslessly with **ECT** (`ect -9 -strip`).

---

## 🎮 Gameplay & The 17-Level Odyssey

### Controls & Steering
- **Move Unicorn:** Click / touch and drag the unicorn's body.
- **Rotate Horn:** Drag the circular **Orbit Ring** surrounding the horn.
- **Micro-Nudge:** Click the **`↺` and `↻` Step Buttons** for precise $0.5^\circ$ angle fine-tuning.
- **Touch-Friendly:** Built-in vertical touch offset ensures your thumb never covers the unicorn while dragging on mobile/tablets.
- **Level Select & Reset:** Jump to any unlocked level or hit Reset if you get stuck in an optical labyrinth.
- **Audio Controls:** Independent toggles for ambient generative music and crystalline sound effects.

### Level Campaign
1. **First Horn** — *Snell's law primer: steer green light into the photodiode.*
2. **Prismatic Party** — *Disperse white light to satisfy three color sensors simultaneously.*
3. **Obsidian Shield** — *Flip the horn upside down to clear high dark barriers.*
4. **Periscope Trick** — *Exceed the critical angle for internal reflection.*
5. **Celestial Mirror** — *Bank light off chrome mirrors into target diodes.*
6. **Upside-Down Rainbow** — *Mirror bounces that flip the entire color spectrum.*
7. **Cosmic Trickshot** — *Floor bounces into multi-target splits.*
8. **Hall of Mirrors** — *Complex multi-surface reflection mazes.*
9. **Enter the Dove** — *Introducing the Dove prism: flips color order with zero beam deflection.*
10. **Prismatic Inversion** — *Disperse the spectrum, then flip it with the Dove.*
11. **Crystal Orb** — *Harness spherical converging optics to focus divergent light.*
12. **Squeeze & Scatter** — *Focusing and redirecting multi-beam arrays.*
13. **Additive Alchemy: Yellow** — *Synthesize yellow light by overlapping Red and Green photons.*
14. **Dual Synthesis** — *Orb-expanded blue light bridging composite chromatic targets.*
15. **Great Recombination** — *Use a second horn to undo dispersion and synthesize pure White light.*
16. **Prismatic Ensemble** — *Horn + Mirror + Orb combos.*
17. **Grand Optical Symphony** — *The ultimate test: all instruments on deck to illuminate the cosmos!*
* **+ Cosmic Sandbox** — *Freely experiment with light, prisms, and physics on the interactive title screen!*

---

## 🌈 Physics Under the Hood (Why Light is Genuinely Awesome)

The optics in this game are not an arcade approximation like “red bounces right because video games”. Every single ray obeys the actual laws of wave and geometric optics.

### 1. Snell's Law of Refraction (Snell-Descartes)
At each boundary interface (air $\leftrightarrow$ unicorn horn), the angle of refraction follows:

$$n_1 \sin(\theta_1) = n_2 \sin(\theta_2)$$

In vector form, for an incident unit vector $\vec{v}$ and surface normal $\vec{n}$, the refracted direction $\vec{r}$ is calculated as:

$$\vec{r} = \eta \vec{v} + \left(\eta (\vec{n} \cdot (-\vec{v})) - \sqrt{1 - \eta^2 (1 - (\vec{n} \cdot (-\vec{v}))^2)}\right) \vec{n}$$

where $\eta = \frac{n_1}{n_2}$. If the expression under the radical drops below zero, nature triggers...

### 2. Total Internal Reflection (TIR)
When light travels from an optically denser medium (crystal horn, $n \approx 1.52$) into a rarer one (air, $n = 1.0$) at an angle steeper than the critical angle:

$$\theta_c = \arcsin\left(\frac{n_2}{n_1}\right)$$

light cannot escape the crystal and bounces back inside with **100% efficiency** and zero loss of energy. This exact principle powers modern fiber-optic internet, submarine periscopes—and in our game, trick levels where you must trap light inside a horn to steer it around dark obsidian barriers.

### 3. Cauchy's Dispersion Equation (How Rainbows are Born)
Why does white light split into a spectrum inside the horn? Because the refractive index $n$ **is not constant for all colors**!

We simulate this with Cauchy's empirical dispersion formula:

$$n(\lambda) = n_{\text{base}} + \frac{B}{\lambda^2}$$

- **Violet light** ($\lambda \approx 400\text{ nm}$) has a shorter wavelength $\implies$ **higher refractive index** $\implies$ **bends more sharply**.
- **Red light** ($\lambda \approx 700\text{ nm}$) has a longer wavelength $\implies$ **lower refractive index** $\implies$ **bends more gently**.

Thanks to this physical phenomenon, a single compact white beam (composed of dozens of discrete wavelengths $\lambda \in [400, 700]\text{ nm}$) fans out into a continuous, vibrant spectral rainbow.

### 4. Wavelength to sRGB Mapping (CIE Colorimetry)
Every ray in the game carries a physical wavelength $\lambda$ in nanometers. To display on computer screens, the wavelength is mapped to human color perception (sRGB tristimulus approximation based on Dan Bruton's piecewise curves) with non-linear gamma correction ($\gamma = 0.8$) and smooth perceptual luminosity falloff at spectral boundaries (380 nm and 750 nm).

### 5. Additive Optical Alchemy & HSV Sensing
Unlike mixing paint (subtractive color), light is **additive**:
- Red ($\sim 660\text{ nm}$) + Green ($\sim 535\text{ nm}$) additively combine into radiant **Yellow** ($\sim 580\text{ nm}$).
- Red + Green + Blue recombine back into pure **White** light!

Our target sensors integrate incoming photon flux in real time and evaluate the perceived hue and saturation in HSV color space. If a puzzle demands Yellow, you can hit it with a pure 580 nm amber beam *or* synthesize it by overlapping Red and Green rays!

---

## 🔬 The Optical Arsenal

Across the 17 levels, you will command a full laboratory of celestial optical components:

| Component | Visual | Optical Function |
| :--- | :---: | :--- |
| **🦄 The Unicorn Horn** | Crystalline Prism | Asymmetric triangular prism that bends light and disperses white beams into full-spectrum rainbows via Cauchy dispersion. |
| **🕊️ The Dove Prism** | Trapezoidal Glass | Flips and inverts the spectral stack (turning red-on-top into violet-on-top) with **zero net angular deflection**. |
| **🔮 The Crystal Orb** | Spherical Lens | Converging circular optics that focus divergent beams into tight pinpoints or expand them into wide washes. |
| **🪞 Chrome Mirror** | Specular Reflector | Pure $100\%$ specular reflection surface. Flips ray geometry and color order across bounce angles. |
| **🧱 Obsidian Shield** | Monolithic Barrier | Absorbs all incident photons. Forces you to find clever periscope paths and ceiling bounces. |
| **🎯 Spectral Sensor** | Photodiode Ring | Demands a specific wavelength or composite hue. Requires a steady photon stream to charge up to $100\%$ and lock. |

---

## 🎨 Engine Architecture & Procedural Aesthetics

When you have a 13-kilobyte budget for code, sound, levels, physics, and visuals, importing Three.js or heavy assets is out of the question.

```
       [ 48–72 Spectral Rays with varying λ ∈ [400, 700] nm ]
                                │
                                ▼
       ┌─────────────────────────────────────────────────┐
       │             Analytical 2D Raytracer             │  (Up to 24 bounces / refractions per ray)
       └─────────────────────────────────────────────────┘
                                │
                      ┌─────────┴─────────┐
                      ▼                   ▼
                 Pass 1: Bloom       Pass 2: Core
                 (Soft wide glow,    (Sharp radiant beam,
                  atmospheric aura)   intense core)
                      │                   │
                      └─────────┬─────────┘
                                ▼
       [ ctx.globalCompositeOperation = 'lighter' ]  ==>  ✨ True Additive Photon Mixing
```

1. **Real-time Analytical 2D Raytracer:**
   - Exact mathematical intersections of rays $\vec{P}(t) = \vec{O} + t\vec{D}$ with polygon edges and circular lenses using vector algebra, cross products, and quadratic discriminants.
   - Recursive ray tracing up to **24 bounces/refractions** per ray across dozens of wavelengths at a rock-solid **60 FPS**.

2. **Additive Light Blending (`globalCompositeOperation = 'lighter'`):**
   - Rays are rendered in dual passes (atmospheric Bloom + radiant Core).
   - Dispersed rays naturally recombine at focal points into brilliant white light.

3. **Procedural Unicorn Silhouette & Upside-Down Fluttering:**
   - Generated entirely with mathematical Bézier curves, dynamic gradient shading, and ambient stardust particles.
   - Featuring floating breathing rhythms, a swishing celestial tail, and **four animated paddling legs** that kick into dynamic fluttering whenever you flip the unicorn upside down!

4. **Procedural Web Audio Synthesis:**
   - 0 bytes of audio files! Ambient 4-chord generative progressions, crystalline bell scale rotation harmonics, smooth dragging whooshes, sensor charging pulses, and triumph fanfare arpeggios synthesized on the fly via the Web Audio API.

---

## 🗜️ How on Earth Did This Fit in 13 KB?

The JS13k competition limit is strictly **13,312 bytes** in a `.zip` archive. Fitting a full analytical 2D raytracer, 17 handcrafted levels, procedural vector rendering, and a real-time Web Audio synthesizer requires wringing out every single bit:

| Step | Tool | What it does |
| :--- | :--- | :--- |
| **1. Bundle** | `esbuild` | Compiles TypeScript into a clean, tree-shaken IIFE JavaScript bundle. |
| **2. JS Minify** | `terser` | 20 aggressive passes with `unsafe_math`, `pure_getters`, and property name mangling. |
| **3. CSS Minify**| `csso` | Structural optimization and style minification. |
| **4. Inlining** | `html-minifier-terser` | Strips redundant attributes and whitespace from the HTML skeleton. |
| **5. Crushing** | `roadroller` | Squeezes HTML, CSS, and JS into a single self-extracting JS payload. |
| **6. Ultra ZIP** | `ect` (Enhanced Compression Tool) | Maximum DEFLATE compression with stripped zip metadata (`-9 -strip`). |

The build script packages the entire game into `dist/spectral-horn.zip`, automatically calculating the exact byte budget and ensuring the final archive lands right under the 13 KB threshold.

---

## 🚀 How to Run Locally

### Prerequisites
- [Node.js](https://nodejs.org/) $\ge$ 18
- npm

### Installation & Development
```bash
# 1. Clone repository
git clone https://github.com/your-username/spectral-horn.git
cd spectral-horn

# 2. Install dependencies
npm install

# 3. Start local development server
npm run dev
```
Open `http://localhost:5173` in your browser.

### Building the JS13k Production ZIP
```bash
npm run build
```
The optimized archive will be generated at `dist/spectral-horn.zip`. The build script verifies your byte count against the strict 13,312 byte limit.

### Optimizing Contest Assets
```bash
node scripts/optimize-assets.ts
```
Processes raw captures (`*-original.png`) in `assets/` to satisfy strict js13k size constraints while retaining high color fidelity.

---

## 📜 License

This project is licensed under the [MIT](LICENSE) License.

---
<p align="center">
  <i>“Nature does not conceal her secrets through malice, but through her own grandeur.”</i><br>
  — Albert Einstein (almost certainly while experimenting with unicorns, prisms, and roadroller compression) ✨🦄
</p>
