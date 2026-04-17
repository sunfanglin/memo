## Process
### You have flux data 
(in `/data/US-ARc_sample_input/01_qc_visual/qcv_files/`) 
### ERA5 data
then you need to gapfill first using ERA data (you made it and in `/data/US-ARc_sample_input/era5_csv/`)  before you can run the whole pipeline. 

### Full process:
- Run oneflux first to generate **02_qc_auto** files, which are necessary for downscaling of ERA data. 
```bash
$ python runoneflux.py all "/data" US-ARc "US-ARc_sample_input" 2005 2006 -l fluxnet_pipeline_US-ARc.log --mcr /usr/local/matlab/v94/ --recint hh --era-fy 2000 --era-ly 2006
```
```bash
$ python runoneflux.py all "/" US-ARc "CN-GHe_input" 2024 2025 -l fluxnet_pipeline_CN-GHe.log --mcr /usr/local/matlab/v94/ --recint hh --era-fy 2015 --era-ly 2025
```

- The pipeline will stop cause there are no **06_meteo_era** files yet, but the **02_qc_auto will appear**.
- Run downscaling, the 06_meteo_era files will be generated.

 ```bash
 $ python -m oneflux.downscaling.rundownscaling /data/US-ARc_sample_input/era5_csv_files_path /data US-ARc_sample_input
  ```
```bash
$ python -m oneflux.downscaling.rundownscaling     /workspace/gonghe/CN-GHe_input/06_meteo_era/reanalysis_input     /workspace/gonghe     CN-GHe_input     --era-fy 2015 --era-ly 2025
```
  Note, there are at least 3 folders to be given, they are (1) the era5 timeseries, (2) the data folder containing all sites folders, and (3) the site folder, where all pipeline outputs will be within. 
- Run oneflux pipeling again.

  `python runoneflux.py all "/data" US-ARc "US-ARc_sample_input" 2005 2006 -l fluxnet_pipeline_US-ARc.log --mcr /usr/local/matlab/v94/ --recint hh --era-fy 2000 --era-ly 2006`


## Appendix
- Install MATLAB Compiler Runtime (MCR) 2018a (version 9.4) in the container:
  `wget https://ssd.mathworks.com/supportfiles/downloads/R2018a/deployment_files/R2018a/installers/glnxa64/MCR_R2018a_glnxa64_installer.zip`

  `unzip MCR_R2018a_glnxa64_installer.zip -d /tmp/mcr_install`

  `/tmp/mcr_install/install -mode silent -destinationFolder /usr/local/MATLAB/MATLAB_Runtime/v94 -agreeToLicense yes`

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzNDI4NDE3MCwtOTYzMjk2Nzk2LDEyNz
gwNzk1NDYsNjI5MzE0MjAxLC0xOTgwNTc0NDc2LC0yMTMzMzA0
MDE4LC0xODk2MzMyMzYwXX0=
-->