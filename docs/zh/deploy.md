## 鲲鹏OpenCV环境部署指南
### 安装说明
本文主要介绍鲲鹏优化版OpenCV的环境部署步骤。
### 安装步骤
> 建议将系统的超线程功能打开，以获取最佳性能。
#### 1.根据版本配套说明，下载开源社区[opencv-4.10.0.zip](https://github.com/opencv/opencv/archive/refs/tags/4.10.0.zip)到/home下并解压
``` bash
unzip opencv-4.10.0.zip #解压后得到/home/opencv-4.10.0
```
#### 2.下载[本仓库文件](https://raw.gitcode.com/boostkit/opencv/archive/refs/heads/master.zip)到/home目录下并解压
``` bash
unzip opencv-master.zip #解压后得到/home/opencv-master
#或者使用git clone方式
git clone https://gitcode.com/boostkit/opencv.git
```
#### 3.安装依赖库

``` bash
yum install -y binutils cmake git pkgconfig make patch gcc-10.3.1 gcc-c++-10.3.1 lapack ffmpeg ffmpeg-devel libjpeg-* python3-devel python3-numpy
```

#### 4.应用优化补丁

``` bash
cd /home/opencv-4.10.0
# 复制补丁文件
cp /home/opencv-master/*.patch ./
# 应用优化补丁
for patch in $(ls -v *.patch); do patch -p1 < "$patch"; done
```

#### 5.编译安装OpenCV

``` bash
mkdir build && cd build
# 执行cmake，默认安装位置/usr/local，可根据需要修改
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

#### 6.验证OpenCV是否成功安装，执行以下命令输出版本号即代表安装成功

``` bash
#设置环境变量，/usr/local是OpenCV安装路径，python3.9是系统的python版本
export PYTHONPATH="/usr/local/lib/python3.9/site-packages:$PYTHONPATH"
python3 -c "import cv2; print(cv2.__version__)"
```