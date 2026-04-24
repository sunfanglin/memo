1.  Confirm the six edited files are present

-   `WRFV4.5.2/phys/module_sf_pv_desert.F`
-   `WRFV4.5.2/phys/noahmp/drivers/wrf/module_sf_noahmpdrv.F`
-   `WRFV4.5.2/phys/module_surface_driver.F`
-   `WRFV4.5.2/dyn_em/module_first_rk_step_part1.F`
-   `WRFV4.5.2/phys/Makefile`
-   `WRFV4.5.2/Registry/Registry.EM_COMMON`

2.  Clean old build artifacts

-   From  `WRFV4.5.2/`: run  `./clean -a`
-   This is important because  `Registry.EM_COMMON`  changed.

3.  (Re)run configure

-   Run  `./configure`  in  `WRFV4.5.2/`
-   Choose the same compiler/MPI option you normally use for this machine.

4.  Run a full Registry/code generation path

-   For WRF, modifying  `Registry.EM_COMMON`  requires regeneration during compile.
-   Do not skip to incremental  `make`  in  `phys/`; use top-level compile.

5.  Set namelist defaults intentionally (before run, not before compile)  Add to  `run/namelist.input`  under  `&physics`:

-   `pv_desert_opt = 1`
-   `pv_desert_frac = 0.60`
-   `pv_desert_tilt = 25.0`
-   `pv_desert_eff = 0.20`
-   `pv_desert_clear = 1.5`

6.  Know current trigger condition

-   In current code, PV is applied only where  `IVGTYP == 16`  (MODIS barren).
-   If your domain is not MODIS or has different barren index, you should adjust this before production runs.

7.  Optional but recommended quick static sanity checks

-   Verify no duplicate PV rconfig lines in  `Registry.EM_COMMON`.
-   Verify  `module_sf_pv_desert.o`  is in  `phys/Makefile`  and `module_sf_noahmpdrv.o: module_sf_pv


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTYwOTU1Njk0XX0=
-->