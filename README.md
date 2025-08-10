# Static Mixer CFD — Mesh Independence & Scheme Comparison

This repository contains my CFD study of a static mixer performed in **ANSYS CFX**, evaluating the effect of **mesh resolution** and **numerical schemes** on thermal mixing accuracy and computational cost.

## Overview
Static mixers are used in chemical processing, water treatment, and HVAC systems to enhance mixing without moving parts.  
In this project, I tested mesh sizes from **25k** to **2M+** elements, applied **y⁺-controlled inflation layers**, compared **Upwind** vs **High-Resolution** discretization schemes, and quantified performance using a **Mixing Index (MI)** at the outlet.

## Methodology

### 1. Geometry Design
The static mixer geometry was designed to represent an industrial mixing unit with features that enhance passive mixing while maintaining computational feasibility for a mesh independence study.

Key features:
- **Two inlet channels**: Deliver separate fluid streams at different temperatures.
- **Mixing chamber with a toroidal bend**: Induces secondary flows and swirl for enhanced mixing without moving parts.
- **Single outlet channel**: Sized to maintain target velocities and avoid excessive pressure drop.

This geometry is representative of mixers used in chemical processing, water treatment, and HVAC systems.

---

### 2. Boundary Conditions
The case simulates a controlled industrial scenario:

| Boundary      | Velocity (m/s) | Temperature (K) | Notes                                |
|---------------|----------------|-----------------|---------------------------------------|
| **Inlet 1**   | 2.0            | 285             | Uniform velocity and temperature     |
| **Inlet 2**   | 2.0            | 315             | Uniform velocity and temperature     |
| **Outlet**    | Pressure outlet (0 Pa gauge) | N/A | Fully developed outflow |
| **Walls**     | No-slip        | Adiabatic       | No heat transfer through walls       |

---

### 3. Turbulence Model
The **SST \( k-\omega \)** model was selected for its ability to:
- Accurately capture near-wall effects.
- Handle separated flows and streamline curvature.
- Blend \( k-\omega \) near walls with \( k-\epsilon \) in the free stream.

---

### 4. Discretization Schemes
Two schemes were tested for convection terms:

#### 4.1 Upwind
- First-order accurate, using upstream values for interpolation.
- Stable and robust but introduces **numerical diffusion**.
- Leads to smoother gradients and reduced peak values.

#### 4.2 High-Resolution
- Blends first-order and second-order schemes.
- Preserves sharper gradients and small-scale features.
- Reduces numerical diffusion while avoiding spurious oscillations.

---

### 5. Mesh Design & Inflation Layers
Meshes of increasing resolution were generated to evaluate mesh independence:

| Mesh Level     | Elements      |
|----------------|---------------|
| Coarse         | ~25,000       |
| Medium         | ~62,000       |
| Intermediate   | ~261,000      |
| Fine           | ~542,000      |
| Ultra-Fine     | ~2,028,000    |

#### Inflation Layers:
- **y⁺ target**: 30–100 (SST \( k-\omega \) scalable wall functions).
- **First layer height**: Calculated from y⁺ target.
- **Number of layers**: 5–8.
- **Growth rate**: ≤ 1.2 to avoid excessive stretching.

These layers ensure accurate wall shear stress and thermal gradient capture.

---

### 6. Performance Metric — Mixing Index (MI)
The **Mixing Index (MI)** was calculated at the outlet plane:

\[
MI = 1 - \frac{\sigma}{\sigma_{\text{max}}}
\]
where:
- \(\sigma\) = Standard deviation of temperature at the outlet.
- \(\sigma_{\text{max}}\) = Standard deviation for the completely unmixed case.

An MI near **1.0** indicates high mixing efficiency.

---

### 7. Case Files
All geometry, mesh setups, and ANSYS CFX case files (.ccl/.def/.res) are available here:  
📂 **[Google Drive — Static Mixer CFD Data](https://drive.google.com/drive/folders/1RmY7mpxsLA048t4DLcVpCGNWAs5pRog1)**

---

## Repository Structure

.
├── README.md               # Project description (this file)
├── LICENSE                 # License information
├── .gitignore              # Ignore rules for CFD & ANSYS outputs
├── data/                   # (empty) Place large solver data, results, CSV files here
├── figures/                # (empty) Place images/plots here
├── cfx_case/               # (empty) Place ANSYS CFX .ccl/.def/.res files here
└── results/                # (empty) Post-processed results here
```

> **Note:** Large solver files are not stored in this repository. Add them locally in the appropriate folders or link to an external storage location.

## How to Cite
If you use or reference this work, please cite:
```
Sharifi, Mj. "Static Mixer CFD — Mesh Independence & Scheme Comparison." GitHub repository, 2025-08-10.
Available at: https://github.com/Mjsharifi92/A-static-mixer-ANSYS-CFX
```

## License
This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
