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




TALK ABOUT SPACECLAIM



**General Setup (Both Cases)**

* **Solver:** Steady-state.
* **Mesh:** Inflation was used to improve the mesh near the boundary between the chips and the air, and the mesh at the boundaries 
* **Mesh sizing for chips**
    - Element Size: **1 mm**
- **Mesh sizing for the enclosure:**
    - Maximum Element Size: **6 mm**
    - Growth Rate: **1.05** (smoother transition)
	- **Inflation Layers on fluid domain walls:**
	    - Number of Layers (Maximum): **5 layers**
	    - Transition Type: **Smooth Transition** 


---

**Case A: Natural Convection & Radiation**

* **Core Idea:** Buoyancy-driven airflow and surface radiation.
* **Models:**
    * **Viscous:** Laminar (Based on Rayleigh number calculations in the appendix).
    * **Energy Equation ON**
    * **Radiation:** Surface-to-Surface (S2S) model.
    * **Gravity:** Enabled (-9.81 m/s² in Y).
* **Materials & Cell Zones:**
    * **Air:** Density set to "incompressible ideal gas" (for buoyancy).
    * **Chips (Aluminum):** Fixed temperature of 358.15 K (85°C).
* **Boundary Conditions :**
    * **Inlet/Outlet (Bottom/Top):** Pressure Inlet/Outlet (0 Pa gauge), 298.15 K (25°C), radiation emissivity 1 (simulating open environment).
    * **Enclosure Walls:** Adiabatic, radiation emissivity 1.
    * **Chip Sides/Back:** Adiabatic, excluded from radiation.
    * **Chip Top Surface (Fluid Walls):** Coupled thermal condition, radiation emissivity 0.6.
* **Solver Settings:**
    * **Coupling:** Uncoupled.
    * **Discretization:** 
	    * Presto (Pressure), Presto provides more accurate results for buoyancy-driven flows like natural convection
	    * Second Order Upwind (Momentum, Energy).


---

**Case B: Forced Convection & Radiation (Changes from Case A)**

* **Core Idea:** Fan-driven airflow  and surface radiation.
* **Models :**
    * **Viscous:** Realizable k-epsilon (turbulent) with Enhanced Wall Treatment (better for forced convection).
    * **Gravity:** Disabled as it is negligible.
* **Materials & Cell Zones:**
    * **Air:** Density set to "constant." 
* **Boundary Conditions :**
    * **Inlet (Bottom):** Changed to Velocity Inlet (to simulate fan).
* **Solver Settings:**
    * **Discretization:** All second order upwind





*(The images below likely represent visualizations from the Ansys Fluent simulation, such as temperature contours or heat flux vectors, illustrating the thermal performance under the simulated conditions.)*

  

![image](https://github.com/user-attachments/assets/58e113a0-f84e-4d79-90f5-95ca80047f2e)

  

![image](https://github.com/user-attachments/assets/4f21d403-98b3-416a-a1d7-1889d36d51ea)

### Laminar floor proof for case a)
**Parameters**
* Surface Temperature, $T_s = 358\text{K}$; Ambient Temperature, $T_{\infty} = 298\text{K}$; Temperature Difference, $\Delta T = 60\text{K}$.
* Film Temperature, $T_f = (T_s + T_{\infty})/2 = 328 \text{ K}$.
* Air properties at $T_f \approx 328 \text{ K}$:
    * Coefficient of thermal expansion, $\beta \approx 0.003049 \text{ K}^{-1}$
    * Kinematic viscosity, $\nu \approx 1.88 \times 10^{-5} \text{ m}^2/\text{s}$
    * Prandtl number, $Pr \approx 0.707$
* Characteristic Length (chip side), $L = 0.015 \text{ m}$.
* Gravitational acceleration, $g = 9.81 \text{ m/s}^2$.
* **Grashof Number ($Gr_L$):**
    $Gr_L = \frac{g \beta \Delta T L^3}{\nu^2} = \frac{(9.81) \cdot (0.003049) \cdot (60) \cdot (0.015)^3}{(1.88 \times 10^{-5})^2} \approx 1.713 \times 10^4$
* **Rayleigh Number ($Ra_L$):**
    $Ra_L = Gr_L \cdot Pr = (1.713 \times 10^4) \cdot (0.707) \approx 1.211 \times 10^4$

The calculated Rayleigh number is $Ra_L \approx 1.21 \times 10^4$. This value falls within the established range for laminar flow ($10^4 < 1.21 \times 10^4 < 10^7$).


### Calculation for Input Velocity in Forced Convection for case b)
1.  **Empirical Correlation for Nusselt Number:**
    For laminar flow over a flat plate (our case), the average Nusselt number is:
    $$Nu_L = 0.664 \cdot Re_L^{1/2} \cdot Pr^{1/3}$$
    where:
    * $Re_L$ is the Reynolds number based on the plate length $L$.
    * $Pr$ is the Prandtl number of the fluid (air).

2.  **Definition of Nusselt Number from Heat Transfer Coefficient ($h$):**
    The Nusselt number can also be defined as:
    $$Nu_L = \frac{h \cdot L}{k}$$
    where:
    * $h$ is the convective heat transfer coefficient.
    * $L$ is the characteristic length (in this case, the side of the chip).
    * $k$ is the thermal conductivity of the air.

3.  **Equating and Substituting Reynolds Number:**
    By equating the two expressions for $Nu_L$ and substituting the Reynolds number $Re_L = \frac{\rho \cdot v \cdot L}{\mu} = \frac{v \cdot L}{\nu}$ (where $\nu = \mu / \rho$ is the kinematic viscosity):
    
    $$\frac{h \cdot L}{k} = 0.664 \cdot \left(\frac{v \cdot L}{\nu}\right)^{1/2} \cdot Pr^{1/3}$$

4.  **Solving for Velocity ($v$):**
    Rearranging the equation to solve for $v$ yields the governing equation for our calculation:
    $$v = \frac{\nu}{L} \cdot \left(\frac{h \cdot L}{k \cdot 0.664 \cdot Pr^{1/3}}\right)^2 ,$$
$$v = \frac{1.8746 \times 10^{-5} \text{ m}^2/\text{s}}{0.015 \text{ m}} \cdot \left(\frac{250 \text{ W/m}^2\text{K} \cdot 0.015 \text{ m}}{0.0283 \text{ W/(m}\cdot\text{K)} \cdot 0.664 \cdot (0.706)^{1/3}}\right)^2 \approx 62.90 \text{ m/s}$$

