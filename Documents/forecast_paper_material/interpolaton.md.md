`xESMF` is the most powerful tool for regridding in Python because it is
built on the Earth System Modeling Framework (ESMF). Unlike simple linear
interpolation, `xESMF` can perform **Conservative Regridding**, which is
highly recommended for precipitation because it preserves the total amount
of water (mass) when moving from a fine grid to a coarse grid.

**Warning on Installation:** `xESMF` cannot be installed via `pip` reliably
because it depends on the ESMF C-library. You **must** use `conda`.

### Phase 1: Installation
Run this inside your `fss` environment:
```bash
conda install -c conda-forge xesmf
```

---

### Phase 2: The xESMF Interpolation Workflow

To interpolate HRES and MSWEP to the ERA5 grid, follow these steps:

#### 1. Define the Target Grid
The "Target" is the grid you want everything to end up on (in your case,
ERA5). `xESMF` needs the coordinates of the target grid to create a "Weight
Map."

#### 2. Create the Regridder (The Weight Map)
Instead of calculating the interpolation for every single pixel every time,
`xESMF` creates a **regridder object**. This object calculates the weights
once and stores them. You can then apply these weights to any number of
time steps.

#### 3. Execute the Regridding
Apply the weights to your source data (MSWEP or HRES).

---

### Phase 3: Full Implementation Script

Here is the complete script to align all three datasets to the ERA5 grid
using `xESMF`.

```python
import xarray as xr
import xesmf as xe
import numpy as np

def regrid_to_era5(src_path, tgt_path, var_name, output_name):
    """
    Interpolates source dataset to target (ERA5) dataset using xESMF.
    """
    print(f"Processing {src_path}...")

    # 1. Load datasets
    ds_src = xr.open_dataset(src_path)
    ds_tgt = xr.open_dataset(tgt_path)

    # Ensure coordinate names are exactly 'lat' and 'lon'
    # xESMF is strict about these names
    ds_src = ds_src.rename({'latitude': 'lat', 'longitude': 'lon'}) if
'latitude' in ds_src.coords else ds_src
    ds_tgt = ds_tgt.rename({'latitude': 'lat', 'longitude': 'lon'}) if
'latitude' in ds_tgt.coords else ds_tgt

    # 2. Create the Regridder
    # 'bilinear' is fast and smooth.
    # 'conservative' is best for precipitation but requires grid cell
boundaries.
    regridder = xe.Regridder(ds_src, ds_tgt, method='bilinear')

    # 3. Apply the regridding to the variable
    # This applies the weights to the data
    ds_regridded = regridder(ds_src[var_name])

    # 4. Save to NetCDF
    ds_regridded.to_netcdf(output_name)
    print(f"Saved aligned data to {output_name}")

# --- Main Execution ---

# Paths to your raw files
era5_file = 'era5_raw.nc'
hres_file = 'hres_raw.nc'
mswep_file = 'mswep_raw.nc'

# We regrid HRES and MSWEP, using ERA5 as the target for both
regrid_to_era5(hres_file, era5_file, 'tp', 'aligned_hres.nc')
regrid_to_era5(mswep_file, era5_file, 'tp', 'aligned_mswep.nc')

# Note: ERA5 is already the target, so we just save it as 'aligned' for
consistency
ds_era5 = xr.open_dataset(era5_file)
# Convert ERA5 meters to mm if necessary
if 'tp' in ds_era5.variables:
    ds_era5['tp'] = ds_era5['tp'] * 1000
ds_era5.to_netcdf('aligned_era5.nc')

print("All datasets aligned to ERA5 resolution.")
```

---

### Phase 4: Advanced Technical Details

#### Bilinear vs. Conservative Regridding
In the script above, I used `method='bilinear'`. Here is the difference:

*   **Bilinear (`'bilinear'`)**: Takes a weighted average of the 4 nearest
pixels. It is the standard for temperature or pressure. For precipitation,
it can "smooth out" extreme peaks.
*   **Conservative (`'conservative'`)**: This is the "gold standard" for
precipitation. It ensures that the total sum of precipitation in the source
area equals the total sum in the target area.
    *   **The Catch:** To use `'conservative'`, `xESMF` needs the
**corners** of the grid cells (the boundaries), not just the center points.
If your `.nc` files only have `lat` and `lon` center points, `xESMF` will
try to estimate the boundaries, but it is more complex to set up.

#### Handling Longitude (0-360 vs -180 to 180)
If your MSWEP data is $-180 \to 180$ and ERA5 is $0 \to 360$, the regridder
will produce an empty file (all NaNs).

**The Fix:**
Add this before creating the regridder:
```python
# Convert longitude from 0..360 to -180..180
ds_src = ds_src.assign_coords(lon=(((ds_src.lon + 180) % 360) -
180)).sortby('lon')
ds_tgt = ds_tgt.assign_coords(lon=(((ds_tgt.lon + 180) % 360) -
180)).sortby('lon')
```

#### Memory Efficiency for Large Files
If your files are huge, `xESMF` might crash your RAM. To solve this:
1.  Use `chunks` in `xr.open_dataset(path, chunks={'time': 10})`.
2.  `xESMF` works natively with **Dask**, meaning it will process the data
in pieces rather than all at once.

### Summary of the pipeline now:
1.  **Align Data:** $\text{HRES} \xrightarrow{xESMF} \text{ERA5 grid}$ and
$\text{MSWEP} \xrightarrow{xESMF} \text{ERA5 grid}$.
2.  **FSS Analysis:** Compare $(\text{ERA5 vs MSWEP})$ and $(\text{HRES vs
MSWEP})$ on that common grid.
3.  **Taylor Diagram:** Compare the statistical variance and correlation of
the three aligned products.


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MDUwMjMwNjJdfQ==
-->