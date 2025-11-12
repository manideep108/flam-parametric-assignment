# ⚙️ Flam Parametric Assignment

**Research & Development Assignment**  
Determination of unknown parameters **(θ, M, X)** in a complex **parametric model** using **L1 optimization**.

---

## 🧮 Theoretical Analysis of the Parametric Model

### 1️⃣ Simplification of the Given Model

The given curve is defined by the following parametric equations:

$$
x = t \cdot \cos(\theta) - e^{M|t|} \cdot \sin(0.3t) \cdot \sin(\theta) + X
$$

$$
y = 42 + t \cdot \sin(\theta) + e^{M|t|} \cdot \sin(0.3t) \cdot \cos(\theta)
$$

Since \( 6 < t < 60 \), the value of \( |t| = t \).  
Hence, the model simplifies to:

$$
x(t) = t\cos(\theta) - e^{Mt}\sin(0.3t)\sin(\theta) + X
$$

$$
y(t) = 42 + t\sin(\theta) + e^{Mt}\sin(0.3t)\cos(\theta)
$$

---

### 2️⃣ Role of the Unknown Parameters

| Parameter | Symbol | Function | Description |
|------------|:-------:|:----------|:-------------|
| **Theta (θ)** | θ | Rotation | Defines the overall orientation (tilt) of the curve in the XY plane. |
| **Modulation (M)** | M | Growth / Decay | Controls how the oscillation amplitude grows (M > 0) or decays (M < 0) as *t* increases. |
| **Offset (X)** | X | Translation | Horizontally shifts the entire curve without changing its shape. |

---

### 3️⃣ Geometric Interpretation

The model can be separated into two components:

#### 🔹 A. Base Ray (Linear Component)
$$
x_{base} = t\cos(\theta) + X
$$

$$
y_{base} = 42 + t\sin(\theta)
$$
This represents a straight line (a *ray*) starting from the point \( (X, 42) \) and extending outward at an angle θ.

#### 🔹 B. Oscillatory Component (Perpendicular Wobble)
$$
x_{pert} = -e^{Mt}\sin(0.3t)\sin(\theta)
$$
$$
y_{pert} = e^{Mt}\sin(0.3t)\cos(\theta)
$$
This adds a sinusoidal “wobble” perpendicular to the base ray.  
The overall shape can be visualized as a **wavy line tilted at angle θ**, where the amplitude of the oscillation slightly increases or decreases depending on the sign of M.

---

### 4️⃣ Parameter Constraints

$$
0° < \theta < 50° \\
-0.05 < M < 0.05 \\
0 < X < 100
$$

These bounds ensure that the oscillation remains subtle and the model stable.

---

### 5️⃣ Conceptual Summary

- The **base ray** defines the main direction and linear growth of the curve.  
- The **oscillatory term** introduces a side-to-side periodic variation.  
- The **angle (θ)** rotates the structure, **M** controls the amplitude’s exponential scaling, and **X** horizontally shifts the entire curve.  

In essence, this model describes a *controlled oscillating line* that follows a linear path while performing a smooth perpendicular wave motion.

---

### 🧩 Visual Overview

| Concept | Description |
|----------|--------------|
| **Type of model** | Parametric 2D curve |
| **Nature** | Oscillatory + Exponential scaling |
| **Domain of t** | \(6 < t < 60\) |
| **Optimization target** | Minimize L1 (mean absolute) distance between observed and predicted points |

---

### ✅ Summary of This Section

- Equations simplified for computational use.  
- Role and influence of each parameter clearly identified.  
- Mathematical interpretation linked to geometric intuition.  
- Parameter constraints finalized for optimization search space.

---




