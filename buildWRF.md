# Building the WRF Model on a Linux Machine

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Downloading WRF](#downloading-wrf)
4. [Setting Up the Environment](#setting-up-the-environment)
5. [Selecting and Installing a Compiler](#selecting-and-installing-a-compiler)
6. [Installing Required Libraries](#installing-required-libraries)
7. [Building WRF](#building-wrf)
8. [Conclusion](#conclusion)
9. [Further Reading](#further-reading)

## Introduction
The Weather Research and Forecasting (WRF) model is a widely used tool for atmospheric research and weather forecasting. Building WRF on a Linux machine requires a series of steps, including setting up the environment and installing necessary libraries.

## Prerequisites
Before you start, ensure you have the following:
- A Linux operating system (e.g., Ubuntu, CentOS).
- Access to a terminal with sufficient permissions (root or sudo).
- Basic knowledge of terminal commands.

## Downloading WRF
1. Go to the [WRF model website].
2. Download the latest version of the WRF source code using `wget` or by manually downloading it to your machine. For example:
   ```bash
   wget https://github.com/wrf-model/WRF/releases/download/v4.6.1/v4.6.1.tar.gz 
   wget https://github.com/wrf-model/WPS/archive/refs/tags/v4.6.0.tar.gz
  ```

## Selecting and Installing a Compiler
WRF can be compiled using various compilers. The most common ones are:
1. GCC (GNU Compiler Collection)
GCC is the default compiler for many Linux distributions and is widely used for building WRF.  
2. Intel Fortran Compiler
The Intel Fortran Compiler can provide better optimization for numerical computations, which is beneficial for WRF. 
3. PGI Compiler
The PGI (NVIDIA HPC SDK) compiler is another option, particularly for high-performance computing environments. 

After installing the desired compiler, verify the installation by checking the version:
``` bash
gfortran --version  # For GCC
ifort --version  # For Intel Fortran
```
## Installing Required Libraries

### Create a building folder
From a terminal window, create the following new directory:
``` bash
mkdir wrf_dependencies
```
### Set environment for building WRF dependencies
Path:
``` bash
DIR=$PWD/wrf_dependencies
```
Compiler:
``` bash
export CC=gcc
export CXX=g++
export FC=gfortran
export FCFLAGS="-m64 -fallow-argument-mismatch"
export F77=gfortran
export FFLAGS="-m64 -fallow-argument-mismatch"
export CPPFLAGS="-fcommon"
```
### Install mpich
``` bash
wget https://www2.mmm.ucar.edu/wrf/OnLineTutorial/compile_tutorial/tar_files/mpich-3.0.4.tar.gz
tar -xf mpich-3.0.4.tar.gz
cd mpich-3.0.4
./configure --prefix=$DIR/mpich
make -j 4 2>&1
make install
cd ..
rm -rf mpich*
```
### Install zlib
``` bash
wget https://www2.mmm.ucar.edu/wrf/OnLineTutorial/compile_tutorial/tar_files/zlib-1.2.11.tar.gz
tar xzvf zlib-1.2.11.tar.gz
cd zlib-1.2.11
./configure --prefix=$DIR/grib2
make -j 4
make install
cd ..
rm -rf zlib*
```
### Install hdf5
``` bash
wget https://github.com/HDFGroup/hdf5/archive/refs/tags/hdf5_1.14.5.tar.gz
tar xzvf hdf5-1.15.5.tar.gz
cd hdf5-hdf5_1.14.5
./configure --prefix=$DIR/netcdf --with-zlib=$DIR/grib2 --enable-fortran --enable-shared
make -j 4
make install
cd ..
rm -rf hdf5*
```
### Install NetCDF-c
``` bash
wget https://github.com/Unidata/netcdf-c/archive/v4.7.2.tar.gz
tar xzvf v4.7.2.tar.gz
cd netcdf-c-4.7.2
./configure --prefix=$DIR/netcdf --disable-dap --enable-netcdf-4 --enable-hdf5 --enable-shared
make -j 4
make install
cd ..
rm -rf v4.7.2.tar.gz netcdf-c*
```
### Install netcdf-fortran
``` bash
wget https://github.com/Unidata/netcdf-fortran/archive/v4.5.2.tar.gz
tar xzvf v4.5.2.tar.gz
cd netcdf-fortran-4.5.2
./configure --prefix=$DIR/netcdf --disable-hdf5 --enable-shared
make -j 4
make install
cd ..
rm -rf netcdf-fortran* v4.5.2.tar.gz
```
### Install libpng
``` bash
wget https://www2.mmm.ucar.edu/wrf/OnLineTutorial/compile_tutorial/tar_files/libpng-1.2.50.tar.gz
tar xzvf libpng-1.2.50.tar.gz
cd libpng-1.2.50
./configure --prefix=$DIR/grib2
make -j 4
make install
cd ..
rm -rf libpng*
```
### Install jasper
``` bash
wget https://www2.mmm.ucar.edu/wrf/OnLineTutorial/compile_tutorial/tar_files/jasper-1.900.1.tar.gz
tar xzvf jasper-1.900.1.tar.gz
cd jasper-1.900.1
./configure --prefix=$DIR/grib2
make
make install
cd ..
rm -rf jasper* ._jasper-1.900.1
``` 
## Building WRF
### Set environment for buiding `WRF&WPS`
Now close the current terminal window, and open a new one. Environment variables set earlier will no longer be set. In the new terminal window, open up the `.bashrc` (or similar) file
``` bash
vi ~/.bashrc
```
 and edit the following entries. When done, save the file.
 
``` bash
export NETCDF=$DIR/netcdf
export LD_LIBRARY_PATH=$NETCDF/lib:$DIR/grib2/lib
export PATH=$NETCDF/bin:$DIR/mpich/bin:${PATH}
export JASPERLIB=$DIR/grib2/lib
export JASPERINC=$DIR/grib2/include
```
Source the `.bashrc` (or similar) file so the above commands go into effect for the current terminal window
``` bash
source ~/.bashrc
```
### Build WRF
``` bash
git clone --recurse-submodule https://github.com/wrf-model/WRF.git
cd WRF
./configure (choose options 34 and 1)
./compile em_real -j 4 >& log.compile
```
### Build WPS
``` bash
git clone https://github.com/wrf-model/WPS.git
cd WPS
export WRF_DIR=path-to-WRF-top-level-directory/WRF
./configure (choose option 1)
./compile >& log.compile
```
## Conclusion
Building the WRF model on a Linux machine involves several steps, including selecting a compiler, setting up the environment, installing necessary libraries, and configuring the model. With these steps, you should be able to successfully build and run the WRF model for your research or forecasting needs.

## Further Reading
[WRF User's Guide](https://www2.mmm.ucar.edu/wrf/users/wrf_users_guide/build/html/index.html)
[WRF Model GitHub Repository](https://github.com/wrf-model/WRF)
[Full WRF and WPS Installation Example (GNU)](https://forum.mmm.ucar.edu/threads/full-wrf-and-wps-installation-example-gnu.12385/)
[NetCDF Documentation](https://docs.unidata.ucar.edu/netcdf-c/current/)


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA2NzI2ODM5NCwxMTQ0MjIzOTcyLC0xNz
MzMDk2NTEyXX0=
-->