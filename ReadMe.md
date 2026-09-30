# HydroNet-Proof: Fluid Dynamics & Hydraulic Network Mathematical Model

An applied mathematics project focused on analytical derivations, fluid mechanics, and numerical analysis models for piping networks. 

## 📌 Project Overview
This project builds a manual mathematical framework to model water flow, mass balance, and energy loss in infrastructure pipelines. It bypasses automated software to focus on step-by-step mathematical proofs and manual calculations needed to analyze structural hydraulic stress.

---

## 📐 Core Governing Physics

The model analyzes steady-state water flow through a pipeline network using two core laws of physics:

### 1. Conservation of Mass (Continuity Theory)
Water cannot disappear. For any pipe with a changing diameter, the flow rate ($Q$) remains constant across all points:
$$A_1 \cdot v_1 = A_2 \cdot v_2 = Q$$

*Where $A$ is the pipe's cross-sectional area ($\frac{\pi D^2}{4}$) and $v$ is the water velocity.*

### 2. Conservation of Momentum (Frictional Energy Loss)
As water moves, friction causes a drop in pressure. This energy loss ($h_f$) is calculated using the **Darcy-Weisbach Equation**:
$$h_f = f \cdot \frac{L}{D} \cdot \frac{v^2}{2g}$$

*Where:*
* **$f$** = Friction factor (dimensionless)
* **$L$** = Pipe length (metres)
* **$D$** = Internal pipe diameter (metres)
* **$v$** = Water velocity (m/s)
* **$g$** = Gravitational acceleration ($9.81 \text{ m/s}^2$)

---

## 🔍 Solving the Friction Factor ($f$)

To calculate energy loss, we must find the friction factor ($f$). The calculation changes depending on how turbulent the water flow is, which is determined by the **Reynolds Number ($Re$)**:

1. **Laminar Flow (Smooth Flow: $Re \le 2100$):** Solved easily and directly using the **Hagen-Poiseuille equation**:
   $$f = \frac{64}{Re}$$

2. **Turbulent Flow (Rough Flow: $Re > 4000$):** The friction factor becomes complex and hidden inside the **Colebrook-White equation**:
   $$F(f) = \frac{1}{\sqrt{f}} + 2 \log_{10} \left( \frac{\varepsilon}{3.71 D} + \frac{2.51}{Re \sqrt{f}} \right) = 0$$

### 🛠️ Manual Numerical Solution (Newton-Raphson Method)
Because $f$ cannot be solved directly by basic algebra in turbulent flows, this project applies the **Newton-Raphson iterative method** to calculate it manually. 

We use the calculus formula $f_{n+1} = f_n - \frac{F(f_n)}{F'(f_n)}$ by deriving the exact mathematical derivative ($F'(f)$) by hand:
$$F'(f) = -\frac{1}{2}f^{-3/2} - \frac{2}{\ln(10)} \cdot \left( \frac{\varepsilon}{3.71 D} + \frac{2.51}{Re \sqrt{f}} \right)^{-1} \cdot \left( -\frac{1}{2} \cdot \frac{2.51}{Re} \cdot f^{-3/2} \right)$$

---

## 📈 Key Outcomes
* **Pure Analytical Models:** Completely derived multi-variable flow networks by hand without relying on pre-built software libraries.
* **Sensitivity Evaluations:** Proved mathematically how structural pipe roughness ($\varepsilon$) scales energy loss over long distances.
