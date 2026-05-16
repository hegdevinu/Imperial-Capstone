# Datasheet: Black-Box Exploration Dataset

## Function Overview

1. **Which function does this datasheet describe?**
   This master datasheet tracks the aggregate optimisation profiles for **Functions 1 through 8** evaluated during the 13-week Black-Box Optimisation challenge.

2. **What real-world scenario does this function simulate?**
   The dataset spans multiple simulated engineering and scientific domains:
   * **Low-D (2D–3D):** Radiation source localization (F1), Log-likelihood tracking (F2), and biochemical drug discovery (F3).
   * **Mid-D (4D–5D):** Industrial warehouse layout optimisation (F4), chemical synthesis yield scaling (F5), and culinary recipe synthesis (F6).
   * **High-D (6D–8D):** Multi-parameter machine learning model hyperparameter tuning (F7 & F8).

3. **What is the dimensionality of the input?**
   Variable across spaces, testing scalability from simple **2D coordinates** up to highly complex **8D hyperspaces**.

4. **How many initial data points were provided?**
   Each black-box function provided a sparse, historic "cold start" matrix containing a minimal collection of initial evaluations (typically between 10 to 20 samples).

5. **What does the output represent?**
   A scalar value $y$ scaling as a direct performance efficiency index or yield metric, where the core objective is absolute maximization.

---

## Nature of the Data

1. **Describe the structure of the initial dataset.**
   Structured as pair-wise normalized matrix arrays: an input coordinate tensor matching the target dimension, paired with a matching 1D matrix tracking the observed performance output ($y$).

2. **How does the dataset evolve as you add new queries weekly?**
   The dataset grew incrementally by exactly one high-precision coordinate evaluation per function every week, expanding from a sparse initial grid into localized clusters concentrated around identified ridges.

3. **Does the function include noise or randomness?**
   Yes, several functions exhibited prominent stochastic variations. This required adjusting the surrogate engine to treat observations as noisy distributions rather than absolute deterministic targets, preventing the system from over-calibrating to lucky hits.

4. **Based on observations, does the function appear unimodal, multimodal, noisy, or smooth?**
   The landscapes are highly diverse:
   * **Function 1** behaves as an isolated needle-in-a-haystack.
   * **Functions 4 and 6** feature severe non-smooth drop-offs and cliffs.
   * **Function 5** behaves as an asymmetric exponential ridge running toward a corner.
   * **Function 8** forms a smooth, high-dimensional dome.

---

## Preprocessing and Data Cleaning

1. **What preprocessing steps were applied to the initial dataset?**
   Data matrices were verified for dimensionality consistency and min-max scaled where necessary to ensure uniform spatial processing across the length-scales of the Gaussian Process.

2. **Did you normalise or transform the input features or output values?**
   Input variables were mapped dynamically using **Automatic Relevance Determination (ARD)** within the kernel setup, allowing the model to adaptively compress less responsive dimensional scales.

3. **Describe any feature engineering or dimensionality reduction techniques.**
   In the 8D hyperspace (Function 8), an analytical **Sobol Sensitivity Analysis** was performed. This mapped the variance contribution of each input variable, showing that two specific dimensions drove over 90% of system behavior. The remaining six inputs were frozen at their historical best values, transforming an intractable 8D search into a precise 2D space.

4. **Did you handle outliers or unusual data points?**
   Yes. When Function 4 recorded a catastrophic score drop to $-22.1$ due to a cliff hit, this point was retained as a critical "No-Go Zone" marker. Instead of filtering it out, the data point was used to define the boundaries of a localized **Hard-Bound Trust Region** to keep the optimizer safe.

---

## Weekly Iteration and Learning

1. How did new data points change your understanding of the function landscape?**
   Early iterations frequently disrupted the model's assumptions, shifting smooth predicted slopes into volatile, multi-peaked hills, highlighting the risk of relying on sparse initial data.

2. **Did you encounter local optima? How did you detect them?**
   Yes, most notably in **Function 5**. The model encountered an active local ridge and plateaued at a yield score of **2939.99**. Local optima were detected when subsequent expected improvement projections flattened to zero despite entering completely new coordinate zones.

3. **Which queried inputs were most informative and why?**
   Boundary and cliff edge points were highly informative for defining safety limits, while **Geometric Midpoints** proved highly effective for capturing narrow summits trapped between two known points, as shown in the Function 2 optimisation run.

4. **If you restarted, what would you do differently?**
   I would implement a more aggressive global exploration strategy during the early rounds of Function 5 to avoid becoming prematurely trapped on the corner ridge. I would also introduce an automated multi-start optimisation routine like TurBO to better balance exploration and exploitation across all functions.

---

## Performance and Results

1. **What is the best output value you achieved?**
   * **Function 4 (4D):** 0.6899
   * **Function 8 (8D):** 9.9922
   * **Function 5 (4D):** 2939.99
   * **Function 2 (2D):** 0.7426

2. **Which input vector produced this value?**
   Refer to the final week-13 configuration logs inside the respective `/notebooks` files for the exact high-precision coordinate strings.

3. **How confident are you that this is near the global maximum? Why?**
   * **Highly Confident (F4, F8):** Confirmed by top-3 and top-4 podium standings on the leaderboard, with model variance approaching zero around the target points.
   * **Moderately Confident (F5):** While the local yield score is high, the model's low rank (#45) indicates it likely settled on an impressive local ridge while missing a sharper global maximum elsewhere.

4. **Did your results align with expectations for this function?**
   Yes, the high-dimensional functions matched expectations regarding the *Curse of Dimensionality*, validating the choice to prioritize custom structural interventions over automated configurations.

---

## Ethical, Practical and General Considerations

1. **How does this black-box optimisation task relate to real-world applications?**
   The methods mirror the complex trade-offs found in industry, such as tuning hyperparameters for large language models, maximizing chemical plant throughput under strict safety limits, or optimizing physical supply chain infrastructure with limited budgets.

2. **What limitations arise from the synthetic nature of the function?**
   Synthetic benchmarks run instantly and without material expense, whereas real-world systems feature shifting parameters over time, physical wear, and massive operational costs for every evaluation.

3. **Would your strategy scale to more serious or more expensive problems?**
   Yes. By relying on custom `scikit-learn` loops and explicit mathematical techniques like Sobol analyses and Trust-Regions rather than brute-force sampling, the system is designed to maximize efficiency under tight evaluation budgets.

4. **What risks or pitfalls should a future user be aware of when analysing this function?**
   The greatest risk is **Premature Exploitation**. It is easy to mistake a high-performing local peak for the absolute global maximum, highlighting the need to maintain an active exploration budget throughout the project life cycle.
