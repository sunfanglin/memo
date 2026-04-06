Fractions Skill Score (FSS) analysis.
`scores` tool (likely referring to the `scores` Python library often used
in meteorology/atmospheric science).
Linux machine.
Conda environment named `fss`.

    *   The `scores` library is typically used for evaluating spatial
forecasts (like precipitation).
    *   It's usually installed via `pip` or `conda-forge`.
    *   It requires data in specific formats (usually NumPy arrays or
Xarray datasets).

    *   **Phase 1: Environment Setup.** Creating the conda env and
installing dependencies.
    *   **Phase 2: Data Preparation.** Getting the observation and forecast
data ready.
    *   **Phase 3: Implementation (The Python Script).** Writing the code
to call the FSS function.
    *   **Phase 4: Execution.** Running the script and interpreting
results.

    *   *Step 1: Environment*
        *   `conda create -n fss python=3.9` (Choosing a stable version).
        *   `conda activate fss`.
        *   `pip install scores` (Check if it's on PyPI) or `conda install
-c conda-forge scores`. Actually, for most meteorology tools, `pip install
scores` is common, but I should check the specific package.
*Self-correction: The "scores" package for FSS is often associated with the
one by the community or specific weather repositories. I'll provide the
installation for the most common Python implementation.*

    *   *Step 2: Dependencies*
        *   FSS usually needs `numpy`, `xarray`, `matplotlib` for
visualization.

    *   *Step 3: The Code (Crucial part)*
        *   Need two inputs: `obs` (observation) and `fcst` (forecast).
        *   Need a threshold (e.g., 1mm/h for rain).
        *   Need the window size (the "fraction" part of FSS).
        *   *Logic:*
            1. Load data.
            2. Binarize data based on threshold.
            3. Call the FSS function.
            4. Plot the results (FSS vs. Window Size).

    *   *Step 4: Linux Specifics*
        *   Mentioning `chmod +x` if they make a script, or just running
`python script.py`.

    *   *Introduction:* Briefly explain what FSS is (spatial verification).
    *   *Section 1: Environment Setup.* Clear commands.
    *   *Section 2: Data format requirements.* Explain that data should be
2D grids.
    *   *Section 3: The Python Script.* Provide a complete, runnable
example.
    *   *Section 4: Execution steps.*
    *   *Section 5: Interpretation.* What does a score of 1.0 or 0.0 mean?
...done thinking.

To perform a **Fractions Skill Score (FSS)** analysis using the `scores`
library (commonly used in meteorology and atmospheric sciences) on a Linux
machine within a specific conda environment, follow these steps.

### Phase 1: Environment Setup
First, we will create the isolated environment to avoid dependency
conflicts with your system Python.

1.  **Open your terminal.**
2.  **Create the conda environment:**
    ```bash
    conda create -n fss python=3.9 -y
    ```
3.  **Activate the environment:**
    ```bash
    conda activate fss
    ```
4.  **Install the necessary libraries:**
    The `scores` package, along with `numpy` (for arrays), `xarray` (for
netCDF/GRIB data), and `matplotlib` (for plotting the FSS curve), are
required.
    ```bash
    pip install scores numpy xarray matplotlib netcdf4
    ```

---

### Phase 2: Data Preparation
FSS compares a **forecast grid** against an **observation grid**. For the
`scores` tool to work, you need:
*   Two 2D arrays (forecast and observation) of the same spatial
resolution.
*   A **threshold** value (e.g., if you are analyzing rain, you
might use $0.1 \text{ mm/h}$ to define "rain vs. no rain").

---

### Phase 3: Implementation (The Python Script)
Create a python file named `run_fss.py`. You can use `nano run_fss.py` or
`vim run_fss.py`.

Copy and paste the following template. This script assumes you have your
data in `.nc` (NetCDF) format, but you can replace the loading section with
your own arrays.

```python
import numpy as np
import xarray as xr
import matplotlib.pyplot as plt
from scores import fss

# 1. Load your data
# Replace 'obs.nc' and 'fcst.nc' with your actual filenames
ds_obs = xr.open_dataset('obs.nc')
ds_fcst = xr.open_dataset('fcst.nc')

# Extract the specific variable as numpy arrays
# Ensure they are the same shape!
obs = ds_obs['precipitation'].values
fcst = ds_fcst['precipitation'].values

# 2. Define the threshold for the binary mask
# FSS is calculated on binary data (1 if >= threshold, 0 otherwise)
threshold = 0.1

# 3. Define the window sizes to test (the "fraction" part of FSS)
# This tests the skill at different spatial scales (e.g., 1km, 2km, 5km...)
# If your grid spacing is 1km, window=5 means a 5x5km area.
windows = np.arange(1, 21)

fss_values = []

# 4. Calculate FSS for each window size
for w in windows:
    # The fss function typically takes: (forecast, observation, threshold,
window)
    score = fss(fcst, obs, threshold, w)
    fss_values.append(score)

