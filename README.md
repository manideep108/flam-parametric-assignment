# flam-parametric-assignment
Research &amp; Development assignment – Determination of unknown parameters (θ, M, X) in a parametric model using L1 optimization.
## 🧮 Theoretical Analysis of the Parametric Model

### 1. Simplification of the Given Model
The given curve is defined by the following parametric equations:

x = t * cos(theta) - exp(M * |t|) * sin(0.3 * t) * sin(theta) + X  
y = 42 + t * sin(theta) + exp(M * |t|) * sin(0.3 * t) * cos(theta)

Since t lies in the range 6 < t < 60, all values of t are positive.  
Hence, |t| = t, and the model simplifies to:

x(t) = t * cos(theta) - exp(M * t) * sin(0.3 * t) * sin(theta) + X  
y(t) = 42 + t * sin(theta) + exp(M * t) * sin(0.3 * t) * cos(theta)

---

### 2. Role of the Unknown Parameters
| Parameter | Symbol | Function | Description |
|------------|:-------:|:----------|:-------------|
| **Theta (θ)** | θ | Rotation | Defines the overall orientation (tilt) of the curve in the XY plane. |
| **Modulation (M)** | M | Growth/Decay | Controls how the amplitude of the oscillation grows (M > 0) or decays (M < 0) as t increases. |
| **Offset (X)** | X | Translation | Horizontally shifts the entire curve left or right. |

---

### 3. Geometric Interpretation
The model can be separated into two distinct parts:

**A. Base Ray (Linear Component):**
x_base = t * cos(theta) + X  
y_base = 42 + t * sin(theta)

This represents a straight line (or “ray”) starting from point (X, 42) and extending outward at an angle theta.

**B. Oscillatory Component (Perpendicular Wobble):**
x_pert = -exp(M * t) * sin(0.3 * t) * sin(theta)  
y_pert = exp(M * t) * sin(0.3 * t) * cos(theta)

This term adds a sinusoidal “wobble” perpendicular to the base line.  
Together, the curve can be visualized as a **wavy line tilted at angle theta**, with its amplitude slightly increasing or decreasing depending on the sign of M.

---

### 4. Parameter Constraints
0° < θ < 50°  
-0.05 < M < 0.05  
0 < X < 100  

These narrow bounds ensure that the model remains stable and the oscillations stay subtle rather than diverging.

---

### 5. Conceptual Summary
- The **base ray** defines the direction and linear growth of the curve.  
- The **oscillatory term** introduces periodic side-to-side variations.  
- The **angle (θ)** sets orientation, **M** defines smooth exponential scaling of the oscillations, and **X** shifts the entire structure horizontally.  

Together, they create a controlled oscillating curve that aligns closely with the given dataset.


