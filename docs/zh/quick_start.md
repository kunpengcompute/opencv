
## 快速入门
### python调用方式
1.新建quick_start.py，并导入cv2库

```
import cv2
```

2.读取图像

```

img = cv2.imread('image.jpg')

# 计算图像各通道的平均值（B, G, R, Alpha）

```

3.调用mean函数

```
mean_values = cv2.mean(img)

print("各通道平均值 (B, G, R, A):", mean_values)
```
4.运行程序
```
python3 quick_start.py
```
### c++调用方式
1.新建 quick_start.cpp，并包含 OpenCV 头文件和 C++ 标准库头文件。
```
#include <opencv2/opencv.hpp>
#include <iostream>
```
2. 读取图像
```
cv::Mat img = cv::imread("image.jpg");

if (img.empty()) {
    std::cerr << "Error: Could not load image!" << std::endl;
    return -1;
}
```
3. 调用 mean 函数
```
// 计算图像各通道的平均值（B, G, R, Alpha）
cv::Scalar mean_values = cv::mean(img);

std::cout << "各通道平均值 (B, G, R, A): "
          << mean_values[0] << ", "
          << mean_values[1] << ", "
          << mean_values[2] << ", "
          << mean_values[3] << std::endl;
```
4. 运行程序
```
g++  quick_start.cpp -o quick_start $(pkg-config --cflags --libs opencv4)
./quick_start
```