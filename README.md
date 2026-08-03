# MAES-Marine Stack: CAD Design, Tolerance Analysis & Dynamic Sealing Verification

![Status](https://img.shields.io/badge/Status-Research_POC-orange) ![Type](https://img.shields.io/badge/Type-Simulation_Model-blue)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Powered by Gemini](https://img.shields.io/badge/Powered%20by-Google%20Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white)](https://gemini.google.com)
![CO2 Reduction](https://img.shields.io/badge/CO%E2%82%82_Reduction-2E7D32?style=for-the-badge&logo=leaf&logoColor=white)
![Electrochemistry](https://img.shields.io/badge/Electrochemistry-00A86B?style=for-the-badge&logo=flask&logoColor=white)
![CAD Design](https://img.shields.io/badge/CAD_Design-E53E3E?style=for-the-badge&logo=autodesk&logoColor=white)
---
## 📌 Project Overview

The **MAES-Marine Stack** repository provides an open-source engineering framework for designing, sizing, and validating marine-grade hydrogen fuel cell / electrolyzer stack assemblies operating under dynamic sea-state conditions.

This project integrates 3D CAD modeling, statistical tolerance budgeting (**ISO 2768**), and a Monte Carlo simulation engine to verify system performance under dynamic vessel pitch and roll motion ($0^\circ - 25^\circ$).

---

## 🏗️ System Architecture & Engineering Scope

```
+---------------------------------------------------------------------------------+
|                            MAES-MARINE STACK SCOPE                              |
+---------------------------------------------------------------------------------+
|  1. CAD DESIGN & HARDWARE (cad/)                                                |
|     - Bipolar Flow Plates (1.00 mm channel depth nominal)                       |
|     - Elastomeric Sealing Gaskets (EPDM/FKM, Shore A 60-70)                     |
|     - End Plate Assembly & Compression Tie-Rods                                 |
|                                                                                 |
|  2. SYSTEM SIMULATION ENGINE (sim/)                                             |
|     - 10,000-Run Monte Carlo Tolerance Analysis                                 |
|     - Channel Pressure Drop ($\Delta P$) & Faradaic Efficiency Modeling         |
|     - Dynamic Sea-State Pitch/Roll ($0^\circ - 25^\circ$) Gasket Strain Bounds  |
+---------------------------------------------------------------------------------+
```

---

## 📐 Mathematical Methodology

### 1. Channel Pressure Drop ($\Delta P$) Sensitivity
Flow channel pressure drop scales dynamically with channel depth tolerance ($t_{\text{dc}}$) and width tolerance ($t_{\text{wc}}$):

$$\Delta P = \Delta P_{\text{nom}} \times \left(\frac{d_{\text{nom}}}{t_{\text{dc}}}\right)^3 \times \left(\frac{w_{\text{nom}}}{t_{\text{wc}}}\right)$$

### 2. Flow Uniformity & Faradaic Efficiency ($\text{FE}$)
Flow distribution uniformity ($\Phi$) is coupled to Gas Diffusion Layer (GDL) compressed thickness ($t_{\text{gdl}}$):

$$\Phi = \left(\frac{t_{\text{dc}}}{d_{\text{nom}}}\right)^2 \times \left(\frac{t_{\text{gdl}}}{t_{\text{gdl,nom}}}\right)$$

$$\text{FE} = 91.8 - 12.0 \times \max\left(0, 1.0 - \Phi\right)^{1.5}$$

### 3. Dynamic Marine Sealing Integrity
Dynamic clamping stress ($\sigma_{\text{clamp}}$) and gasket strain ($\varepsilon_{\text{gasket}}$) vary with vessel pitch angle ($\theta_{\text{pitch}}$) under dynamic sea-state loads ($1.0\text{g} - 2.5\text{g}$):

$$\sigma_{\text{clamp}} = 2.50 + 0.35 \cdot \sin(\theta_{\text{pitch}}) \cdot 2.5 \quad [\text{MPa}]$$

$$\varepsilon_{\text{gasket}} = 25.0 + (\sigma_{\text{clamp}} - 2.50) \cdot 8.0 \quad [\%]$$

---

## 📊 Phase 1 Simulation Results

A 10,000-run Monte Carlo simulation yielded the following manufacturing pass rates and operational outputs across standard tolerance classes:

| Tolerance Class | Channel Depth Tol. | Mean $\Delta P$ (kPa) | Std Dev $\sigma$ (kPa) | Faradaic Eff. (%) | Manufacturing Yield (%) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ISO 2768-f (Fine)** | $\pm 0.005\text{ mm}$ | $45.01$ | $0.37$ | $91.78\%$ | **100.0%** |
| **ISO 2768-m (Medium)** | $\pm 0.020\text{ mm}$ | $45.00$ | $0.95$ | $91.71\%$ | **100.0%** |
| **ISO 2768-c (Coarse)** | $\pm 0.050\text{ mm}$ | $45.11$ | $2.26$ | $89.93\%$ | **99.86%** |

### Key Conclusions
1. **Manufacturing Tolerance:** **ISO 2768-m ($\pm 0.020\text{ mm}$)** is selected as the production standard. It achieves a **100% manufacturing pass rate**, rendering high-cost fine precision machining (ISO 2768-f) unnecessary.
2. **Sealing Integrity:** Gasket strain stays smoothly within the target **$20\% - 35\%$ safe sealing zone** across all marine pitch angles ($0^\circ - 25^\circ$).

---

## 🚀 Quickstart & Execution

```bash
# Clone repository
git clone [https://github.com//Abhishek1033ubuntu/MAES-Marine-Stack-CAD-Sim.git](https://github.com//Abhishek1033ubuntu/MAES-Marine-Stack-CAD-Sim.git)
cd MAES-Marine-Stack-CAD-Sim/sim

# Install dependencies
pip install -r requirements.txt

# Run simulation script
python maes_simulation.py
```

---

## ⚠️ Verification Disclaimer & Next Steps

This Python engine performs **system-level statistical and analytical verification**. For final physical hardware manufacturing sign-off:
* Non-linear spatial continuum FEA (e.g., via FreeCAD/CalculiX, ANSYS, or Abaqus) is recommended to evaluate localized stress concentrations at plate corners.
* Gasket materials should meet **EPDM / FKM (60–70 Shore A)** specifications.

---

## 📜 License
PROPRIETARY SOURCE-AVAILABLE LICENSE & END USER AGREEMENT

Copyright (c) 2026 Abhishek Singh | UIDAI: 9414 9122 9013
Location: Madhya Pradesh, India
Contact: abhishek1033@gmail.com | abhishek.s@live.in
