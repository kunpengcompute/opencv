## 鲲鹏opencv环境部署指南
### 安装说明
本文主要介绍鲲鹏优化版opencv的环境部署步骤。
### 安装步骤
##### 1.根据版本配套说明，下载opencv-4.10.0.zip到Linux环境, 建议将环境的超线程功能打开，以获取最佳性能。

#### 2.安装依赖库

```
yum install -y binutils cmake git pkgconfig gcc gcc-c++ lapack ffmpeg ffmpeg-devel libjpeg-* python3-devel python3-numpy
```

#### 3.解压opencv-4.10.0.zip并应用opencv-4.10.0.patch

```
unzip opencv-4.10.0.zip && cd opencv-4.10.0 # 解压
git apply opencv-4.10.0.patch            # 应用优化补丁
```

#### 4.编译安装OpenCV

```
mkdir build && cd build
# 执行cmake
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D CMAKE_CXX_FLAGS="-O3 -march=armv8-a" \
    -D CMAKE_C_FLAGS="-O3 -march=armv8-a" \
    -D BUILD_opencv_python3=ON\
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D WITH_OPENMP=ON \
    -D PYTHON3_EXECUTABLE=$(which python3) ..
# 开始编译安装
make -j && make install
```

#### 5.验证OpenCV是否成功安装：执行以下命令输出版本号即代表安装成功。

```
python -c "import cv2; print(cv2.__version__)"
```