# 5. Plotting the results
plt.figure(figsize=(8, 5))
plt.plot(windows, fss_values, marker='o', color='b')
plt.axhline(0, color='black', lw=1)
plt.xlabel('Window Size (grid cells)')
plt.ylabel('FSS')
plt.title(f'Fractions Skill Score (Threshold: {threshold})')
plt.grid(True)
plt.savefig('fss_result.png')
plt.show()

print("Analysis complete. Plot saved as fss_result.png")
```

---

### Phase 4: Execution

1.  **Ensure your data files** (`obs.nc` and `fcst.nc`) are in the same
directory as the script.
2.  **Run the script:**
    ```bash
    python run_fss.py
    ```

---

### Phase 5: Interpreting the Results

When you look at the resulting plot, here is how to read the FSS:

*   **FSS = 1**: Perfect forecast. The forecast and observation are
identical at that spatial scale.
*   **FSS > 0**: The forecast is better than a random guess (it has
"skill").
*   **FSS $\le$ 0**: The forecast is no better than (or worse than) a
random placement of the forecast pattern over the domain.
*   **The Curve**: Usually, as the window size increases, the FSS value
increases. This tells you the **spatial scale** at which your model becomes
"skillful." If the FSS crosses $0$ at a window size of 5, your model is
skillful at scales of $5\times5$ grid cells or larger, but not smaller.

### Troubleshooting Common Issues

*   **Memory Error:** If your grids are massive (e.g., $10000 \times
10000$), `fss` can be computationally expensive. Try slicing your xarray
dataset first: `ds.isel(x=slice(0, 1000), y=slice(0, 1000))`.
*   **Dimension Mismatch:** If you get a `ValueError` regarding shapes,
check that your forecast and observation arrays are exactly the same size
using `print(obs.shape, fcst.shape)`.
*   **Conda environment not found:** Ensure you ran `conda activate fss`
before running the python command.


Prepare regional precipitation datasets for FSS analysis.
ERA5 (reanalysis), ECMWF HRES (forecast/high-res), MSWEP (benchmark/merged
precipitation).
Differing spatial resolutions.
Linux machine, Conda environment (`fss`), Python (implied from previous
turns).

    *   *ERA5:* Usually $\sim 0.25^\circ \times 0.25^\circ$.
    *   *ECMWF HRES:* Usually $\sim 0.1^\circ \times 0.1^\circ$ (varies by
version).
    *   *MSWEP:* $\sim 0.1^\circ \times 0.1^\circ$.
    *   *The Problem:* FSS requires arrays of identical dimensions. You
cannot compare a $100 \times 100$ grid to a $250 \times 250$ grid directly.

    *   *Approach A: Downscaling (Interpolation).* Upsample the coarse data
to the fine resolution.
    *   *Approach B: Upscaling (Aggregation).* Downsample the fine data to
the coarse resolution.
    *   *Industry Standard:* For FSS and precipitation, it is generally
better to interpolate the coarse data (ERA5) to the resolution of the
benchmark/fine data (MSWEP/HRES) to maintain the spatial context, *or* to
use a common grid. However, since MSWEP is the benchmark, interpolating
others to the MSWEP grid is a common choice.

    *   **Step 1: Domain Selection (Cropping).** All datasets must cover
the exact same geographic bounding box (Lat/Lon).
    *   **Step 2: Temporal Alignment.** Ensure the time steps match exactly
(e.g., hourly, daily).
    *   **Step 3: Regridding (The Core Step).** Convert different
resolutions to a "Common Target Grid."
    *   **Step 4: Unit Standardization.** Ensure all are in
$\text{mm/hour}$ or $\text{mm/day}$.
    *   **Step 5: Export/Save.** Save as aligned NetCDF files for the FSS
script to read.

    *   *Tooling:* `xarray` and `xesmf` are the gold standard for
regridding in Python. `rioxarray` is also useful. *Self-correction:*
`xesmf` can be tricky to install via conda (requires ESMF). I should
suggest a simpler `xarray.interp` method for beginners, but mention `xesmf`
for scientific rigor.

    *   *Detailed Workflow:*
        1.  Load data.
        2.  Cut to region (Lat/Lon).
        3.  Interpolate ERA5 and HRES to MSWEP grid.
        4.  Handle units (ERA5 often stores total precip as meters).

    *   *Highlight the "Benchmark" role:* MSWEP is the reference.
Everything maps *to* MSWEP.
...done thinking.

Since you are comparing **ERA5** (coarse), **ECMWF HRES** (fine), and
**MSWEP** (fine/benchmark), you face a "resolution mismatch" problem.

FSS is a spatial verification metric; it requires all input arrays to be on
the **exact same grid (same dimensions and same pixel coordinates)**. You
cannot run FSS on raw data if one is $0.25^\circ$ and another is
$0.1^\circ$.

Here is the professional workflow to prepare these datasets for FSS
analysis.

---

### 1. The Strategy: "Regridding to the Benchmark"
Since **MSWEP** is your benchmark, the standard approach is to
**interpolate (regrid)** the ERA5 and HRES data onto the MSWEP grid.

*   **MSWEP:** Keep as the Target Grid.
*   **ECMWF HRES:** Interpolate to MSWEP grid (usually very close, but
needs alignment).
*   **ERA5:** Upsample (interpolate) from $0.25^\circ \to 0.1^\circ$.

---

### 2. Tooling Requirements
You will need additional libraries in your `fss` conda environment to
handle spatial coordinates and regridding.

```bash
conda activate fss
pip install xarray numpy pandas netcdf4 dask
# For high-quality regridding, xESMF is recommended,
# but xarray's built-in .interp() is sufficient for basic bilinear
interpolation.
```

---

### 3. Step-by-Step Preparation Pipeline

#### Step A: Spatial Cropping (Domain Selection)
All three datasets must cover the exact same bounding box (e.g., a specific
country or region).
*   **Why?** FSS compares arrays. If one file is $100\times100$ pixels and
another is $110\times110$, the code will crash.

#### Step B: Temporal Alignment
Ensure all three datasets have the same time steps.
*   ERA5 and HRES might be hourly; MSWEP might be daily.
*   **Action:** Resample all to a common frequency (e.g., daily sum) using
`xarray.resample`.

#### Step C: Unit Standardization
Precipitation is often stored differently:
*   **ERA5:** Often stored as "Total Precipitation" in **meters**. (Convert
to mm: $m \times 1000$).
*   **MSWEP/HRES:** Usually in **mm**.
*   **Action:** Ensure all three are in $\text{mm/day}$ or
$\text{mm/hour}$.

#### Step D: Regridding (The most critical step)
Use bilinear interpolation to bring ERA5 and HRES onto the MSWEP grid.

---

### 4. Implementation Script (Preparation)

Create a script called `prepare_data.py`. This script transforms your raw
files into "FSS-ready" files.

```python
import xarray as xr
import numpy as np

