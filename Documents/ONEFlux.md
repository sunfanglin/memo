## Process
- You have flux data and are going to gapfill using ERA data, you need to run oneflux first to generate 02_qc_auto files, which are necessary for downscalling of ERA data. 
  `python runoneflux.py all "../datadir/" US-ARc "US-ARc_sample_input" 2005 2006 -l fluxnet_pipeline_US-ARc.log --mcr /usr/local/matlab/v94/ --recint hh --era-fy 2000 --era-ly 2006`
- The pipeline will stop cause there are no ERA data yet, but the 02_qc_auto will appear.
- Run downscaling to get 06_meteo_era files.
  
- Run oneflux pipeling again. 


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk0NzUxMTU0NywtMTg5NjMzMjM2MF19
-->