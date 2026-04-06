
The short answer is: **Neither is "better" because they measure
fundamentally different things.**

If you only use one, you are missing half the story. In meteorology,
especially for precipitation, the standard practice is to use **both**
because they address different types of errors.

Here is the detailed breakdown of why you need both and what each one tells
you.

---

### 1. Fractions Skill Score (FSS)
**Focus: Spatial Placement and Scale**

FSS is designed to solve the **"Double Penalty" problem**. In
precipitation, if a model predicts a heavy rain cell 5km to the left of
where it actually happened, a standard point-by-point correlation will
penalize the model twice: once for missing the rain at the observation
point, and once for predicting rain where there was none.

*   **What it tells you:** "At what spatial scale does my model become
useful?"
*   **Best for:** Binary patterns (Rain vs. No-Rain).
*   **Key Insight:** It tells you if your model is getting the *location*
and *size* of the rain events right, even if the exact pixel is slightly
off.
*   **Weakness:** It doesn't tell you if the *amount* of rain (intensity)
is correct. It only cares if the rain is "there."

### 2. Taylor Diagram
**Focus: Statistical Amplitude and Phase**

A Taylor Diagram summarizes three statistics into one plot:
**Correlation**, **Root Mean Square Error (RMSE)**, and **Standard
Deviation**.

*   **What it tells you:** "How well does the model mimic the overall
statistical behavior of the observations?"
*   **Best for:** Continuous values (mm/day).
*   **Key Insight:**
    *   **Correlation:** Does the model follow the same "ups and downs" as
the observations?
    *   **Std Dev:** Does the model overestimate or underestimate the
intensity (variance) of the rain? (e.g., does it predict too many drizzle
events and not enough extremes?)
    *   **RMSE:** The overall distance between the model and observations.
*   **Weakness:** It is a "point-to-point" metric. It suffers from the
Double Penalty. A model could have a terrible Taylor Diagram but actually
be a very useful forecast if the rain cells are just slightly shifted.

---

### Comparison Table: FSS vs. Taylor Diagram

| Feature | FSS | Taylor Diagram |
| :--- | :--- | :--- |
| **Primary Goal** | Spatial Skill / Scale | Statistical Similarity |
| **Data Type** | Binary (Thresholded) | Continuous (Values) |
| **Handles "Shift"** | Yes (via windowing) | No (penalizes shifts heavily)
|
| **Measures Intensity** | No | Yes (via Standard Deviation) |
| **Main Question** | "Is the rain in the right neighborhood?" | "Are the
values and variance correct?" |
| **Result Format** | Curve (FSS vs. Scale) | 2D Polar Plot |

---

### Which one should you use for ERA5, HRES, and MSWEP?

Because you are comparing different resolutions, you **absolutely need
both**.

**Scenario A: Only using Taylor Diagrams**
You might find that HRES has a higher RMSE than ERA5. You might conclude
that ERA5 is "better." However, this might be because HRES is predicting
sharp, intense cells that are slightly shifted, while ERA5 is "smoothing"
everything out. The smoothing makes ERA5 *look* better statistically, even
though HRES is more physically realistic.

**Scenario B: Only using FSS**
You might find that HRES has a much higher FSS at small scales than ERA5.
You conclude HRES is better. However, you wouldn't know if HRES is
consistently overestimating the amount of rain by 50%—FSS doesn't see that.

### The "Gold Standard" Evaluation Workflow
If you are writing a paper or a technical report, the most robust approach
for precipitation is:

1.  **Taylor Diagram:** To show the overall statistical fit and variance
(amplitude) of the three products.
2.  **FSS Curves:** To show the spatial skill and prove that HRES provides
value at finer scales than ERA5.
3.  **Bias/Mean Error:** A simple plot showing if the models systematically
over- or under-predict total rainfall.
4.  **PDF (Probability Density Function):** To see if the models capture
the "tails" (the extreme heavy rain events) or if they just predict average
rain.

**Final Recommendation:** Use the **Taylor Diagram** to evaluate the
**intensity and correlation**, and use **FSS** to evaluate the **spatial
accuracy and resolution benefit**.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEzNjExNDQ0NV19
-->