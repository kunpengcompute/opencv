# Introduction to OpenCV

## What's New

* Optimized the performance of common OpenCV functions based on Kunpeng servers. The involved functions include `erode`, `Canny`, `HoughLines`, `HoughCircles`, `norm`, `mean`, `determinant`, `completeSymm`, `eigen`, `moments`, `minAreaRect`, `connectedComponents`, `connectedComponentsWithStats`, `minMaxLoc`, `warpPerspective`, `rotate`, `perspectiveTransform`, and `transform`.

## Overview

Kunpeng OpenCV optimizes OpenCV based on Kunpeng servers. It stores patches for OpenCV performance optimization. The patches are mainly used to optimize the performance of common image functions in fields such as ultrasound healthcare, AIGC, and industrial quality inspection.

## Basic Concept

OpenCV is an open-source computer vision library that provides a wide range of image and video processing functions, including image filtering, edge detection, feature extraction, object recognition, face detection, camera calibration, and motion tracking. It is widely used in fields such as facial recognition, autonomous driving, augmented reality, medical image analysis, security surveillance, and industrial automation. It supports multiple programming languages (such as Python and C++) and cross-platform deployment. It is one of the most commonly used core tools in computer vision development.

# Directory Structure

``` bash
├── docs/                  # Documentation
    ├── en                 # English documentation
        ├── deploy.md      # Environment deployment
        ├── LICENSE        # Document license
        ├── quick_start.md # Quick start
├── LICENSE                # License description file
├── 0001-opencv_4.10.0-optimize-core-v1.0.1.patch     # Optimization patch for the core module
├── 0002-opencv_4.10.0-optimize-imgproc-v1.0.1.patch  # Optimization patch for the imgproc module
├── README.md              # Project introduction document
```

# Version Description

## Version Mapping

| Patch Version| GCC Version|Matching OpenCV Version| Download Link                                                    |
| -------- | -------- |-------------- | ------------------------------------------------------------ |
| 1.0.1   | 10.3.1   |4.10.0         | [Download link](https://github.com/opencv/opencv/archive/refs/tags/4.10.0.zip)|

# Environment Deployment

For details about how to deploy the Kunpeng OpenCV environment, see [Kunpeng OpenCV Deployment Guide](./docs/en/deployment_guide.md).

# Quick Start

The mean function is used as an example to calculate the mean value of each channel of an image. For details, see [Quick Start](./docs/en/quick_start.md).

# Features

The patches for optimizing the OpenCV performance in this repository mainly optimize the performance of functions in the following table.

| Function                        | Description (General)                                        |
| ------------------------------ | ------------------------------------------------------------ |
| `erode`                        | Performs morphological corrosion on images to eliminate small objects, separate objects, or shrink the foreground area.|
| `Canny`                        | Detects edges in an image using the Canny algorithm and outputs a binary edge map.           |
| `HoughLines`                   | Detects straight lines in a binary image using the Hough transform and returns the polar coordinates (ρ, θ) of the lines.|
| `HoughCircles`                 | Detects circles in a grayscale image using the Hough gradient method and returns the coordinates of the circle center and radius.    |
| `norm`                         | Computes the norm (such as L1, L2, or infinity norm) of an array (such as an image or vector) to measure its size or difference.|
| `mean`                         | Computes the mean value of each channel in an image or array.                      |
| `determinant`                  | Computes the determinant of a square matrix, which is often used to determine whether a matrix is invertible or to calculate the geometric volume scaling factor.|
| `completeSymm`                 | Completes a lower triangular (or upper triangular) symmetric matrix into a complete symmetric matrix.      |
| `eigen`                        | Computes the eigenvalues and corresponding eigenvectors of a real symmetric matrix.                    |
| `moments`                      | Computes the image moments (including spatial moments, central moments, and normalized central moments) of a binary or grayscale image, which are used for shape analysis and centroid calculation.|
| `minAreaRect`                  | Computes the minimum-area bounding rotated rectangle (angle-enclosed bounding box) of a point set.          |
| `connectedComponents`          | Performs connected component analysis on a binary image, labels all 4- or 8-connected components, and returns the number of labels and the labe map.|
| `connectedComponentsWithStats` | In addition to connected component analysis, returns statistics (such as bounding box, area, and centroid) for each connected component.|
| `minMaxLoc`                    | Finds the minimum and maximum values in a single-channel array (such as a grayscale image) and their corresponding coordinates.|
| `warpPerspective`              | Applies perspective transformation (using a 3×3 homography matrix) to project an image onto a new view or plane.|
| `rotate`                       | Rotates an image by a multiple of 90 degrees (for example, 90 degrees clockwise, 180 degrees, or 90 degrees counterclockwise).  |
| `perspectiveTransform`         | Applies perspective transformation to a 2D or 3D point set (using a 3×3 homography matrix).         |
| `transform`                    | Applies affine or linear transformation (using a 2×3 or 3×3 transformation matrix) to a point set, which is commonly used for coordinate mapping.|

# Helpful Links

For details, see the [OpenCV documentation](https://docs.opencv.org/4.10.0/).

# License

This project is licensed under Apache License Version 2.0. For details, see [LICENSE](./LICENSE).
The documents of this project are licensed under CC-BY 4.0. For details, see [LICENSE](./docs/en/LICENSE).

# Contribution Statement

We welcome your contributions to the community. If you have any questions/suggestions or want to provide feedback on feature requirements and bug reports, you can submit [issues](https://gitcode.com/boostkit/opencv/issues). For details, see the [contribution guideline](https://gitcode.com/boostkit/community/blob/master/docs/contributor/contributing.md). You are also welcome to share insights in [Discussions](https://gitcode.com/boostkit/community/discussions). Thank you for your support.
