# MAES-Marine Stack: Detailed Mathematical & Mechanical Derivations

This document details the governing equations and physical assumptions used in the **MAES-Marine Stack** CAD sizing, tolerance analysis, and dynamic stress verification.

---

## 1. Fluid Dynamics & Pressure Drop Scaling

Flow inside the bipolar plate channels is treated as laminar fluid flow through rectangular ducts ($Re < 2300$). 

### 1.1 Hydraulic Diameter ($D_h$)
For a rectangular channel with depth $d_c$ and width $w_c$:

$$D_h = \frac{2 \cdot w_c \cdot d_c}{w_c + d_c}$$

### 1.2 Pressure Drop Derivation
Using the Darcy-Weisbach equation for laminar duct flow where friction factor $f = \frac{C}{Re}$:

$$\Delta P = f \cdot \left(\frac{L}{D_h}\right) \cdot \left(\frac{\rho v^2}{2}\right)$$

Assuming constant mass flow rate $\dot{m}$, velocity $v$ scales inversely with cross-sectional area $A = w_c \cdot d_c$. Substituting $A$ into the pressure drop formulation yields the primary sensitivity scaling relationship:

$$\Delta P \propto \frac{1}{w_c \cdot d_c^3}$$

### 1.3 Statistical Pressure Sensitivity
The statistical variation in pressure drop ($\Delta P$) driven by manufacturing depth variation ($t_{\text{dc}}$) and width variation ($t_{\text{wc}}$) is calculated as:

$$\Delta P = \Delta P_{\text{nom}} \times \left(\frac{d_{\text{nom}}}{t_{\text{dc}}}\right)^3 \times \left(\frac{w_{\text{nom}}}{t_{\text{wc}}}\right)$$

---

## 2. Mass Transport & Faradaic Efficiency Coupling

Flow distribution uniformity ($\Phi$) governs reactant supply to the Gas Diffusion Layer (GDL).

### 2.1 Flow Uniformity Index ($\Phi$)
Flow distribution is influenced by channel geometry variation and GDL compression state:

$$\Phi = \left(\frac{t_{\text{dc}}}{d_{\text{nom}}}\right)^2 \times \left(\frac{t_{\text{gdl}}}{t_{\text{gdl,nom}}}\right)$$

Where $t_{\text{gdl}}$ is the compressed GDL thickness derived from tie-rod clamping stress $\sigma_{\text{clamp}}$ and GDL elastic modulus $E_{\text{gdl}} \approx 12.0\text{ MPa}$:

$$t_{\text{gdl}} = t_{\text{gdl,uncompressed}} \times \left(1 - \frac{\sigma_{\text{clamp}}}{E_{\text{gdl}}}\right)$$

### 2.2 Faradaic Efficiency ($\text{FE}$) Empirical Coupling
Under maldistributed flow ($\Phi < 1.0$), localized mass-transport losses reduce overall efficiency:

$$\text{FE} = \text{FE}_{\text{max}} - \alpha \times \max\left(0, 1.0 - \Phi\right)^\beta$$

Where:
* $\text{FE}_{\text{max}} = 91.8\%$ (Nominal Faradaic Efficiency)
* $\alpha = 12.0$ (Sensitivity coefficient)
* $\beta = 1.5$ (Non-linear penalty exponent)

---

## 3. Dynamic Marine Sealing & Stress Mechanics

When operating on marine vessels, wave action induces dynamic vertical and angular accelerations ($\mathbf{a}_{\text{dynamic}}$), altering the stack clamping force.

### 3.1 Dynamic Pre-load Fluctuation
The static pre-load stress ($\sigma_0 = 2.50\text{ MPa}$) fluctuates as a function of vessel pitch angle ($\theta_{\text{pitch}}$) and dynamic load factor ($g_{\text{dynamic}}$):

$$\sigma_{\text{clamp}}(\theta) = \sigma_0 + \Delta\sigma_{\text{dynamic}} \cdot \sin(\theta_{\text{pitch}}) \cdot g_{\text{dynamic}}$$

Where $\Delta\sigma_{\text{dynamic}} = 0.35\text{ MPa}$ represents the baseline dynamic stress offset.

### 3.2 Elastomeric Gasket Strain Calculation
Gasket strain ($\varepsilon_{\text{gasket}}$) is computed from clamping stress assuming linear hyperelastic recovery within the working strain region ($20\% - 35\%$):

$$\varepsilon_{\text{gasket}} = \varepsilon_0 + \left(\sigma_{\text{clamp}} - \sigma_0\right) \cdot \left(\frac{\Delta \varepsilon}{\Delta \sigma}\right)$$

$$\varepsilon_{\text{gasket}} = 25.0\% + (\sigma_{\text{clamp}} - 2.50) \times 8.0 \quad [\%]$$

---

## 4. Acceptance Boundaries

The stack assembly design is validated against the following mechanical and electrochemical operational bounds:

| Parameter | Minimum Limit | Maximum Limit | Units |
| :--- | :--- | :--- | :--- |
| **Channel Pressure Drop ($\Delta P$)** | $38.0$ | $53.0$ | $\text{kPa}$ |
| **Faradaic Efficiency ($\text{FE}$)** | $90.0$ | $100.0$ | $\%$ |
| **Gasket Compression Strain ($\varepsilon_{\text{gasket}}$)** | $20.0$ | $35.0$ | $\%$ |
| **Tie-Rod Pre-load Stress ($\sigma_{\text{clamp}}$)** | $2.00$ | $3.50$ | $\text{MPa}$ |
