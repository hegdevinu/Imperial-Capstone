# 🌌 Navigating the High-Dimensional Unknown
### **BBO Capstone Project | Imperial College London**

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Python: 3.8+](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Status: Success](https://img.shields.io/badge/Status-Project_Completed-green.svg)

> **"MY KEY LEARNING - In Black-Box Optimization, data is expensive and cliffs are everywhere. Success is not just finding the peak; it's building the map that gets you there safely."**

---

## 🏆 Comprehensive Leaderboard Performance Audit

This table provides a transparent audit of my performance across all 8 functions. 

| Function | Complexity | **Final Rank** | **Best Score** | **Strategic Status** | **The Technical Highlight** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **F1** | 2D | **#6** | 0.6766 | **✅ Success** | Targeted the "Needle" center using High-Resolution Slicing. |
| **F2** | 2D | **#13** | 0.7426 | **⚡ Breakthrough** | Used **Midpoint Bracketing** to jump +21% over previous best. |
| **F3** | 3D | **#5** | -0.0013 | **✅ Success** | Reached the theoretical stability ceiling for drug discovery. |
| **F4** | 4D | **#3** | 0.6899 | **🚀 Major Success** | **Recovery Mastery:** Reclaimed top-3 after a mid-project crash to -22.1. |
| **F5** | 4D | **#45** | 2939.99 | **❌ Failure** | **Local Optima Trap:** Scaled a "Chimney" ridge but missed the global spike. |
| **F6** | 5D | **#11** | -0.1443 | **🔄 Recovery** | Balanced yield against steep cliffs to return to a stable peak. |
| **F7** | 6D | **#25** | 2.3613 | **⚠️ Stalled** | **Plateau Trap:** Maintained stability but failed to scale the final summit. |
| **F8** | 8D | **#4** | 9.9922 | **🚀 Major Success** | **Precision Lock:** 6-decimal convergence via Dimensionality Freezing. |

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

## 🔍 Critical Analysis: Successes vs. Failures

### **The Masterstrokes (F4, F8, F2)**
* **The Pivot (Function 4):** The defining effort of the project. After hitting a hidden "cliff" (-22.1), I realized the model was over-fitting to outliers. By implementing a **Trust-Region Constraint**, I manually "fenced in" the optimizer, forcing it to climb back safely from the abyss.
* **Dimensionality Freezing (Function 8):** In a massive 8D search space, traditional exploration is a "hit or miss" game. I utilized **Sobol Sensitivity Analysis** to identify the "Master Knobs." By freezing 6 of the 8 variables, I transformed an impossible 8D search into a high-precision 2D strike.



### **The "Local Optima" Lessons (F5, F7)**
* **The Chimney Trap (Function 5):** While my final yield of 2939.99 was a local record, the leaderboard reveals this was a failure of global exploration. My model identified an aggressive "ridge" and I exploited it prematurely, missing a much sharper, high-magnitude peak elsewhere. This taught me that **premature exploitation** is the greatest risk in exponential landscapes.
* **The Plateau (Function 7):** In the 6D space, my strategy became too conservative. I stayed on the "High Ground" to protect my score, but failed to venture into the high-variance zones that likely held the global maximum.

---

## ⛰️ Visual Evidence: Mapping the Search

Success was driven by **Terrain Slicing**. I generated 3D topography maps using Gaussian Process predictions to visualize the landscape. Crucially, my process distinguished between:

1.  **Base Data:** The initial "cold start" points provided.
2.  **Historical Queries:** The iterative path (and mistakes) taken over 13 weeks.
3.  **The Recommendation:** The final "Summit Strike" target based on the highest **Probability of Improvement (PI)**.

![Function 1 Terrain Analysis](../visuals/F1_terrain_analysis.png)
![Function 2 Terrain Analysis](../visuals/F2_terrain_analysis.png)
![Function 3 Terrain Analysis](../visuals/F3_terrain_analysis.png)
![Function 4 Terrain Analysis](../visuals/F4_terrain_analysis.png)
![Function 5 Terrain Analysis](../visuals/F5_terrain_analysis.png)
![Function 6 Terrain Analysis](../visuals/F6_terrain_analysis.png)
![Function 7 Terrain Analysis](../visuals/F7_terrain_analysis.png)
![Function 8 Terrain Analysis](../visuals/F8_terrain_analysis.png)

---

## 🛠️ Technical Methodology & Rationale

The optimization engine was built from the ground up on three pillars of Bayesian Optimization (BO) theory, prioritizing transparency and manual control over high-level automation.

### **A. Surrogate Modeling: Gaussian Process (GP)**
I utilized **Gaussian Process Regression** (via `scikit-learn`) as the core surrogate model. GPs were selected because they provide a full probability distribution over the function space, allowing for formal **Uncertainty Quantification (UQ)**.

* **Kernel Selection:** I implemented the **Matérn 5/2 kernel**. Unlike the Squared Exponential kernel, the Matérn 5/2 does not assume infinite smoothness, making it the preferred choice in BBO literature (*Snoek et al., 2012*) for handling the "cliffs" and non-smooth transitions observed in Functions 4 and 7.
* **ARD (Automatic Relevance Determination):** I enabled ARD to automatically tune the length-scale for each dimension, identifying which "knobs" were most sensitive before performing deeper sensitivity analysis.

### **B. Decision Logic: Strategic Acquisition**
The search path was driven by a dynamic blend of **Expected Improvement (EI)** and **Upper Confidence Bound (UCB)**. Unlike a simple "Greedy" search, these functions naturally account for the "Exploration-Exploitation" trade-off.

* **The Trust-Region Constraint:** Following the critical "Week 8 Regression," I transitioned from a global search to a **Trust-Region approach** (*Eichfelder, 2008*). By limiting the acquisition function’s search radius to a specific area around known optima, I stabilized the model and prevented the optimizer from over-fitting to outliers in high-stakes dimensions.

### **C. High-Dimensionality: The "Master Knob" Strategy**
To combat the **Curse of Dimensionality** in the 8D Architect (Function 8), I applied **Sobol Sensitivity Analysis** (*Sobol, 2001*) to perform "Dimensionality Freezing."

1.  **Sensitivity Mapping:** I identified that dimensions $x_5$ and $x_8$ accounted for over 90% of total variance.
2.  **Dimensionality Reduction:** By locking the 6 "low-impact" dimensions to their best-known values, I transformed an impossible 8D search into a high-precision 2D strike. 
3.  **Micro-Tuning:** This enabled the 6-decimal precision needed to hit the **9.9922** peak in the final weeks.

---

## 📂 Project Structure

```bash
├── notebooks/          # Chronological record of effort (Weeks 1-13)
├── visuals/            # GP Slices & Topography Maps
├── capstone_data/      # initial_data & weekly_updates
├── scripts/            # Python scripts for automated data management and sensitivity modeling.
├── README.md           # Executive Project Case Study
├── MODEL_CARD.md       # Detailed deep-dive into the CTR-GPBO strategy.
└── CHANGELOG.md        # Week-by-week audit trail of optimization decisions.
