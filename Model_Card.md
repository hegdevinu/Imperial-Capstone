# Model Card: Custom Gaussian Process Optimisation Engine

## Model Description

**Input:** Continuous numerical vectors representing multi-dimensional search coordinate spaces ranging from 2D (Functions 1 & 2) up to 8D (Function 8). The input space boundaries are bounded according to specific system design limits (e.g., coordinate constraints for warehouse layouts, chemical mixture ratios, and hyperparameter bounding boxes).

**Output:** A scalar value $y$ representing an unobserved black-box target performance metric, including radioactive intensity (F1), log-likelihood score (F2), drug discovery chemical stability (F3), warehouse storage efficiency (F4), manufacturing process yield (F5), recipe rating (F6), and machine learning hyperparameter scores (F7 & F8).

**Model Architecture:**
The surrogate model is built from the ground up using a non-automated **Gaussian Process Regressor (GPR)** via `scikit-learn`.
* **Kernel Configuration:** A foundational **Matérn 5/2 kernel** combined with an automated white-noise variance parameter. The Matérn 5/2 kernel was selected globally because it relaxes the infinite differentiability assumption of the Squared Exponential kernel, allowing the model to adapt gracefully to the sharp, non-smooth gradients ("cliffs") observed across the landscapes.
* **Dimensionality Management:** Employs **Automatic Relevance Determination (ARD)** via custom length-scale vectors for coordinate pruning, paired with an upstream analytical **Sobol Sensitivity Analysis** routine for high-dimensional structures.
* **Decision Framework (Acquisition):** A dynamic, manually adjusted framework blending **Expected Improvement (EI)** and **Upper Confidence Bound (UCB)** algorithms to balance exploration and exploitation phases over a 13-week loop.

---

## Performance

The engine's performance is measured using absolute yield improvement from a sparse "cold start" baseline over 13 evaluation iterations, verified directly against the live Imperial Capstone leaderboard.

### Key Performance Milestones:
* **High-Dimensional Scaling (Function 8 - 8D):** Achieved a **#4 global rank (9.9922)** by successfully compressing an intractable 8-dimensional hyperspace into a localized 2D coordinate search.
* **Resilient Path Correction (Function 4 - 4D):** Successfully executed a recovery maneuver following an early exploration crash to a score of $-22.1$, utilizing localized optimization to secure a **#3 global rank (0.6899)**.
* **Exponential Climb (Function 5 - 4D):** Discovered an aggressive upward trend line to achieve an absolute local processing yield peak of **2939.99**.

---

## Limitations

* **Sparse-Data Myopia:** The model relies heavily on early sampling coverage. If the initial dataset misses a high-frequency region entirely, the Gaussian Process can construct a prematurely flattened representation of that zone.
* **Sensitivity to Noise Calibration:** In heavily randomized environments, if the white-noise parameter is set too low, the model mistakes stochastic variations for true performance indicators, leading it to track false peaks.
* **Curse of Dimensionality:** In higher-dimensional realms (such as the 6D and 8D spaces), the mathematical volume of the search environment expands exponentially, causing standard acquisition strategies to stall without manual coordinate reduction.

---

## Trade-offs

* **Safety vs. Peak Discovery (The Trust-Region Trade-off):** Implementing a localized **Hard-Bound Trust Region** after structural drops effectively ensures system safety and guarantees steady, incremental progress. However, this localized approach trades away global exploration capabilities, preventing the engine from locating alternative, potentially higher peaks across different regions of the landscape.
* **Exploitation Speed vs. Horizon Horizons:** Shifting acquisition parameters heavily toward immediate exploitation (e.g., aggressively lowering the UCB $\kappa$ parameter) secures fast local progress, but risks trapping the model on a local ridge—as observed during the Function 5 optimization run.