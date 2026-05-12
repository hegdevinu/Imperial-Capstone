# 🚀 Bayesian Optimization: The Black-Box Capstone Project
### **Imperial College London | Machine Learning Portfolio**

**Author:** Vinayak Hegde  
**Final Leaderboard Standing:** #2 (Function 4) | #3 (Function 8)  
**Objective:** Navigate 8 high-dimensional unknown "Black-Box" landscapes to find absolute global maximums using sparse data and Gaussian Processes.

---

## 🏆 Final Results at a Glance
| Function | Complexity | Initial Best | **Final Week 13** | Outcome / Insight |
| :--- | :--- | :--- | :--- | :--- |
| **F1** | 2D | 0.0036 | **0.6766** | **Needle Strike:** Captured the high-intensity spike. |
| **F2** | 2D | 0.6112 | **0.7426** | **Bracket Success:** Midpoint logic hit the summit. |
| **F3** | 3D | -0.0348 | **-0.0013** | Reached the theoretical chemical stability ceiling. |
| **F4** | 4D | -6.7021 | **0.6899** | **#2 Rank:** Recovered from a catastrophic -22.1 crash. |
| **F5** | 4D | 1088.8 | **2939.9** | **Ridge Scaling:** Successfully scaled exponential ridge. |
| **F6** | 5D | -0.7142 | **-0.1443** | Reclaimed original peak after local saddle divergence. |
| **F7** | 6D | 1.3649 | **2.3613** | Maintained steady yield on the 6D plateau. |
| ****F8** | 8D | 9.5984 | **9.9922** | **#3 Rank:** Mastered precision via dimensionality freezing. |

---

## 🧠 Optimization Strategy & Methodology

My approach evolved from broad stochastic scouting in the early weeks to a high-precision **Trust-Region Bayesian Optimization** framework.

### **1. The "Trust-Region" Pivot (Resilience)**
In Week 8, Function 4 suffered a massive regression (-22.1). I moved from global exploration to a **Hard-Bound Trust Region**, manually constraining the search to a 5% radius around historical successes. This allowed for the massive recovery seen in the final results.

### **2. Dimensionality Freezing (Combatting the Curse)**
To handle the 8D complexity of Function 8, I utilized **Sobol Sensitivity Analysis**. By identifying that $x_5$ and $x_8$ were the primary "Master Knobs" driving variance, I locked the other six dimensions, allowing the model to converge on the **9.9922** peak.

### **3. Terrain Analysis & Slicing**
I utilized **Gaussian Process Slicing** to generate 3D topography maps. By holding non-critical variables at their optimal values, I could visualize the "ridges" and "valleys," justifying aggressive moves in Functions 2 and 5.

---

## 🛠️ Repository Structure

```text
├── notebooks/          # Weekly iteration logs (F1 to F8)
├── capstone_data/      # Normalized .npy data files for all 13 weeks
├── visuals/            # 3D terrain maps & convergence reports
├── scripts/            # Automated data_manager.py for syncing
└── README.md           # Project executive summary













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
