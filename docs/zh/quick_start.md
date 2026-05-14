# 快速入门

在进行快速入门前，请参考[安装指南](./installation_guide.md)完成鲲鹏优化版opencv的安装，如果已经安装，请忽略。

## Python调用方式

1. 新建`quick_start.py`文件，并写入以下内容后，保存文件。

    ``` python
    #导入cv2库
    import cv2
    #读取图片
    img = cv2.imread('input.jpg')
    #计算每个通道的平均值
    mean_values = cv2.mean(img)
    print("各通道平均值 (B, G, R, A):", mean_values)
    ```

2. 运行`quick_start.py`。

    ``` bash
    python3 quick_start.py
    ```

## c++调用方式

1. 新建`quick_start.cpp`文件，并写入以下内容后，保存文件。

    ``` c++
    // 引入OpenCV头文件
    #include <opencv2/opencv.hpp>
    // 引入标准库头文件
    #include <iostream>

    int main()
    {
        // 读取图片
        cv::Mat img = cv::imread("input.jpg");
        if (img.empty())
        {
            std::cerr << "Error: Could not load image!" << std::endl;
            return -1;
        }
        // 计算图像各通道的平均值（B, G, R, Alpha）
        cv::Scalar mean_values = cv::mean(img);

        std::cout << "各通道平均值 (B, G, R, A): "
                << mean_values[0] << ", "
                << mean_values[1] << ", "
                << mean_values[2] << ", "
                << mean_values[3] << std::endl;
        return 0;
    }
    ```

2. 配置环境变量。其中`/home/opencv_install/`是OpenCV的安装路径，请根据实际安装路径进行修改。

    ``` bash
    export PKG_CONFIG_PATH=/home/opencv_install/lib64/pkgconfig:$PKG_CONFIG_PATH
    export LD_LIBRARY_PATH=/home/opencv_install/lib64:$LD_LIBRARY_PATH
    ```

3. 编译并运行`quick_start.cpp`。

    ``` bash
    g++ quick_start.cpp -o quick_start $(pkg-config --cflags --libs opencv4)
    ./quick_start
    ```
