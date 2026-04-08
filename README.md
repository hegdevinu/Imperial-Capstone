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

---
