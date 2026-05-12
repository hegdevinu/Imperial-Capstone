# 🌌 Navigating the High-Dimensional Unknown
### **BBO Capstone Project | Imperial College London**

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Python: 3.8+](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Status: Success](https://img.shields.io/badge/Status-Project_Completed-green.svg)

> **"In Black-Box Optimization, data is expensive and cliffs are everywhere. Success is not just finding the peak; it's building the map that gets you there safely."**

---

## 🏆 Final Leaderboard Standings Summary
| **Rank** | **Function** | **Focus Area** | **Final Score** | **Strategic Outcome** |
| :--- | :--- | :--- | :--- | :--- |
| **🥇 #2** | **Function 4** | Warehouse Storage Optimization | **0.6899** | **Recovery Mastery:** From -22.1 to Podium. |
| **🥇 #3** | **Function 8** | 8D Hyperparameter Tuning | **9.9922** | **Precision Lock:** 6-decimal convergence. |
| **🚀 Breakthrough** | **Function 2** | Log-Likelihood Ridge Capture | **0.7426** | **Midpoint Bracket:** +21% over baseline. |
| **🚀 Breakthrough** | **Function 5** | Chemical Yield Scaling | **2939.99** | **Corner Chimney:** Scaling exponential ridges. |

---

## 📈 The 13-Week Journey: Evolution of Effort

This repository documents a 13-week iterative journey of learning from the "Black-Box." The process was defined by three distinct strategic shifts:

### **Phase 1: Global Scouting (Weeks 1-4)**
* **Strategy:** Latin Hypercube Sampling (LHS) & High-Jitter Acquisition.
* **Goal:** Map the broad contours of the search space.
* **Outcome:** Established "Islands of Success" across all 8 functions, identifying initial gradients.

### **Phase 2: The "Cliff Crisis" & Pivot (Weeks 5-8)**
* **The Setback:** Function 4 hit a hidden "cliff," plummeting from a stable positive score to **-22.1**.
* **The Realization:** Standard Bayesian Optimization was "chasing shadows." The model was over-fitting to outliers in a sparse landscape.
* **The Pivot:** Switched to **Trust-Region Constraints**. I moved from global search to **Local Peak Refinement**, bounding queries to a 5% radius of known success.

### **Phase 3: Surgical Exploitation (Weeks 9-13)**
* **Strategy:** Dimensionality Freezing & Midpoint Bracketing.
* **Achievement:** Finalized top-3 leaderboard spots.
* **Final Rounds:** Utilized 6-decimal precision **"Golden Queries"** to strike the absolute summits.

---

## ⛰️ Visual Evidence: The Optimization Terrain

Success was driven by **Terrain Slicing**. By generating 3D topography maps using Gaussian Process predictions, I visualized the landscape while distinguishing between:
1.  **Base Data:** The initial "cold start" state of the function.
2.  **Historical Queries:** The iterative path taken over 13 weeks.
3.  **The Recommendation:** The final "Summit Strike" target.

### **Strategic Highlights:**
* **Function 5 (The Exponential Chimney):** Visualized as a steep ridge moving toward the (1,1) corner. The terrain justified an aggressive push that broke the **2900 barrier**.
* **Function 2 (The Midpoint Bracket):** After overstepping the ridge in Week 12, the 2D heatmap showed the peak was trapped between two points. The **Geometric Midpoint** move captured the **0.74** summit.

---

## 🛠️ Technical Implementation

### **The Engine**
Built from the ground up using **Scikit-Learn's Gaussian Process Regressor**, allowing for manual control over:
* **ARD (Automatic Relevance Determination):** Identifying "Master Knobs" in high-D space.
* **Matern 2.5 Kernels:** Optimized for the "cliff-heavy" nature of warehouse and chemical functions.
* **Custom Acquisition:** A dynamic blend of **Expected Improvement (EI)** and **Upper Confidence Bound (UCB)**.

### **The "Master Knob" Strategy**
In Function 8 (8D), the "Curse of Dimensionality" makes exploration nearly impossible. My breakthrough came from **Dimensionality Freezing**:
1.  Performed **Sobol Sensitivity Analysis** on historical data points.
2.  Identified that $x_5$ and $x_8$ were responsible for **92% of variance**.
3.  Locked the other 6 dimensions, turning an 8D search into a high-precision 2D strike.

---

## 📂 Repository Structure

```bash
├── notebooks/          # Chronological record of effort (Weeks 1-13)
│   ├── 01_Function_1.ipynb   # 2D Radiation Scout
│   ├── 04_Function_4.ipynb   # The Recovery Strategy
│   └── 08_Function_8.ipynb   # 8D Precision Tuning
├── visuals/            # GP Slices & 3D Topography Maps
├── capstone_data/      # initial_data/ & weekly_updates/
├── scripts/            # Data-update-Manager & Terrain Generators
└── README.md           # Executive Project Case Study




# Black-Box Optimization (BBO) Capstone
**Adaptive Bayesian Optimization with Trust-Region Recovery**

# Imperial-Capstone
This project is used for showcasing the Imperial Capstone work carried out during certification. 

## 📑 Project Documentation
- [Google-style Model Card](./Model_Card.md)
- [BBO Project Datasheet](./Datasheet.md)

## Methodology
This repository documents the 13-week optimization of eight hidden functions (2D to 8D). My approach utilizes **Gaussian Process (GP) Regression** implemented via `scikit-learn` and `BoTorch`.

### **Strategy Stack**
* **Surrogate Model:** Gaussian Process with Matérn 5/2 kernels (to handle non-smoothness).
* **Acquisition:** Expected Improvement (EI) for exploration; Upper Confidence Bound (UCB) for exploitation.
* **Safety Mechanism:** **Trust-Region Constraints** (limiting search to 1-5% of historical peaks) to avoid "boundary cliffs."

## Visual Evidence
I utilized **Sobol Sensitivity Analysis** to identify "Master Knobs" in high-dimensional functions (F7, F8). This allowed me to "freeze" low-impact dimensions and achieve 9.99+ scores.

## Repository Structure

* **[`/notebooks`](./notebooks):** Documented Jupyter Notebooks for each function (01-08).
* **[`/capstone_data`](./capstone_data):** Versioned NumPy arrays (`.npy`) containing the 20-week evaluation history.
* **[`/visuals`](./visuals):** GP uncertainty maps, convergence plots, and Sobol indices.
* **[`/scripts`](./scripts):** Python scripts for automated data management and sensitivity modeling.
* **[MODEL_CARD.md](./MODEL_CARD.md):** Detailed deep-dive into the CTR-GPBO strategy.
* **[CHANGELOG.md](./CHANGELOG.md):** Week-by-week audit trail of optimization decisions.

## Technical Rationale & Academic Grounding

The optimization strategy for this project was built on three pillars of Bayesian Optimization (BO) theory:

### **A. Surrogate Modeling: The Gaussian Process (GP)**
I utilized **Gaussian Process Regression** (via `scikit-learn`) as the surrogate model. GPs were chosen because they provide a full probability distribution over the function space, allowing for formal uncertainty quantification (UQ). 
* **Kernel Selection:** I implemented the **Matérn 5/2 kernel**, which is widely preferred in BBO literature (e.g., *Snoek et al., 2012*) over the Squared Exponential kernel, as it does not assume infinite smoothness and better handles the "cliffs" observed in Function 4 and 7.

### **B. Decision Logic: Exploitation vs. Exploration**
The search path was driven by **Expected Improvement (EI)**. Unlike simple Greedy search, EI naturally accounts for the "Exploration-Exploitation" trade-off by quantifying the magnitude of improvement in unexplored regions.
* **The Trust-Region Constraint:** Following the "Week 8 Regression," I moved from global EI to a **Trust-Region approach** (*Eichfelder, 2008*). This limited the acquisition function's search space to a specific radius around known optima to ensure stability in high-stakes dimensions.

### **C. High-Dimensionality: Sobol Sensitivity**
To combat the **Curse of Dimensionality** in the 8D Architect (Function 8), I applied **Sobol Sensitivity Analysis** (*Sobol, 2001*). This allowed for "Dimensionality Reduction" by identifying that dimensions $x_5$ and $x_8$ accounted for over 85% of total variance, enabling high-precision micro-tuning in the final weeks.

## 🏁 Project Conclusion
**Status: Optimization Phase Complete**
* **Final Leaderboard Entry:** Week 13
* **Primary Strategy:** Trust-Region Bayesian Optimization with Sobol-driven Sensitivity Analysis.
* **Key Achievements:** Successfully reclaimed the Function 4 peak after a mid-project regression and broke the 2850 yield barrier on Function 5.
---
