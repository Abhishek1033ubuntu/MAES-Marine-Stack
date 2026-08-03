# MAES-Marine Stack: Phase 1 Engineering Verification Report

**Project Title:** MAES-Marine Stack CAD Tolerance & Dynamic Stress Verification  
**Author:** MAES Hardware & Simulation Team  
**Verification Date:** August 2026  
**Status:** **PASSED** (Approved for Phase 2 Prototyping)

---

## Executive Summary

Phase 1 validation evaluates the mechanical and operational robustness of the **MAES-Marine Stack** under manufacturing variability and dynamic marine vessel motion. Using a 10,000-iteration Monte Carlo engine, the design was tested across **ISO 2768** tolerance classes to identify optimal manufacturing limits.

### Primary Conclusions
1. **Manufacturing Tolerance Selection:** **ISO 2768-m (Medium, $\pm 0.020\text{ mm}$)** is selected as the production standard. It achieves a **100% manufacturing pass rate** for pressure drop and efficiency, eliminating the need for expensive fine machining (ISO 2768-f).
2. **Dynamic Marine Integrity:** Sealing gasket strain remains bounded within **$25.0\% - 27.96\%$** across vessel pitch angles of $0^\circ - 25^\circ$, well within the safe sealing range ($20\% - 35\%$).

---

## 1. Tolerance Sensitivity & Yield Analysis

The nominal channel dimensions ($1.00\text{ mm}$ depth, $1.00\text{ mm}$ width) were perturbed using Gaussian normal distributions matching standard tolerance classes ($3\sigma$ bounds).

### Statistical Output Summary (10,000 Runs)

| Tolerance Class | Channel Depth Tol. | Mean $\Delta P$ (kPa) | Std Dev $\sigma$ (kPa) | Mean Faradaic Eff. (%) | Manufacturing Yield (%) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ISO 2768-f (Fine)** | $\pm 0.005\text{ mm}$ | $45.01$ | $0.37$ | $91.78\%$ | **100.0%** |
| **ISO 2768-m (Medium)** | $\pm 0.020\text{ mm}$ | $45.00$ | $0.95$ | $91.71\%$ | **100.0%** |
| **ISO 2768-c (Coarse)** | $\pm 0.050\text{ mm}$ | $45.11$ | $2.26$ | $89.93\%$ | **99.86%** |

Key Observation: ISO 2768-c introduces a 0.14% scrap rate due to Faradaic efficiency drops below 90.0%. ISO 2768-m achieves 100% yield while maintaining standard CNC milling costs.
---

## 2. Dynamic Marine Sealing Integrity

Simulated dynamic pitch variations ($0^\circ - 25^\circ$) show controlled clamping stress fluctuations:

* **Resting Baseline ($0^\circ$ Pitch):** Clamping stress $= 2.50\text{ MPa} \implies \varepsilon_{\text{gasket}} = 25.0\%$
* **Maximum Dynamic Pitch ($25^\circ$ Pitch):** Clamping stress $= 2.87\text{ MPa} \implies \varepsilon_{\text{gasket}} = 27.96\%$

The elastomeric gasket operates entirely within the linear elastic region, preventing permanent deformation, blowout, or stress relaxation leakage.

---

## 3. Phase 2 Hardware Roadmap

To transition from analytical verification to physical hardware release:

1. **CAD Freeze:** Lock bipolar plate CAD channel geometry at $1.00\text{ mm}$ nominal with ISO 2768-m drawing callouts.
2. **Material Callouts:**
   * Bipolar Plates: Graphite composite or coated titanium (Grade 2).
   * Sealing Gaskets: Molded **EPDM / FKM (Viton)** with **60–70 Shore A** durometer.
3. **Physical Testing:** Validate contact stress uniformity using **Fujifilm Prescale** pressure-indicating film on a 5-cell test stack.