def prepare_dataset(file_path, var_name, target_grid=None,
scale_factor=1.0):
    """
    Loads, crops, and regrids a dataset.
    """
    ds = xr.open_dataset(file_path)
    data = ds[var_name]

    # 1. Apply scale factor (e.g., m to mm for ERA5)
    data = data * scale_factor

    # 2. Spatial Crop (Example: Central Europe)
    # Adjust these coordinates to your specific region
    data = data.sel(lat=slice(40, 50), lon=slice(10, 20))

    # 3. Regrid to target_grid if provided
    if target_grid is not None:
        # Linear interpolation to the target's lat/lon coordinates
        data = data.interp(lat=target_grid.lat, lon=target_grid.lon,
method="linear")

    return data

# --- Main Execution ---

# 1. Load Benchmark (MSWEP) first to define the target grid
ds_mswep = prepare_dataset('mswep.nc', 'tp') # tp = total precip

# 2. Load and regrid ERA5 to match MSWEP
# ERA5 is often in meters, so scale_factor=1000
ds_era5 = prepare_dataset('era5.nc', 'tp', target_grid=ds_mswep,
scale_factor=1000)

# 3. Load and regrid HRES to match MSWEP
ds_hres = prepare_dataset('hres.nc', 'tp', target_grid=ds_mswep)

# Save the prepared files for the FSS script
ds_mswep.to_netcdf('prep_obs.nc')
ds_era5.to_netcdf('prep_era5.nc')
ds_hres.to_netcdf('prep_hres.nc')

