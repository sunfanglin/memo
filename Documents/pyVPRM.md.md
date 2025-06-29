## convert MODIS hdf files to netcdf4
- Only NASA [`modisconverter`](https://github.com/nasa/modisconverter/tree/main) works without errors.  It's suggested to install the module on a [official container](https://hub.docker.com/r/osgeo/gdal/tags) with gdal-3.6.3 preinstalled. The full Ubuntu one works. But the official docker.com may be blocked in China, so need to use a mirror site.
- The following command run a saved container with a worked `modisconcerter` installed.
`podman run -it --security-opt label=disable -v ~/data/sat/modis:/data modisconverter:ubuntu-full-gdal-3.6.3`

verter:ubuntu-full-gdal-3.6.3



## light-use efficiency ($\epsilon$)

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEwMjY3NTE2MSwtMTA2NzIxNjQ2OV19
-->