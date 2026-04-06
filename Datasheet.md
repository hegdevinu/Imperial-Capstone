# Datasheet: BBO Capstone Dataset
**Dataset Owner:** Vinayak Hegde | **Last Updated:** April 2026

---

## Motivation
* **Purpose:** This dataset was created to provide a benchmark for **low-data optimization**. 
* **Task Support:** It documents the trajectory of an optimiser navigating eight distinct mathematical landscapes under a strict 20-query budget.
* **Funding:** Produced as part of the 2026 Imperial BBO Capstone Project.

## Composition
* **Observations:** 20 points per function (160 total observations).
* **Features:** $d$-dimensional input vectors $X \in [0, 1]^d$ and scalar output $y$.
* **Dimensionality:** Functions span 2D, 3D, 4D, 5D, 6D, and 8D search spaces.
* **Format:** Provided in `.npy` (NumPy) for computation and `.csv` for readability.
* **Gaps:** There is an inherent "exploration gap" in high-dimensional functions (F7, F8) where 20-40 points cannot fully map the surface.

## Collection Process
* **Mechanism:** Queries were generated via the **CTR-GPBO** model (see Model Card).
* **Strategy:** Sequential optimisation where each query $x_{n+1}$ is conditioned on the full history $\{x_{1 \dots n}, y_{1 \dots n}\}$.
* **Noise Handling:** Function 2 was identified as a heteroscedastic environment, requiring a noise-alpha adjustment of 0.1 to prevent overfitting.
* **Validation:** Every coordinate was manually verified against $[0.0, 1.0]$ boundary constraints.

## Preprocessing and Uses
* **Transformations:** Input features are normalized to $[0, 1]$. No output transformations were applied to ensure raw physical/chemical signals remained interpretable.
* **Intended Use:** Analyzing convergence behavior and "recovery" strategies in Bayesian Optimization.
* **Inappropriate Use:** Training Deep Neural Networks; the dataset size is insufficient for gradient-based weight updates.

## Distribution & Maintenance
* **Repository:** Publicly available on GitHub.
* **License:** MIT License.
* **Maintenance:** The dataset is static and final as of Week 13. 
* **Contact:** [[https://github.com/hegdevinu]]