print("Datasets successfully aligned and saved.")
```

---

### 5. Final FSS Analysis Workflow

Now that you have three aligned files (`prep_obs.nc`, `prep_era5.nc`,
`prep_hres.nc`), you can perform the FSS analysis in pairs:

1.  **Pair 1:** $\text{MSWEP (Obs)} \longleftrightarrow \text{ERA5
(Model)}$ $\rightarrow$ Result: **FSS_ERA5**
2.  **Pair 2:** $\text{MSWEP (Obs)} \longleftrightarrow \text{HRES
(Model)}$ $\rightarrow$ Result: **FSS_HRES**

**Comparing the two:**
*   If the **FSS_HRES** curve stays above the **FSS_ERA5** curve for small
window sizes, it proves that the higher resolution of HRES provides actual
physical skill and isn't just "noise."
*   If they overlap, the HRES resolution is not adding value over the
coarser ERA5.

### Summary Checklist for Data Prep
| Feature | ERA5 | HRES | MSWEP | Action |
| :--- | :--- | :--- | :--- | :--- |
| **Resolution** | $0.25^\circ$ | $0.1^\circ$ | $0.1^\circ$ | Interpolate
ERA5 $\to$ MSWEP |
| **Units** | meters | mm | mm | ERA5 $\times 1000$ |
| **Extent** | Global/Reg | Global/Reg | Global/Reg | Crop all to identical
Lat/Lon |
| **Time** | Hourly | Hourly | Daily | Resample all to common $\Delta t$ |

>>> Steps to interplote all data to the same as ERA5.
Thinking...
Interpolate all precipitation datasets (ERA5, ECMWF HRES, MSWEP) to the
*lowest* common denominator: the **ERA5 resolution** ($\sim 0.25^\circ$).

        1. ERA5 (Target Grid)
        2. ECMWF HRES (Source $\to$ Target)
        3. MSWEP (Source $\to$ Target)
Linux machine, Conda environment (`fss`), Python (`xarray`, `numpy`).

    *   *Downsampling (Fine $\to$ Coarse):* This is effectively "averaging"
or "aggregating" pixels. If you use simple linear interpolation to go from
$0.1^\circ$ to $0.25^\circ$, you are essentially sampling a few points and
ignoring others, which can lead to aliasing or loss of extreme rainfall
events.
    *   *The "Correct" Way:* For precipitation, the best way to downsample
is **Area-Weighted Averaging** (Conservation of mass). However, for
standard FSS analysis, bilinear interpolation (`.interp`) is common and
computationally simpler, provided the user understands it's a sample. I
should mention both but provide the `.interp` code for ease of use.

    *   **Step 1: Load the Target.** Load ERA5 first because its
coordinates define the grid for everyone else.
    *   **Step 2: Load the Sources.** Load HRES and MSWEP.
    *   **Step 3: Spatial Alignment (Cropping).** Ensure they all cover the
same region.
    *   **Step 4: Interpolation.** Map HRES and MSWEP $\to$ ERA5 grid.
    *   **Step 5: Unit Conversion.** Handle the meters $\to$ mm conversion
for ERA5.
    *   **Step 6: Save.** Export the aligned datasets.

    *   *Wait, if I'm interpolating to ERA5, I don't need to change ERA5's
grid, only its units.*
    *   *I need to be careful with coordinates. Some files use
$0-360^\circ$ longitude, others use $-180$ to $180^\circ$. I should mention
`assign_coords` or `roll` if necessary, but for simplicity, I'll assume
they are compatible or the user is aware.*

    *   *Introduction:* Explain that interpolating to the coarsest
resolution is "Downsampling."
    *   *Code:* Write a clear, modular Python script.
    *   *Specifics:*
        *   Use `xarray.interp` for the interpolation.
        *   Handle the units (ERA5 meters $\to$ mm).
        *   Explain the risk: "Loss of detail." (Crucial point: if you
interpolate HRES to ERA5, you are removing the very thing that makes HRES
"high resolution").
...done thinking.

If you choose to interpolate everything to the **ERA5 resolution**
($\approx 0.25^\circ$), you are performing **downsampling** (moving from a
fine grid to a coarse grid).

**Warning:** By doing this, you are intentionally removing the
high-resolution detail from MSWEP and HRES. The FSS analysis will then tell
you if the models are skillful at the "coarse scale," but you will lose the
ability to see if HRES is better than ERA5 at "fine scales."

Here are the steps to align all data to the ERA5 grid.

### 1. The Logic Flow
1.  **Load ERA5 first**: It acts as the "Master Template" for coordinates
(Latitude and Longitude).
2.  **Load MSWEP and HRES**: These are the datasets that need to be
changed.
3.  **Standardize Units**: Convert ERA5 from meters to mm.
4.  **Interpolate**: Use the coordinates from ERA5 to sample the values
from MSWEP and HRES.
5.  **Save**: Export three files that are now perfectly identical in shape.

---

### 2. Implementation Script

Save this as `align_to_era5.py`.

```python
import xarray as xr
import numpy as np

