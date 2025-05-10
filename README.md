## Problem Statement (1.40)

Chips of width $L = 15 \text{ mm}$ on a side are mounted to a substrate that is installed in an enclosure whose walls and air are maintained at a temperature of $T_{sur} = T_{\infty} = 25^\circ\text{C}$. The chips have an emissivity of $\epsilon = 0.60$ and a maximum allowable temperature of $T_s = 85^\circ\text{C}$.

![image](https://github.com/user-attachments/assets/0bcac1bc-c5a3-4496-bba6-341f23ef1d41)


**(a)** If heat is rejected from the chips by radiation and natural convection, what is the maximum operating power of each chip? The convection coefficient depends on the chip-to-air temperature difference and may be approximated as $h = C(T_s - T_{\infty})^{1/4}$, where $C = 4.2 \text{ W/m}^2 \cdot \text{K}^{5/4}$.

**(b)** If a fan is used to maintain air flow through the enclosure and heat transfer is by forced convection, with $h = 250 \text{ W/m}^2 \cdot \text{K}$, what is the maximum operating power?

**Parameters Used:**

* **$A$ (Top Surface Area):** $0.0009 \text{ m}^2$ (Calculated: 4 $\cdot$ 0.015<sup>2</sup>)
* **$T_s$ (Chip Surface Temp.):** $358 \text{ K}$ (Given, from $85^\circ\text{C}$)
* **$T_{\infty}, T_{sur}$ (Surrounding Temp.):** $298 \text{ K}$ (Given, from $25^\circ\text{C}$)
* **$\Delta T$ (Temp. Difference):** $60 \text{ K}$ (Calculated: $T_s - T_{\infty}$)
* **$\epsilon$ (Emissivity):** $0.60$ (Given)
* **$\sigma$ (Stefan-Boltzmann Const.):** $5.67 \times 10^{-8} \text{ W/m}^2\text{K}^4$ (Given)
* **$C$ (Nat. Conv. Formula Const.):** $4.2 \text{ W/m}^2\text{K}^{5/4}$ (Given)
* **$h_{nat}$ (Nat. Conv. Coeff.):** 
    * **Formula:** $h_{nat} = C(T_s - T_{\infty})^{1/4}$
    * **Calculation:** $h_{nat} = (4.2 \text{ W/m}^2\text{K}^{5/4}) \cdot (60 \text{ K})^{1/4} \approx 4.2 \cdot 2.78316 \approx 11.6893 \text{ W/m}^2\text{K}$
* **$h_{forced}$ (Forced Conv. Coeff.):** $250 \text{ W/m}^2\text{K}$ (Given)

---

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

![image](https://github.com/user-attachments/assets/3488b04a-a2ad-4b54-b5e6-6696f23d9ec1)

![image](https://github.com/user-attachments/assets/20584e14-3ba6-4004-a051-d9db77e4c5cc)

