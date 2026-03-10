# Electromagnetic Knot Visualizer

Real-time 3D CUDA/OpenGL visualization of exact Hopfion and Bateman torus-knot solutions of Maxwell's equations, rendered as moving field-line families inside an energy-density halo with a free-fly camera.

This project started as a visual question: if electromagnetic knots are real mathematics, what do they actually look like in motion? The answer is interesting on its own, and it also makes one point much clearer: these structures are compelling topology, but they do not look like the most plausible explanation for ordinary ball lightning reports.

## What This Repo Does

- Evaluates the exact vacuum Hopfion field using the Bateman / Riemann-Silberstein construction.
- Evaluates the exact Bateman torus-knot family `F = nabla alpha^p x nabla beta^q`.
- Renders two different Hopfion views:
  - `FIELD LINES`: traced instantaneous electric and magnetic field-line families.
  - `TOPOLOGY`: direct Hopf-fibration circles, useful for seeing the linked-circle structure cleanly.
- Uses CUDA/OpenGL interop for the line data, with a volumetric halo, bloom, filters, HUD, and mouse-look camera.

## Build

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DCMAKE_CUDA_ARCHITECTURES=86
cmake --build build -j
```

## Run

```bash
./build/em_loop
./build/em_loop --quality high
./build/em_loop --preset trefoil
./build/em_loop --field torus --p 2 --q 3
```

Available quality presets: `low`, `medium`, `high`, `ultra`  
Available field modes: `hopfion`, `torus`  
Available named presets: `hopfion`, `trefoil`, `cinquefoil`, `linked-rings`

## Controls

- `W`, `A`, `S`, `D`: move on the horizontal plane
- `Q`, `E`: move down / up
- Mouse: look around
- `Shift`: move faster
- `Tab`: toggle mouse capture
- `R`: reset camera and simulation time
- `1`, `2`, `3`: switch between `hopfion`, `trefoil`, and `cinquefoil`
- `T`: in `hopfion`, toggle between `FIELD LINES` and `TOPOLOGY`
- `F`: cycle post-process filters, including `OFF` and `NO GLOW`
- `Escape`: quit

## Research Background

The mathematically serious part of this repo is the field evaluator. Hopfions and related torus-knot fields are exact vacuum solutions of Maxwell's equations built from Bateman variables. In the Hopfion case, the field-line structure is tied to the Hopf fibration: the electric-field family and magnetic-field family each form closed loops on nested tori, with nontrivial helicity encoded in the linking of those loops.

That is why the visual language of this repo is nested tori, linked circles, and torus-knot families. The code is not inventing those shapes from scratch. It is sampling exact field expressions and then choosing a rendering strategy that makes the topology legible.

The important caveat is equally important: this is still a visualization layer, not a general Maxwell solver. The halo, bloom, color grading, time scaling, seeding strategy, and line styling are chosen for legibility and frame time. The underlying field formulas are exact; the presentation is interpretive.

## Ball Lightning Takeaway

After building this renderer and comparing it against the literature, the working conclusion behind this repo is:

- Electromagnetic knots are real Maxwell/topology research and are worth visualizing in their own right.
- They are not the leading explanation for most natural ball lightning reports.
- The best-supported explanation today is still some form of material plasma: dusty plasma, aerosol plasma, or chemically sustained plasma created when lightning interacts with soil, air chemistry, or other matter.

Why that conclusion?

- The strongest natural evidence is still the 2012 instrumented observation reported by Cen, Yuan, and Xue, where the spectrum contained silicon, iron, and calcium consistent with soil material.
- Exact vacuum Hopfions propagate at the speed of light and are not naturally "parked" glowing balls.
- Ball lightning reports often behave like a physical blob: drifting, fading, exploding, sometimes leaving residue, and sometimes appearing near conductive structures or aircraft.

This repo's practical conclusion is that there are at least two serious physical buckets worth keeping in mind:

- Ground/material events:
  Lightning strikes soil or other material, ejects hot particles and plasma, and the glow persists through oxidation, recombination, and residual electrical driving.
- Airborne/electrically driven events:
  Plasma near storms or aircraft can be maintained or steered by local electric fields, ionized aerosols, convection, and turbulence without requiring a pure self-trapped electromagnetic knot.

That last point matters because plasma does not have to move like a simple hot gas blob. In microwave plasma experiments it can wander or jump as local electric-field gradients, hot-gas flow, and convection compete. Around aircraft the same can happen under a different mix of forces: fields around the metal body, turbulent airflow, and charged-particle drift along field lines. If plasma briefly detaches from a surface, it can drift sideways, spiral, or move in ways that look surprisingly independent of the background airflow.

So the repo's final research position is simple:

- `EM knots`: real and beautiful mathematics, exact enough to deserve careful visualization.
- `Ball lightning`: probably plasma first, often with matter involved, and only speculatively related to free electromagnetic-knot objects.

## Exactness And Limits

What is exact here:

- The Hopfion field evaluator.
- The Bateman torus-knot field family.
- The energy-density sampling used by the halo.
- The `FIELD LINES` mode, which traces instantaneous electric and magnetic directions from those exact fields.

What is interpretive here:

- The `TOPOLOGY` view for Hopfion mode, which shows the Hopf-fibration picture directly instead of only traced instantaneous `E` and `B` lines.
- Color mapping, bloom, halo density, and filter choices.
- Camera framing and independent display-time scaling.

## Source Links Used For This Repo

Primary Maxwell-knot sources:

- Kedia, Bialynicki-Birula, Peralta-Salas, and Irvine, "Tying Knots in Light Fields" (Phys. Rev. Lett. 111, 150404, 2013): https://doi.org/10.1103/PhysRevLett.111.150404
- Kedia arXiv preprint: https://arxiv.org/abs/1302.0342
- Arrayas and Trueba, "Knots in Electromagnetism" (Physics Reports, 2017): https://doi.org/10.1016/j.physrep.2017.03.001

Experimental and optical topology references:

- Irvine and Bouwmeester, "Linked and knotted beams of light" (Nature Physics, 2008): https://doi.org/10.1038/nphys1056
- Larocque et al., "Reconstructing the topology of optical polarization knots" (Nature Physics, 2018): https://doi.org/10.1038/s41567-018-0229-2
- Wan et al., "Observation of optical hopfions and their transition from skyrmions to non-collinear vortices" / scalar optical Hopfion work (eLight, 2022): https://doi.org/10.1186/s43593-022-00030-2

Ball-lightning references that informed the README conclusions:

- Cen, Yuan, and Xue, "Observation of the Optical and Spectral Characteristics of Ball Lightning" (Phys. Rev. Lett. 112, 035001, 2014): https://doi.org/10.1103/PhysRevLett.112.035001
- Abrahamson and Dinniss, "Ball lightning caused by oxidation of nanoparticle networks from normal lightning strikes on soil" (Nature, 2000): https://doi.org/10.1038/35000525
- Paiva et al., "Production of Ball-Lightning-Like Luminous Balls by Electrical Discharges in Silicon" (Phys. Rev. Lett. 98, 048501, 2007): https://doi.org/10.1103/PhysRevLett.98.048501
- Dikhtyar and Jerby, "Fireball Ejection from a Molten Hot Spot to Air by Localized Microwaves" (Phys. Rev. Lett. 96, 045002, 2006): https://doi.org/10.1103/PhysRevLett.96.045002

## Notes

- `--preset` is a convenience layer on top of the exact fields: `trefoil` = `(2,3)`, `cinquefoil` = `(2,5)`, and `linked-rings` = `(2,2)`.
- Coprime `(P, Q)` values give torus knots; non-coprime pairs give linked rings.
- `medium` is the default preset and is tuned to be much lighter than the original first pass.
