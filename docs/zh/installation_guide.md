# 鲲鹏OpenCV安装指南

## 安装说明

本文主要介绍鲲鹏优化版OpenCV的安装步骤。

## 环境要求

硬件环境

| 项目  | 说明    |
| ------------ | ------------ |
| CPU | 鲲鹏920新型号 |

软件环境

| 软件  | 版本    |
| ------------ | ------------ |
| OS | openEuler 22.03 LTS SP4 |
| 编译器 | GCC 10.3.1 或以上版本|
| make | 4.3 或以上版本|
| cmake | 3.10 或以上版本|

## 安装步骤
>
> **须知**
> 建议将系统的超线程功能打开，以获取最佳性能。
>
**步骤1** 根据版本配套说明，下载开源社区[opencv-4.10.0.zip](https://github.com/opencv/opencv/archive/refs/tags/4.10.0.zip)到`/home`下并解压。

``` bash
unzip opencv-4.10.0.zip
```

解压后得到/home/opencv-4.10.0

**步骤2** 下载本仓库文件到`/home`目录下。

``` bash
git clone https://gitcode.com/boostkit/opencv.git
```

**步骤3** 安装依赖库。

``` bash
yum install -y binutils cmake git pkgconfig make patch gcc-10.3.1 gcc-c++-10.3.1 lapack ffmpeg ffmpeg-devel libjpeg-* python3-devel python3-numpy
```

**步骤4** 应用优化补丁。

``` bash
cd /home/opencv-4.10.0
# 复制补丁文件
cp /home/opencv/*.patch ./
# 应用优化补丁
for patch in $(ls -v *.patch); do patch -p1 < "$patch"; done
```

**步骤5** 编译安装OpenCV。

``` bash
mkdir build && cd build
# 执行cmake，默认安装位置/home/opencv_install，可根据需要修改
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/home/opencv_install \
    -D CMAKE_CXX_FLAGS="-O3 -march=armv8-a" \
    -D CMAKE_C_FLAGS="-O3 -march=armv8-a" \
    -D BUILD_opencv_python3=ON\
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D WITH_OPENMP=ON \
    -D PYTHON3_EXECUTABLE=$(which python3) ..
# 开始编译安装
make -j && make install
```

根据用户需要，可添加安全配置选项：

| 选项  | 说明    |
| ------------ | ------------ |
| -fPIC | 生成位置无关代码。 |
| -fPIE | 生成位置无关可执行文件。 |
| -fstack-protector-strong |  启用栈溢出保护。 |
| -D_FORTIFY_SOURCE=2 | 开启编译&运行时缓冲区溢出检查。 |
| -ftrapv | 运行时错误检查。 |
| -Wl,-z,relro,-z,now,-s | 开启内存安全选项，避免代码注入等攻击。|

在`CMAKE_C_FLAGS`和`CMAKE_CXX_FLAGS`中新增需要的安全配置选项，同时新增链接选项`CMAKE_EXE_LINKER_FLAGS`、`CMAKE_SHARED_LINKER_FLAGS`和`CMAKE_MODULE_LINKER_FLAGS`，以及设置开启`CMAKE_SKIP_RPATH`选项，以避免运行时依赖路径硬编码，随后重新编译安装即可。例如：

```bash
-D CMAKE_C_FLAGS="-O3 -march=armv8-a -fPIC -fPIE -fstack-protector-strong -D_FORTIFY_SOURCE=2 -ftrapv" \
-D CMAKE_CXX_FLAGS="-O3 -march=armv8-a -fPIC -fPIE -fstack-protector-strong -D_FORTIFY_SOURCE=2 -ftrapv" \
-D CMAKE_EXE_LINKER_FLAGS=" -pie -Wl,-z,relro,-z,now,-s " \
-D CMAKE_SHARED_LINKER_FLAGS=" -Wl,-z,relro,-z,now,-s " \
-D CMAKE_MODULE_LINKER_FLAGS=" -Wl,-z,relro,-z,now,-s "  \
-D CMAKE_SKIP_RPATH=ON \
```

**步骤6** 验证OpenCV是否成功安装。

``` bash
#设置环境变量，/home/opencv_install是OpenCV安装路径，python3.9是系统的python版本
export PYTHONPATH="/home/opencv_install/lib/python3.9/site-packages:$PYTHONPATH"
python3 -c "import cv2; print(cv2.__version__)"
```

如果成功输出OpenCV的版本号，则表示安装成功。
