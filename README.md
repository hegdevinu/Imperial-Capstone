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
* `/capstone_data`: Raw `.npy` files for all 20 observations.
* `/visuals`: Convergence plots and GP uncertainty maps.
* `CHANGELOG.md`: Detailed week-by-week decision log for all 8 functions.

---
