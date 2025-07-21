# 2025
## Week 27
### 06/30/2025
- [x] Download ERA5 data by year and merge. :white_check_mark:
- [x] Merge IMDAA data, split them by month, change variable names, fix time name if needed.  :white_check_mark:
- [x] NOTE: The t2m of IMDAA data are hourly while ssrd 3-hourly.

### 07/01/2025
- [x] Re-process IMDAA data since The t2m of IMDAA data are hourly while ssrd are 3-hourly. Ignoring this resulted in fault ssrd values in merged data.
- [ ] Merge ssrd data of IMDAA, and re-split them by year to avoid the first record of the year (2022-01-01 00:00 ) being stored in data file of last year (2021).
- [ ] Evaluate the performance of IMDAA data driving pyVPRM
- [ ]  Download GLDAS data, and evaluate with IMDAA and ERA5
- [ ] Compare T and radiation between ERA5 and IMDAA over Tibetan Plateau.q
- [ ] Sentinel image to derive NEE and GPP  

**The pyVPRM out driven by IMDAA data are wrong.** 
### 07/12/2025
- [x] Re-process MODIS tiles of 2024, and run pyVPRM, compare the out with 2022.  **The GPP sum of 2024 is nearly twice of 2022**
### 07/13/2025
- [x] Process MODIS tiles of 2023. **
- [x] Got many INF values, the cause is likely the usage of multi-cores, but reason is still unknown.** 
## Week 28
### 07/20/2025
- [x] The sat-download script does not work, due to empty folders of the source link. Changed to download directly from  [LPCLOUD of NASA EARTHDATA](https://search.earthdata.nasa.gov/search?q=C2343111356-LPCLOUD)
- [x] Make a github repo of scripts dealing with pyVPRM inputs and outputs. [My ](https://github.com/sunfanglin/pyVPRM_examples)
### 07/21/2025
- [ ] Make parallel folders of vprm-prediction based on landcover 2016 and 2019 
> 面对信仰，纵身一跃
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ0NjE4MjU1OSwxNTUzMjM2NDMxLC0xOD
g2MjQ5NzA1LDI4ODY4NzgzMCwtMTI5MTMxNDk2OCwxNzY1NDQw
MjA4LDEyMzEyMTgwMzQsLTE3MjczMjc5NzcsMTA3NTUxMjUyMi
w2Mjg1MzgyNDNdfQ==
-->