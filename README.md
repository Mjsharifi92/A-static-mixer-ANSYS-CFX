# Static Mixer CFD — Mesh Independence & Scheme Comparison

This repository contains my CFD study of a static mixer performed in **ANSYS CFX**, evaluating the effect of **mesh resolution** and **numerical schemes** on thermal mixing accuracy and computational cost.

## Overview
Static mixers are used in chemical processing, water treatment, and HVAC systems to enhance mixing without moving parts.  
In this project, I tested mesh sizes from **25k** to **2M+** elements, applied **y⁺-controlled inflation layers**, compared **Upwind** vs **High-Resolution** discretization schemes, and quantified performance using a **Mixing Index (MI)** at the outlet.

## Key Findings
- **Fine mesh (~542k elements) + High-Resolution** produced results almost identical to ultra-fine meshes while cutting CPU time by ~65%.
- Proper near-wall resolution (**y⁺ ≈ 30–100**) was essential for accurate turbulence capture.
- High-Resolution preserved sharper gradients; Upwind smoothed them out.

## Repository Structure
```
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