def align_to_era5(era5_path, hres_path, mswep_path,
output_prefix="aligned"):
    # 1. Load ERA5 (The Master Template)
    print("Loading ERA5...")
    ds_era5 = xr.open_dataset(era5_path)

    # Handle ERA5 units: Convert meters to mm (standard for ERA5
precipitation)
    # Check if the variable is 'tp' (total precipitation)
    if 'tp' in ds_era5.variables:
        ds_era5['tp'] = ds_era5['tp'] * 1000

    # Define the target grid coordinates
    target_lat = ds_era5.lat
    target_lon = ds_era5.lon

    # 2. Load and Interpolate HRES
    print("Interpolating HRES to ERA5 grid...")
    ds_hres = xr.open_dataset(hres_path)
    # Interpolate HRES onto the ERA5 lat/lon
    # We use .interp() which performs linear interpolation by default
    ds_hres_aligned = ds_hres.interp(lat=target_lat, lon=target_lon,
method="linear")

    # 3. Load and Interpolate MSWEP
    print("Interpolating MSWEP to ERA5 grid...")
    ds_mswep = xr.open_dataset(mswep_path)
    # Interpolate MSWEP onto the ERA5 lat/lon
    ds_mswep_aligned = ds_mswep.interp(lat=target_lat, lon=target_lon,
method="linear")

    # 4. Save the results
    # This ensures all three files have the exact same dimensions
    ds_era5.to_netcdf(f"{output_prefix}_era5.nc")
    ds_hres_aligned.to_netcdf(f"{output_prefix}_hres.nc")
    ds_mswep_aligned.to_netcdf(f"{output_prefix}_mswep.nc")

    print(f"Done! Files saved as {output_prefix}_era5.nc, etc.")
    print(f"Final Grid Shape: {ds_era5.dims}")

# --- Run the process ---
align_to_era5(
    era5_path='era5_raw.nc',
    hres_path='hres_raw.nc',
    mswep_path='mswep_raw.nc'
)
```

---

### 3. Important Technical Considerations

#### A. Linear Interpolation vs. Area Averaging
In the script above, `method="linear"` is used.
*   **Linear Interpolation** is fast and works well for general patterns.
*   **Area Averaging (Conservative Remapping)** is technically the
"correct" way for precipitation. Because precipitation is an *accumulated*
value, simply sampling a point (interpolation) can lead to errors. If you
find your total precipitation sums are changing too much, you should use
the `xESMF` library for **conservative regridding**.

#### B. Longitude Convention (0-360 vs -180 to 180)
ERA5 often uses $0 \to 360^\circ$ longitude, while MSWEP might use $-180
\to 180^\circ$. If your output files contain `NaN` values, it is because
the longitudes don't overlap.

**Fix:** Add this line to your script before interpolating if you see
`NaNs`:
```python
# Convert 0-360 to -180 to 180
ds_era5 = ds_era5.assign_coords(lon=(((ds_era5.lon + 180) % 360) -
180)).sortby('lon')
```

#### C. Memory Management
If these files are very large, `xarray` might crash your RAM. To fix this:
1.  Open the files using chunks: `xr.open_dataset(path, chunks={'lat': 100,
'lon': 100})`.
2.  This enables **Dask**, which processes the data in small pieces rather
than loading the whole global map into RAM.

### 4. Next Step: FSS Analysis
Now that you have `aligned_era5.nc`, `aligned_hres.nc`, and
`aligned_mswep.nc`, you can plug them into the FSS script from the previous
response:

*   **Test 1:** `fss(aligned_era5, aligned_mswep, threshold, window)`
*   **Test 2:** `fss(aligned_hres, aligned_mswep, threshold, window)`

Because they are now on the same grid, the `fss` function will run without
dimension errors.

>>> Send a message (/? for help)
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk1MDc2ODY0NSwtOTgwOTc3MDExXX0=
-->