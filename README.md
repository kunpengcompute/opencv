## 简介

### 项目介绍

鲲鹏OpenCV代码仓是基于鲲鹏服务器对开源OpenCV进行优化的成果。存放OpenCV性能优化的相关补丁。补丁主要对超声医疗、AIGC、工业质检等领域的常用图像函数进行性能优化。

### 基本概念

OpenCV 是一个开源的计算机视觉库，提供丰富的图像和视频处理功能，包括图像滤波、边缘检测、特征提取、目标识别、人脸检测、相机校准以及运动跟踪等。它广泛应用于人脸识别、自动驾驶、增强现实、医学图像分析、安防监控和工业自动化等领域，支持多种编程语言（如 Python、C++）和跨平台部署，是计算机视觉开发中常用的核心工具之一。

## 目录结构

```
├── COPYING.LGPLv2.1      # LGPL v2.1许可证文本
├── LICENSE.md            # 许可证说明文件
├── opencv-4.10.0.patch   #优化补丁
├── README.md             #项目介绍文档
```

## 版本说明

### 版本配套说明

| 补丁版本 | 配套OpenCV版本 | 下载链接                                                     |
| -------- | -------------- | ------------------------------------------------------------ |
| 4.10.0   | 4.10.0         | https://github.com/opencv/opencv/archive/refs/tags/4.10.0.zip |

## 环境部署
鲲鹏opencv的环境部署详见[鲲鹏opencv环境部署指南](https://gitcode.com/boostkit/opencv/blob/master/doc/zh/deploy.md)


## 快速入门
以mean函数为例，求图像各通道的平均值。详见[快速入门](https://gitcode.com/boostkit/opencv/blob/master/doc/zh/quick_start.md)

## 功能介绍&特性介绍

本仓库的OpenCV性能优化的相关补丁主要对以下这些函数进行了性能优化。

| 函数名                         | 函数功能描述（通用）                                         |
| ------------------------------ | ------------------------------------------------------------ |
| `erode`                        | 对图像执行形态学腐蚀操作，用于消除小物体、分离物体或缩小前景区域。 |
| `Canny`                        | 使用 Canny 算法检测图像中的边缘，输出二值边缘图。            |
| `HoughLines`                   | 利用霍夫变换在二值图像中检测直线，返回直线的极坐标表示（ρ, θ）。 |
| `HoughCircles`                 | 利用霍夫梯度法在灰度图像中检测圆形，返回圆心坐标和半径。     |
| `norm`                         | 计算数组（如图像或向量）的范数（如 L1、L2、无穷范数等），用于衡量大小或差异。 |
| `mean`                         | 计算图像或数组各通道的平均值（均值）。                       |
| `determinant`                  | 计算方阵的行列式值，常用于判断矩阵是否可逆或几何体积缩放因子。 |
| `completeSymm`                 | 将一个下三角（或上三角）对称矩阵补全为完整的对称矩阵。       |
| `eigen`                        | 计算实对称矩阵的特征值和对应的特征向量。                     |
| `moments`                      | 计算二值或灰度图像的图像矩（包括空间矩、中心矩、归一化中心矩等），用于形状分析和质心计算。 |
| `minAreaRect`                  | 计算点集的最小面积外接旋转矩形（带角度的包围框）。           |
| `connectedComponents`          | 对二值图像执行连通域分析，标记所有 4-或 8-连通区域，并返回标签数量和标签图。 |
| `connectedComponentsWithStats` | 在连通域分析基础上，额外返回每个连通区域的统计信息（如边界框、面积、质心等）。 |
| `minMaxLoc`                    | 查找单通道数组（如灰度图）中的最小值、最大值及其对应的位置坐标。 |
| `warpPerspective`              | 应用透视变换（基于 3×3 单应矩阵）将图像投影到新的视角或平面。 |
| `rotate`                       | 对图像进行90度倍数的旋转（如顺时针90°、180°、逆时针90°）。   |
| `perspectiveTransform`         | 对二维或三维点集应用透视变换（使用 3×3 单应矩阵）。          |
| `transform`                    | 对点集应用仿射或线性变换（使用 2×3 或 3×3 变换矩阵），常用于坐标映射。 |

## 学习文档

OpenCV中文文档：https://docs.opencv.ac.cn/4.10.0/

## License

本项目采用Apache License Version 2.0许可证。详见[LICENSE](https://gitcode.com/boostkit/opencv/blob/master/LICENSE.md)文件。

## 贡献声明

欢迎大家为社区做贡献，如果使用过程中有任何问题/建议，或者需要反馈特性需求和bug报告，可以提交[Issues](https://gitcode.com/boostkit/opencv/issues)联系我们，具体贡献方法可参考[这里](https://gitcode.com/boostkit/community/blob/master/docs/contributor/contributing.md)。同时也欢迎大家在[讨论专区](https://gitcode.com/boostkit/community/discussions)展开讨论交流。感谢您的支持



