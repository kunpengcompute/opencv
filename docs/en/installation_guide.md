# Kunpeng OpenCV Deployment Guide

## Description

This document describes how to deploy the Kunpeng OpenCV environment.

## Environment Requirements

Hardware environment

| Item | Description   |
| ------------ | ------------ |
| CPU | New Kunpeng 920 model|

Software environment

| Software | Version   |
| ------------ | ------------ |
| OS | openEuler 22.03 LTS SP4 |
| Compiler| GCC 10.3.1 or later|
| make | 4.3 or later|
| cmake | 3.10 or later|

## Procedure
>
> >![](public_sys-resources/icon-notice.gif) **NOTICE**
>You are advised to enable system hyper-threading to obtain the optimal performance.
>
**Step 1** Download and decompress the OpenCV source code package based on the version mapping. Copy the OpenCV source code package [`opencv-4.10.0.zip`](https://github.com/opencv/opencv/archive/refs/tags/4.10.0.zip) to the `/home` directory and decompress it.

``` bash
unzip opencv-4.10.0.zip
```
`/home/opencv-4.10.0` is obtained after the decompression.

**Step 2** Download the files in this repository to the `/home` directory.

``` bash
git clone https://gitcode.com/boostkit/opencv.git
```

**Step 3** Install the dependencies.

``` bash
yum install -y binutils cmake git pkgconfig make patch gcc-10.3.1 gcc-c++-10.3.1 lapack ffmpeg ffmpeg-devel libjpeg-* python3-devel python3-numpy
```

**Step 4** Apply the optimization patch.

``` bash
cd /home/opencv-4.10.0
# Copy the patch.
cp /home/opencv/*.patch ./
# Apply the optimization patch.
for patch in $(ls -v *.patch); do patch -p1 < "$patch"; done
```

**Step 5** Compile and install OpenCV.

``` bash
mkdir build && cd build
# Run the `cmake` command. The default installation path is `/home/opencv_install`. You can change the path as needed.
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/home/opencv_install \
    -D CMAKE_CXX_FLAGS="-O3 -march=armv8-a" \
    -D CMAKE_C_FLAGS="-O3 -march=armv8-a" \
    -D BUILD_opencv_python3=ON\
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D WITH_OPENMP=ON \
    -D PYTHON3_EXECUTABLE=$(which python3) ..
# Start compilation and installation.
make -j && make install
```

You can add the following security configuration options as needed:

| Option | Description   |
| ------------ | ------------ |
| -fPIC | Generates position-independent code.|
| -fPIE | Generates position-independent executable files.|
| -fstack-protector-strong |  Enables stack overflow protection.|
| -D_FORTIFY_SOURCE=2 | Enables buffer overflow check during compilation and runtime.|
| -ftrapv | Checks for runtime errors.|
| -Wl,-z,relro,-z,now,-s | Enables memory security options to prevent attacks such as code injection.|

In `CMAKE_C_FLAGS` and `CMAKE_CXX_FLAGS`, add the required security configuration options, and add the link options `CMAKE_EXE_LINKER_FLAGS`, `CMAKE_SHARED_LINKER_FLAGS`, and `CMAKE_MODULE_LINKER_FLAGS`. In addition, enable the `CMAKE_SKIP_RPATH` option to avoid hard coding of paths during runtime. Then, recompile and install OpenCV. For example:

```bash
-D CMAKE_C_FLAGS="-O3 -march=armv8-a -fPIC -fPIE -fstack-protector-strong -D_FORTIFY_SOURCE=2 -ftrapv" \
-D CMAKE_CXX_FLAGS="-O3 -march=armv8-a -fPIC -fPIE -fstack-protector-strong -D_FORTIFY_SOURCE=2 -ftrapv" \
-D CMAKE_EXE_LINKER_FLAGS=" -pie -Wl,-z,relro,-z,now,-s " \
-D CMAKE_SHARED_LINKER_FLAGS=" -Wl,-z,relro,-z,now,-s " \
-D CMAKE_MODULE_LINKER_FLAGS=" -Wl,-z,relro,-z,now,-s "  \
-D CMAKE_SKIP_RPATH=ON \
```

**Step 6** Check whether OpenCV is installed.

``` bash
#Configure environment variables. `/home/opencv_install` indicates the OpenCV installation path, and `python3.9` indicates the Python version of the system.
export PYTHONPATH="/home/opencv_install/lib/python3.9/site-packages:$PYTHONPATH"
python3 -c "import cv2; print(cv2.__version__)"
```
If the OpenCV version number is displayed, the installation is successful.
