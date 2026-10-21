# Two-Stage Rocket (OpenRocket Simulation)

---

## Table of Contents

- [Overview](#overview)
- [Design](#design)
- [Component Inventory](#component-inventory)
- [Mass Budget](#mass-budget)
- [Motors and Staging](#motors-and-staging)
- [Simulation Results](#simulation-results)
- [Design Review Notes](#design-review-notes)
- [Known Issues](#known-issues)
- [How to Run](#how-to-run)
- [Screenshots](#screenshots)

---

## Overview

| Item | Details |
|---|---|
| Software | OpenRocket |
| Stages | 2 (booster + upper stage) |
| Flight configuration | `[H133-P; H70-0]` |
| Simulation | Simulation 11 |
| Payload | 1500 g mass component (16 cm x 4 cm) |
| Goal | Reliable staging: booster (H70-0) burns at launch, upper stage (H133-P) ignites after booster burnout |

## Design

| Parameter | Value |
|---|---|
| Total length | 160 cm (nose 20 + upper body 82 + booster 58) |
| Outer diameter | 7.5 cm (all body tubes and nose base) |
| Body material | Carbon-fibre reinforced, 1.5 g/cm³, smooth paint (20 µm) |
| Nose cone | Ogive (tangent, shape parameter 1), 20 cm long, 0.2 cm wall |
| Fins (each stage) | 4x trapezoidal, fibreglass, airfoil section, 0.2 cm thick |
| Fin geometry | Root chord 7.5 cm, tip chord 2.5 cm, height 3 cm, sweep length 6.1 cm, sweep angle 63.8° |
| Fin cant | 0° |
| Stability margin | _TBD (read from OpenRocket for both the full stack and the post-separation upper stage)_ |

<!-- Add design screenshot: docs/design.png -->
![Rocket design](docs/design.png)

## Component Inventory

Dimensions are taken from the OpenRocket component dialogs. Position is relative to the parent component, as entered in OpenRocket.

| Component | Key dimensions | Material | Mass | Placement |
|---|---|---|---|---|
| Nose Cone | 20 cm long, 7.5 cm base dia., 0.2 cm wall | Carbon fibre (1.5 g/cm³) | 92.3 g | Top of rocket |
| Body Tube (upper stage) | 82 cm long, OD 7.5 / ID 7.02 cm | Carbon fibre (1.5 g/cm³) | 673 g | Below nose cone |
| Payload Tube (inner tube) | 30 cm long, OD 7.2 / ID 6.8 cm | Carbon fibre (1.5 g/cm³) | _not captured_ | Bottom of parent, -51.2 cm |
| Mass Component "Payload" | 1500 g, 16 cm long, 4 cm dia. | n/a (density 7.46 g/cm³) | 1500 g | Top of parent, 0 cm |
| Booster (body tube) | 58 cm long, OD 7.5 / ID 7.02 cm | Carbon fibre (1.5 g/cm³) | 476 g | Below upper stage |
| Tube Coupler | 6 cm long, OD 7.02 / ID 6.62 cm | Carbon fibre (1.5 g/cm³) | 38.6 g | Bottom of parent, -51.9 cm |
| Trapezoidal Fin Set (x2, one per stage) | See [Design](#design) | Fibreglass (1.85 g/cm³) | 18.9 g each | Bottom of parent, 0 and +0.2 cm |
| Centering Ring (x3) | 0.2 cm thick, OD 7.02 cm, ID auto (0) | Ti-6Al-4V (4.43 g/cm³) | 34.3 g each | Bottom of parent: -82 cm (x2), 0 cm (x1) |
| Bulkhead-1 | 0.3 cm thick, 7.02 cm dia. | Polycarbonate (1.2 g/cm³) | 13.9 g | Bottom of parent, -10.2 cm |
| Bulkhead-2 | 0.3 cm thick, 7.02 cm dia. | Carbon fibre (1.78 g/cm³) | 20.7 g | Bottom of parent, -29.8 cm |
| Bulkhead-3 | 0.3 cm thick, 7.02 cm dia. | Polycarbonate (1.2 g/cm³) | 13.9 g | Bottom of parent, -33.2 cm |
| Bulkhead-4 | 0.3 cm thick, 7.02 cm dia. | Carbon fibre (1.78 g/cm³) | 20.7 g | Bottom of parent, -29.8 cm |

## Mass Budget

| Group | Mass |
|---|---|
| Nose cone | 92.3 g |
| Upper body tube | 673 g |
| Booster tube | 476 g |
| Payload (mass component) | 1500 g |
| Fins (2 sets) | 37.8 g |
| Centering rings (3) | 102.9 g |
| Bulkheads (4) | 69.2 g |
| Tube coupler | 38.6 g |
| **Subtotal (listed components)** | **~2990 g** |
| Payload tube, motors, other | _TBD_ |

The payload is about half of the listed mass, so it is the main driver of the rocket's low performance on H-class motors.

## Motors and Staging

| Stage | Motor | Intended ignition | Separation |
|---|---|---|---|
| Booster (bottom) | H70-0 | Launch | At motor burnout |
| Upper stage (top) | H133-P | First burnout of previous stage (0 to 0.5 s delay) | n/a |

Notes:
- The H133-P is a plugged motor (no ejection charge).
- The ignition override must name the exact configuration being simulated (`[H133-P; H70-0]`), otherwise the setting has no effect on the run.

<!-- Add motor config screenshot: docs/motors.png -->
![Motor configuration](docs/motors.png)

## Simulation Results

Preliminary results from an early run (staging not yet working correctly; update after re-running):

| Metric | Value |
|---|---|
| Apogee | ~32 m |
| Time to apogee | ~4.9 s |
| Total flight time | ~9.6 s |
| Peak acceleration | ~26 m/s² |
| Tumbling observed | Yes, at ~4.6 s |

<!-- Add plot screenshot: docs/flight-plot.png -->
![Flight plot](docs/flight-plot.png)

## How to Run

1. Install [OpenRocket](https://openrocket.info/downloads.html) (Java required).
2. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   ```
3. Open the `.ork` file in OpenRocket (File > Open).
4. Go to **Flight simulations**, select **Simulation 11**, and click **Run**.
5. Check the **Warnings** and **Plot data** tabs.

## Screenshots

| Design | Motor configuration |
|---|---|
| ![Design](docs/design.png) | ![Motors](docs/motors.png) |

| Flight plot | Warnings |
|---|---|
| ![Plot](docs/flight-plot.png) | ![Warnings](docs/warnings.png) |

<details>
<summary>Component dialogs</summary>

![Nose cone](docs/components/nose-cone.png)
![Upper body tube](docs/components/body-tube.png)
![Payload tube](docs/components/payload-tube.png)
![Payload mass](docs/components/payload-mass.png)
![Booster](docs/components/booster.png)
![Tube coupler](docs/components/tube-coupler.png)
![Fin set](docs/components/fin-set.png)

