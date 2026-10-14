# The Photonics Bench

An interactive optics and photonics laboratory that runs in a browser. Drag lasers,
lenses, prisms and interferometer arms onto a 25 mm breadboard and every beam is
ray-traced live — real Snell refraction, real dispersion, real interference.

**Live:** https://thephotonicsbench.com *(replace with your URL)*

---

## What it does

- **19 optical components** — lasers and white sources, flat and curved mirrors,
  beamsplitters, thin lenses, polarisers, waveplates, prisms, gratings, ND and
  bandpass filters, slits, irises, screens and power meters.
- **Two modes.** A flat top-down bench, and a full 3D bench with an orbit camera
  where every part has a height and a tilt — so periscopes, two-level beam routing
  and screens that image in two dimensions all work.
- **19 ready-made experiments**, each with a written brief covering the background,
  the concept, and what to try.
- **A guided tour and 10 build-it-yourself challenges**, graded by measuring the
  simulated light rather than by checking which buttons were pressed.

## The physics

Each ray carries a position, a direction, a vacuum wavelength, a Jones vector for
polarisation, and the optical path length accumulated so far.

| | |
|---|---|
| Refraction | Snell's law with total internal reflection |
| Dispersion | 3-term Sellmeier for N-BK7, N-SF11 and fused silica; Cauchy for PMMA |
| Polarisation | Jones vectors carried in a per-ray transverse basis, decomposed into s and p at each surface |
| Interference | Complex field amplitudes summed per wavelength at every detector |
| Diffraction | Grating orders, and slit fans with the correct sinc² envelope (2D mode) |

Fringes, spectra and focal spots are computed results, not drawn effects.

## Validation

The simulator's output was checked against closed-form predictions:

| Test | Simulated | Theory |
|---|---|---|
| Malus's law, 0–90° | exact | I₀cos²θ |
| Michelson fringe pitch | 0.867 mm | 0.906 mm |
| Mach–Zehnder fringe pitch | 0.600 mm | 0.604 mm |
| Young's fringes, d = 0.2 mm | 1.524 mm | 1.582 mm |
| Grating order m = ±1, 550 nm | ±41.4 mm | ±41.4 mm |
| Tilted slab displacement | 4.150 mm | 4.151 mm |
| Lens focal spot | minimum at z = f | f = 100 mm |

The 2D and 3D engines were written independently. Constrained to a single plane they
agree with each other to about 1 part in 10¹⁶ — stronger evidence than either engine
passing its own tests, since they cannot share a bug.

27 automated test suites cover the physics, the UI flows, every challenge's intended
solution, and 13 deliberately incorrect setups that must fail.

## What it deliberately does not model

- **No Fresnel coefficients.** Glass faces use a flat transmission with no angle or
  polarisation dependence, so there is no Brewster angle and no ghost reflections.
  Total internal reflection *is* modelled.
- **Geometric rays, not Gaussian beams.** No waist, Rayleigh range or diffraction
  limit in free propagation — a perfect lens focuses to a mathematical point.
- **Ideal thin lenses.** No spherical aberration, coma or astigmatism. Chromatic
  aberration *is* available, because it follows from n(λ).
- **Diffraction is 2D-only.** The double slit and single slit live in the flat mode;
  the 3D bench carries the other 17 components.

## Running it

It is one self-contained HTML file. Open `index.html` in any modern browser — no
install, no server, no build step. The only network request is the Google Fonts
stylesheet; everything else is inline.

## Deploying

Any static host works. The file needs no build step and no server-side code.

```
index.html     the entire application
.nojekyll      tells GitHub Pages to serve files as-is
robots.txt
```

## Licence

MIT
