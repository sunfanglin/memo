## Highest-priority improvements

### 1. Fix equation formatting and method clarity

The Methods still contain badly rendered equations.

Examples:

-   Bulk Richardson number equation appears merged:  `Rib=(gθ0)θz-θ0zuz2+vz2`
-   Variable text has errors:  `heighz`,  `uzand vz`
-   SNR normalization and Haar wavelet equations are still hard to read.

Advice:

-   Use Word equation editor or LaTeX-style equations.
-   For Rib, consider using the standard form with wind differences:  `Rib(z) = g z [theta_v(z)-theta_v(0)] / {theta_v(0)[(u(z)-u0)^2+(v(z)-v0)^2]}`
-   Define whether you use potential temperature or virtual potential temperature.
-   Explain clearly how stable PBLH is selected.

This is very important because Reviewer #2 specifically criticized formula inconsistencies.

### 2. Be careful with validation claims

The new validation metrics are good: R² = 0.895, RMSE = 41 m, MAE = 27 m, bias = -7 m. But the error values are very small compared with 30 m lidar resolution and radiosonde uncertainty.

Advice:

-   State clearly that this is an internal validation using only 16 daytime monsoon-season radiosonde comparisons.
-   Avoid saying the scale test “demonstrates robustness” too strongly.
-   Say “supports the choice of a = 300 m for the available validation cases.”
-   Add  `N = 16`  directly in Fig. 4 and the manuscript text.
-   In the response to Reviewer #1, avoid saying the radiosonde PBLH was retained after comparison with lidar SNR. That sounds circular because lidar is being validated against radiosonde.

### 3. Correct time-of-day language

The manuscript now uses UTC in figures, but some wording still describes local time incorrectly.

Examples:

-   Abstract says “late-morning maximum,” but 08:00 UTC is 16:00 CST, i.e. afternoon local time.
-   Plain Language Summary says afternoon, which is better.
-   Clear case reaches 07:10 UTC = 15:10 CST.

Advice:

-   Use wording such as “afternoon maximum in local time” or “around 07:00–09:00 UTC / 15:00–17:00 CST.”
-   Be consistent throughout Abstract, Results, captions, and Conclusions.

### 4. Fix geographical inconsistency

The title and site description say “northern Mount Qomolangma region,” but several places say “southern TP.”

Advice:

-   Use one consistent phrase, e.g.:
    -   “northern Mount Qomolangma region”
    -   or “southern Tibetan Plateau / northern Mount Qomolangma region”
-   Avoid switching casually between “southern TP” and “northern Mount Qomolangma.”

### 5. Check water-vapour pressure units

The manuscript says summer water-vapour pressure is  `0.75–0.85 hPa`  and winter is below  `0.15 hPa`. These values look too low; they may actually be in kPa.

Advice:

-   Verify the unit.
-   If values are kPa, write  `0.75–0.85 kPa`.
-   If values are hPa, recheck the calculation.

This is a potentially serious physical-unit issue.

## Response letter improvements

### 1. Fix “Minor comments” label for Reviewer #2

In the response letter, Reviewer #2’s major comments are introduced as “Minor comments.” This should be changed to “Major comments.”

### 2. Fix response-figure numbering

There is inconsistent figure numbering:

-   Seasonal mechanism response says “Figure R4” in the caption but later calls it “Figure R6.”
-   Later, “Figure R6” is also used for validation density plots.

Advice:

-   Renumber all response figures/tables sequentially.
-   Make sure the same figure number is used in caption, text, and response.

### 3. Reduce typos and polish language

Examples from the response letter:

-   `choic`  →  `choice`
-   `heigh AGL`  →  `height AGL`
-   `day-to-day.Following`  → add space
-   `The lidar ’ s`  → remove extra spaces
-   “Wind Profiler Radar” vs “coherent Doppler wind lidar” should be consistent unless quoting reviewer text.

### 4. Add manuscript line references

The response letter often says “we revised the manuscript” but does not give exact locations.

Advice:

-   Add line/page references after each major response:
    -   “Revised in Section 3.2, Lines xxx–xxx”
    -   “Added Fig. S2 and Table S1”
    -   “Revised Conclusions, Lines xxx–xxx”

This makes the response more convincing and easier for reviewers to verify.

## Manuscript polish issues

Fix these before submission:

-   Affiliation line says “Special Atmospheric Processes” but main text says “Spatial Atmospheric Processes.” Use the official name consistently.
-   Table 1:
    -   `Radial Rang Resolution`  →  `Radial Range Resolution`
    -   `6000m`  →  `6000 m`
    -   `1.5µm`  →  `1.5 µm`
    -   `0–360`  →  `0–360°`
    -   Verify whether the lidar really provides temperature, humidity, and pressure.
-   Introduction still repeats: “Radiosonde observations have consistently revealed an exceptionally deep PBL over the TP.”
-   Line with “lucidate” should be “elucidate.”
-   “captures captures” appears in the mean diurnal section.
-   “lidar algorithm product” should probably be “hybrid retrieval.”
-   Data availability statement repeats the Zenodo sentence and partly conflicts with restricted station-data access. Clarify what is public and what is restricted.

## Overall advice

The revised science is much improved and likely addresses the reviewers’ main concerns. The biggest remaining risks are not the overall story, but preventable details: equation formatting, time/units consistency, response-letter numbering, and over-strong validation wording. I would fix those carefully before resubmission.


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA4Njk3ODQ2Ml19
-->