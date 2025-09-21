## Process
You have flux data 
(in `/data/US-ARc_sample_input/01_qc_visual/qcv_files/`) 
then you need to gapfill first using ERA data (you made it and in `/data/US-ARc_sample_input/era5_csv/`)  before you can run the whole pipeline. 
The full process:
- Run oneflux first to generate 02_qc_auto files, which are necessary for downscaling of ERA data. 
  `python runoneflux.py all "/data" US-ARc "US-ARc_sample_input" 2005 2006 -l fluxnet_pipeline_US-ARc.log --mcr /usr/local/matlab/v94/ --recint hh --era-fy 2000 --era-ly 2006`
- The pipeline will stop cause there are no 06_meteo_era yet, but the 02_qc_auto will appear.
- Run downscaling, the 06_meteo_era files will be generated.
  ` python -m oneflux.downscaling.rundownscaling /data/US-ARc_sample_input/era5_csv /data US-ARc_sample_input`
  Note, there are at least 3 folders to be given, they are (1) the era5 timeseries, (2) the data folder containing all sites folders, and (3) the site folder, where all pipeline outputs will be within. 
- Run oneflux pipeling again. 
  `python runoneflux.py all "/data" US-ARc "US-ARc_sample_input" 2005 2006 -l fluxnet_pipeline_US-ARc.log --mcr /usr/local/matlab/v94/ --recint hh --era-fy 2000 --era-ly 2006`


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwNTQ4ODU3NywtMTg5NjMzMjM2MF19
-->