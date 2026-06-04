
# Quick Start

## Python Calling

**Step 1** Create the `quick_start.py` file, write the following content into the file, and save the file.

``` python
#Import the cv2 library.
import cv2
#Read images.
img = cv2.imread('input.jpg')
#Calculate the mean value of each channel.
mean_values = cv2.mean(img)
print("Mean value of each channel (B, G, R, A):", mean_values)
```

**Step 2** Run `quick_start.py`.

``` bash
python3 quick_start.py
```

## C++ Calling

**Step 1** Create the `quick_start.py` file, write the following content into the file, and save the file.

``` c++
// Include the OpenCV header file.
#include <opencv2/opencv.hpp>
// Include the standard library header file.
#include <iostream>

int main()
{
    // Read images.
    cv::Mat img = cv::imread("input.jpg");
    if (img.empty())
    {
        std::cerr << "Error: Could not load image!" << std::endl;
        return -1;
    }
    // Calculate the mean value of each channel (B, G, R, Alpha).
    cv::Scalar mean_values = cv::mean(img);

    std::cout << "Mean value of each channel (B, G, R, A): "
              << mean_values[0] << ", "
              << mean_values[1] << ", "
              << mean_values[2] << ", "
              << mean_values[3] << std::endl;
    return 0;
}
```

**Step 2** Configure environment variables. `/home/opencv_install/` indicates the OpenCV installation path. Change it to the actual installation path.

``` bash
export PKG_CONFIG_PATH=/home/opencv_install/lib64/pkgconfig:$PKG_CONFIG_PATH
export LD_LIBRARY_PATH=/home/opencv_install/lib64:$LD_LIBRARY_PATH
```

**Step 3** Compile and run `quick_start.py`.

``` bash
g++ quick_start.cpp -o quick_start $(pkg-config --cflags --libs opencv4)
./quick_start
```
