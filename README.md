## Problem Statement (1.40)

Chips of width $L = 15 \text{ mm}$ on a side are mounted to a substrate that is installed in an enclosure whose walls and air are maintained at a temperature of $T_{sur} = T_{\infty} = 25^\circ\text{C}$. The chips have an emissivity of $\epsilon = 0.60$ and a maximum allowable temperature of $T_s = 85^\circ\text{C}$.

![image](https://github.com/user-attachments/assets/a85c6e9e-d908-4831-a4c5-ab6a4b0f23f3)

**(a)** If heat is rejected from the chips by radiation and natural convection, what is the maximum operating power of each chip? The convection coefficient depends on the chip-to-air temperature difference and may be approximated as $h = C(T_s - T_{\infty})^{1/4}$, where $C = 4.2 \text{ W/m}^2 \cdot \text{K}^{5/4}$.

**(b)** If a fan is used to maintain air flow through the enclosure and heat transfer is by forced convection, with $h = 250 \text{ W/m}^2 \cdot \text{K}$, what is the maximum operating power?

**Parameters Used:**

* **$A$ (Top Surface Area):** $0.0009 \text{ m}^2 = 4 \cdot  (0.015 m)^2$
* **$T_s$ (Chip Surface Temp.):** $358 \text{ K}$ (Given, from $85^\circ\text{C}$)
* **$T_{\infty}, T_{sur}$ (Surrounding Temp.):** $298 \text{ K}$ (Given, from $25^\circ\text{C}$)
* **$\Delta T$ (Temp. Difference):** $60 \text{ K}$ (Calculated: $T_s - T_{\infty}$)
* **$\epsilon$ (Emissivity):** $0.60$ (Given)
* **$\sigma$ (Stefan-Boltzmann Const.):** $5.67 \times 10^{-8} \text{ W/m}^2\text{K}^4$ (Given)
* **$C$ (Nat. Conv. Formula Const.):** $4.2 \text{ W/m}^2\text{K}^{5/4}$ (Given)
* **$h_{nat}$ (Nat. Conv. Coeff.):** 
    $h_{nat} = C(T_s - T_{\infty})^{1/4} = (4.2 \text{ W/m}^2\text{K}^{5/4}) \cdot (60 \text{ K})^{1/4} \approx 4.2 \cdot 2.78316 \approx 11.6893 \text{ W/m}^2\text{K}$
* **$h_{forced}$ (Forced Conv. Coeff.):** $250 \text{ W/m}^2\text{K}$ (Given)

---
### Analytical Solution
**Part (a): Maximum Power with Natural Convection and Radiation**

1.  **Natural Convection Heat Transfer ($q_{conv,nat}$):**
    $q_{conv,nat} = h_{nat} \cdot A \cdot \Delta T$
    $q_{conv,nat} = (11.6893 \text{ W/m}^2\text{K}) \cdot (0.0009 \text{ m}^2) \cdot (60 \text{ K}) \approx 0.6312 \text{ W}$

2.  **Radiation Heat Transfer ($q_{rad}$):**
    $q_{rad} = \epsilon \cdot A \cdot \sigma \cdot (T_s^4 - T_{sur}^4)$
    $q_{rad} = (0.60) \cdot (0.0009 \text{ m}^2) \cdot (5.67 \times 10^{-8} \text{ W/m}^2\text{K}^4) \cdot ((358 \text{ K})^4 - (298 \text{ K})^4) \approx 0.2615 \text{ W}$

3.  **Total Maximum Power for Part (a) ($P_a$):**
    $P_a = q_{conv,nat} + q_{rad}$
    $P_a = 0.6312 \text{ W} + 0.2615 \text{ W} \approx \mathbf{0.8927 \text{ W}}$

---

**Part (b): Maximum Power with Forced Convection and Radiation**

4.  **Forced Convection Heat Transfer ($q_{conv,forced}$):**
    $q_{conv,forced} = h_{forced} \cdot A \cdot \Delta T$
    $q_{conv,forced} = (250 \text{ W/m}^2\text{K}) \cdot (0.0009 \text{ m}^2) \cdot (60 \text{ K}) = 13.5 \text{ W}$

5.  **Radiation Heat Transfer ($q_{rad}$):**
    (Value from Part (a), Step 2, as it depends on the same parameters)
    $q_{rad} \approx 0.2615 \text{ W}$

6.  **Total Maximum Power for Part (b) ($P_b$):**
    $P_b = q_{conv,forced} + q_{rad}$
    $P_b = 13.5 \text{ W} + 0.2615 \text{ W} \approx \mathbf{13.7615 \text{ W}}$

---

Answers:
* **(a) Maximum Power (Natural Convection + Radiation): $\approx 0.8927 \text{ W}$**
* **(b) Maximum Power (Forced Convection + Radiation): $\approx 13.7615 \text{ W}$**
### Ansys Fluent Solution


**General Physical Assumptions (Common to Both Cases):**

* **Steady-State:** The thermal conditions and flow field do not change over time.
* **3D Geometry:** A simplified 3D representation of the chips and enclosure was used.
* **Diffuse Gray Surfaces:** Chip surfaces were treated as diffuse gray emitters for radiation ($\epsilon = 0.6$).
* **Constant Chip Temperature:** The chip surface was maintained at a uniform $T_s = 85^\circ\text{C}$.
* **Constant Enclosure Temperature:** Enclosure walls and ambient air were at a uniform $T_{sur} = T_{\infty} = 25^\circ\text{C}$.
* **Material Properties:** Standard properties for air and aluminum (default) were used.

  

**Case A: Natural Convection & Radiation - Specific Physical Assumptions:**

* **Buoyancy-Driven Flow:** Air movement is primarily caused by density differences due to temperature gradients.
* **Non-zero Gravity:** Gravitational acceleration was included in the model.
* **Temperature-Dependent Air Density:** Air density varied with temperature (e.g., incompressible ideal gas law) to model natural convection currents.
* **Laminar Flow:** The airflow regime was assumed to be laminar, justified by an expected low Grashof number.
* **Open Boundaries:** Pressure inlet/outlet conditions simulated an open environment allowing natural air circulation.

### Justification for Laminar Flow Assumption (Rayleigh Number) - Concise

To justify assuming laminar flow for natural convection (Part a), we evaluate the Rayleigh number ($Ra_L$). For a heated horizontal plate facing upwards, laminar flow is typically observed when $10^4 < Ra_L < 10^7$.

**1. Essential Parameters & Calculations:**
* Surface Temperature, $T_s = 358\text{K}$; Ambient Temperature, $T_{\infty} = 298\text{K}$; Temperature Difference, $\Delta T = 60\text{K}$.
* Film Temperature, $T_f = (T_s + T_{\infty})/2 = 328 \text{ K}$.
* Air properties at $T_f \approx 328 \text{ K}$:
    * Coefficient of thermal expansion, $\beta \approx 0.003049 \text{ K}^{-1}$
    * Kinematic viscosity, $\nu \approx 1.88 \times 10^{-5} \text{ m}^2/\text{s}$
    * Prandtl number, $Pr \approx 0.707$

* **Grashof Number ($Gr_L$):**
    $Gr_L = \frac{g \beta \Delta T L^3}{\nu^2} = \frac{(9.81) \cdot (0.003049) \cdot (60) \cdot (0.015)^3}{(1.88 \times 10^{-5})^2} \approx 1.713 \times 10^4$

* **Rayleigh Number ($Ra_L$):**
    $Ra_L = Gr_L \cdot Pr = (1.713 \times 10^4) \cdot (0.707) \approx 1.211 \times 10^4$

**2. Conclusion:**
The calculated Rayleigh number is $Ra_L \approx 1.21 \times 10^4$. Since this value falls within the established range for laminar flow ($10^4 < 1.21 \times 10^4 < 10^7$), the assumption of laminar flow for the natural convection scenario is justified.





**Case B: Forced Convection & Radiation - Specific Physical Assumptions:**

* **Fan-Driven Flow:** Air movement is primarily caused by an external fan.
* **Negligible Buoyancy :** Effects of gravity and natural buoyancy may be considered secondary to the forced flow.
* **Constant Air Density :** Air density could be assumed constant if temperature variations' impact on density is minor compared to fan effects.
* **Turbulent Flow:** The airflow regime was assumed to be turbulent due to higher velocities induced by the fan (e.g., k-epsilon model).
* **Defined Inlet Velocity:** A specific velocity profile was defined at an inlet boundary to represent the fan's airflow.



*(The images below likely represent visualizations from the Ansys Fluent simulation, such as temperature contours or heat flux vectors, illustrating the thermal performance under the simulated conditions.)*

  

![image](https://github.com/user-attachments/assets/58e113a0-f84e-4d79-90f5-95ca80047f2e)

  

![image](https://github.com/user-attachments/assets/4f21d403-98b3-416a-a1d7-1889d36d51ea)