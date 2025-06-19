## convert MODIS hdf files to netcdf4
- Only NASA [`modisconverter`](https://github.com/nasa/modisconverter/tree/main) works without errors.  
`podman run -it --security-opt label=disable -v ~/data/sat/modis:/data modisconverter:ubuntu-full-gdal-3.6.3`

verter:ubuntu-full-gdal-3.6.3

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjc3NzI2MzA2XX0=
-->