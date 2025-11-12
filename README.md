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

The model can be separated into two fundamental components:

---

#### 🔹 **A. Base Ray (Linear Component)**

This represents the *core direction* of the curve — a straight ray extending at an angle θ.

<div align="center">

$$
x_{base} = t \cdot \cos(\theta) + X
$$

$$
y_{base} = 42 + t \cdot \sin(\theta)
$$

</div>

Geometrically, this is a straight line starting from the point **(X, 42)** and extending outward at an angle **θ** from the x-axis.

---

#### 🔹 **B. Oscillatory Component (Perpendicular Wobble)**

This component introduces a sinusoidal side-to-side “wobble” that is **perpendicular** to the base ray.

<div align="center">

$$
x_{pert} = -e^{Mt} \cdot \sin(0.3t) \cdot \sin(\theta)
$$

$$
y_{pert} = e^{Mt} \cdot \sin(0.3t) \cdot \cos(\theta)
$$

</div>

This perturbation term causes the path to oscillate orthogonally around the base line.  
The exponential term \( e^{Mt} \) modulates the amplitude of this oscillation:

- If **M > 0** → oscillations gradually **increase** in amplitude (growth).  
- If **M < 0** → oscillations **decay** smoothly (damping).  
- If **M ≈ 0** → oscillations remain nearly constant.

Hence, the entire structure can be viewed as a **wavy line tilted at angle θ**, with a controlled amplitude scaling over time.


---

### 4. Parameter Constraints

The model parameters are restricted to the following valid ranges (all angles in degrees unless stated otherwise):

| Parameter | Symbol | Range | Description |
|------------|:-------:|:-------------------:|-----------------------------|
| Angle ( θ) |   θ |  0 <  θ < 50  | Orientation (tilt) of the base ray in the XY plane |
| Modulation Factor |  M  |  -0.05 < M < 0.05  | Controls exponential growth/decay of the oscillation amplitude |
| Horizontal Offset |  X  |  0 < X < 100  | Horizontal translation of the entire curve (origin at (X, 42)) |

These bounds keep the model stable and ensure the oscillations remain subtle rather than diverging.


</div>

These bounds ensure that:
- The oscillation remains **subtle** and **bounded**.  
- The model maintains **numerical stability** during optimization.  
- The resulting shape visually aligns with realistic geometric behavior.

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
## 📊 Exploratory Data Analysis (EDA)

### 1️⃣ Overview of the Dataset
The dataset `xy_data.csv` contains **1,000 coordinate points** \((x_i, y_i)\) that represent samples of a smooth parametric curve generated from the model:

$$
x(t) = t\cos(\theta) - e^{Mt}\sin(0.3t)\sin(\theta) + X
$$

$$
y(t) = 42 + t\sin(\theta) + e^{Mt}\sin(0.3t)\cos(\theta)
$$



Each pair \((x_i, y_i)\) lies somewhere along this curve, but **the parameter \(t_i\)** for each point is **unknown** — this makes it a *curve-fitting without correspondence* problem.

---

### 2️⃣ Key Observations from the Data
After loading and inspecting the data, the following general properties are observed:

| Statistic | X Coordinate | Y Coordinate |
|:-----------|:-------------:|:-------------:|
| **Count** | 1000 | 1000 |
| **Mean** | 82.50 | 58.01 |
| **Standard Deviation** | 11.53 | 7.92 |
| **Minimum** | 59.66 | 46.03 |
| **Maximum** | 109.23 | 69.69 |
| **Median (50%)** | 83.95 | 57.46 |

*(These values come from programmatic analysis in Colab using Pandas.)*

---

### 3️⃣ Visual Characteristics
- The data points form a **wavy, elongated pattern** extending diagonally from the lower-left to upper-right region of the XY-plane.  
- The **spread in X (≈50 units)** is roughly double that of Y (≈24 units), indicating the curve is **shallowly inclined** — consistent with a small θ (≈25°).  
- The **oscillations** are visible as small periodic fluctuations perpendicular to the main diagonal line.  
- The dataset is **unordered**, meaning points are not sorted by the parameter \(t\).  

This unordered nature makes a standard regression \(x(t), y(t)\) impossible — the optimization must instead match the curve to the *shape* of the point cloud, not to individual indices.

---

### 4️⃣ Insights for Parameter Estimation
- **θ (Theta):**  
  The average slope of the data cloud (\(Delta y / Delta x \approx 0.47\)) corresponds to a θ of roughly **25°**, which provides a strong initial guess.

- **X (Offset):**  
  The horizontal midpoint of the cloud (≈82.5 mean) and base level at y=42 suggest **X ≈ 49**.

- **M (Modulation):**  
  The oscillation amplitude slightly decreases as x increases — implying **M is slightly negative**, i.e., mild damping in oscillations.

These rough estimates will be refined through numerical optimization in the next stage.

---

### 5️⃣ Visual Summary (Descriptive)
| Feature | Interpretation |
|:--------|:----------------|
| **Shape** | Smooth oscillating line |
| **Angle** | ≈ 25° inclination |
| **Oscillation** | Small perpendicular “wave” pattern |
| **Trend** | Slightly damped amplitude (M < 0) |
| **Data Type** | Unordered 2D coordinates |

---

### ✅ Summary
The Exploratory Data Analysis (EDA) establishes that:
- The dataset is a **noisy but structured point cloud** around a tilted oscillating curve.  
- The values of θ and X can be **approximated from geometry**, while M requires **numerical fitting**.  
- These insights provide a strong foundation for defining the **cost function** and **optimization process** in the following stage.

---
## ✅ Final Results and Submission

**Final optimized parameters (after hybrid search + Nelder–Mead refinement):**

| Parameter | Value |
|-----------|-------:|
| Theta (deg) | 30.000445 |
| Theta (rad) | 0.523608 |
| M | 0.030000 |
| X | 55.000783 |

**Final performance**
- Exact Mean L1 (Chamfer, n_pred = 1500): **0.01342545**  
- KDTree (approx) Mean L1 reported during optimization: **0.016737**

**Files (in repo)**
- `Parametric_Model_Assignment.ipynb` — full Colab notebook with code + results  
- `xy_data.csv` — raw dataset  
- `plots/data_distribution.png` — scatter of raw data  
- `plots/initial_model_fit.png` — initial guess overlay  
- `plots/final_fit.png` — final fitted curve overlay  
- `plots/residuals_hist.png` — final residual histogram  
- `results/final_params.txt` — plain text with final parameter values

**Desmos visualization**  
Interactive Desmos plot of the final parametric curve:  
👉 [View on Desmos](https://www.desmos.com/calculator/r3bgquhfam)

**Short method summary**  
We used a Chamfer-style L1 cost with KDTree for nearest neighbor search and a two-stage optimization:  
(1) random coarse search for good seeds and (2) Nelder–Mead local refinement.  
Final validation used an exact L1 Chamfer on 1500 sampled points, giving mean L1 ≈ 0.0134.











