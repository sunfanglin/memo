## Process
You have flux data (in `01_qc_visual/qcv_files/`) and are going to gapfill using ERA data (you made it and in `/data/US-ARc_sample_input/era5_csv/`), you need to :
- Run oneflux first to generate 02_qc_auto files, which are necessary for downscalling of ERA data. 
  `python runoneflux.py all "../datadir/" US-ARc "US-ARc_sample_input" 2005 2006 -l fluxnet_pipeline_US-ARc.log --mcr /usr/local/matlab/v94/ --recint hh --era-fy 2000 --era-ly 2006`
- The pipeline will stop cause there are no ERA data yet, but the 02_qc_auto will appear.
- Run downscaling, the 06_meteo_era files will be generated.
  ` python -m oneflux.downscaling.rundownscaling /data/US-ARc_sample_input/era5_csv /data US-ARc_sample_input`
  Note, there are at least 3 folders to be given, they are (1) the era5 timeseries, (2) the data folder containing all sites folders, and (3) the site folder, where all pipeline outputs will be within. 
- Run oneflux pipeling again. 
  `python runoneflux.py all "../datad/" US-ARc "US-ARc_sample_input" 2005 2006 -l fluxnet_pipeline_US-ARc.log --mcr /usr/local/matlab/v94/ --recint hh --era-fy 2000 --era-ly 2006`


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTMxOTQxMDA5LC0xODk2MzMyMzYwXX0=
-->