---
layout: post
title: "Digital Image Fundamentals"
date: 2026-09-28
category: guide
tags: [image-processing, computer-vision, opencv, rgb, hsv, pixels]
---

A practical guide to how digital images are captured, represented, and manipulated — from Bayer filters and pixels to RGB, HSV, coordinates, and core OpenCV operations.

## Contents

1. [How Is a Digital Image Captured & Processed?](#1-how-is-a-digital-image-captured--processed)
2. [Pixels](#2-pixels)
3. [Image Resolution](#3-image-resolution)
4. [Bit Depth](#4-bit-depth)
5. [Grayscale](#5-grayscale)
6. [RGB](#6-rgb)
7. [HSV (Hue, Saturation, Value)](#7-hsv-hue-saturation-value)
8. [Image Coordinates](#8-image-coordinates)
9. [Pixel Intensity](#9-pixel-intensity)
10. [Image Operations](#10-image-operations)
11. [References](#references)

---

## 1. How Is a Digital Image Captured & Processed?

Light falls on a **sensor** present in a camera / phone which consists of a grid of pixels. The light-sensitive element on a pixel cannot detect colour — only **intensity**.

To calculate the RGB values of each pixel, the camera mostly uses a **Bayer filter**. This Bayer filter places an R, G, or B filter on top of each pixel, helping to detect the value of one particular colour. The missing two colour values are estimated using adjacent pixels through **demosaicing**.

The Bayer filter pattern uses **two green pixels for every red and blue pixel**, because the human eye is more sensitive to green than to other wavelengths. The Bayer filter requires only one filter sensor per pixel, rather than needing separate sensors for each colour channel. Digital cameras then use demosaicing algorithms to convert this colour mosaic into an equally sized mosaic of true colours, effectively reconstructing the full RGB information at every pixel location.

![Capture overview: light falls on the sensor grid (intensity only); Bayer filter (2G:1R:1B); demosaicing estimates the missing two colours; R+G+B combine into full colour.](/images/digital-image-fundamentals/fig1-p0.png)
*Figure 1 — Capture overview: sensor → Bayer filter (2G:1R:1B) → demosaicing → full colour.*

**Key takeaway:** each photosite measures one colour; full RGB at every pixel is *reconstructed*.

---

## 2. Pixels

**Pixel**, short for *picture element*, represents a single point of light carrying colour and brightness information.

- For a **greyscale** image, each pixel has a value between **0 and 255**, representing the darkest and lightest parts of the image respectively.
- **Coloured** images consist of three separate channels: **red, green, and blue**. The overall image is formed by combining these RGB channels into one consolidated image, producing the final full-colour picture that we see.

---

## 3. Image Resolution

- An image with **28 × 28 pixels** has a resolution of **784 pixels**.
- **Display resolution** is the maximum that can fit on the full dimension of an image. Example: `800 × 600 = 480,000` pixels on a PC screen.
- **Pixel density** determines the number of pixels per inch of image. The more pixels per unit width, the higher the clarity of the image.
- Resolution is measured in **pixels per inch (PPI)**. The size of a pixel is determined by how much space it takes in a square inch.

In these notes:

> **Pixel dimension = Length × PPI.**

More PPI leads to more information, detail, sharpness, and better quality.

![Image resolution, display resolution, and PPI.](/images/digital-image-fundamentals/fig2-p1.png)
*Figure 2 — Image resolution = width × height (total pixel count); display resolution = max pixels on screen (e.g. 800 × 600); pixel density (PPI) = pixels per inch.*

![Resolution comparison: 300 ppi versus 72 ppi (cloud detail).](/images/digital-image-fundamentals/fig3-p1.png)
*Figure 3 — Resolution comparison: 300 PPI vs 72 PPI. Same scene, far more detail at higher PPI.*

| Term | Meaning | Example |
|---|---|---|
| Image resolution | width × height = total pixels | 28 × 28 = 784 |
| Display resolution | max pixels a screen can show | 800 × 600 = 480,000 |
| Pixel density (PPI) | pixels per inch | 300 PPI sharper than 72 PPI |

---

## 4. Bit Depth

**Bit depth** refers to the number of bits used to represent colour or brightness information of a single pixel in a digital image. Images are computed using the binary system.

In **line art**, where only two colours are required — 0 for black and 1 for white — **one bit suffices**. However, bit depth gives a pixel more information than just two values, enabling richer tonal representation.

For greyscale images, **8 bits = 1 byte** of data per pixel. When an image is converted to an 8-bit image, it contains 8 bits of information within each pixel. With 8 bits, we have:

> **2⁸ = 256 tonal levels**

…meaning the image can represent 256 distinct shades of grey ranging from pure black to pure white. This is a significant improvement over 1-bit images, which can only represent two values.

![Bit depth — 1-bit versus 8-bit greyscale.](/images/digital-image-fundamentals/fig4-p1.png)
*Figure 4 — 1-bit (line art, 2¹ = 2 values per pixel) versus 8-bit greyscale (2⁸ = 256 values per pixel). Bit depth directly affects smoothness and detail.*

---

## 5. Grayscale

Grayscale is the simplest model, which represents colours using the brightness range **0 (black) to 255 (white)**. Grayscale is used when **shape, structure, and brightness** matter more than colour representation.

Grayscale uses less space and processes computations faster.

**Applications:**

1. **OCR and document scanning** — captures more detail while keeping file size small.
2. **Medical imaging and terrain mapping** — provides more depth. An 8-bit grayscale image shows 256 shades of grey, whereas a 16-bit image provides 65,536 shades. 8-bit is for general use cases, while 16-bit is for medical imaging and remote sensing.

| Depth | Levels | Use |
|---|---|---|
| 1-bit | 2 | line art |
| 8-bit | 256 | general use |
| 16-bit | 65,536 | medical, remote sensing |

---

## 6. RGB

RGB uses **additive colour mixing** of the primary colours. It is heavily used in screens, leading to ubiquitous image processing. The RGB model is based on a **3D Cartesian system**.

Digital images are **8 bits per channel**, meaning 2⁸ = 256 values per channel. Therefore:

> **R × G × B = 256³ = 16,777,216 colours**

With 8 bits of information per channel we have 2⁸ = 256 levels. For example, `(255, 0, 0)` corresponds to pure red.

![RGB colour cube.](/images/digital-image-fundamentals/fig5-p2.png)
*Figure 5 — RGB colour cube: three axes (R, G, B), each 0–255.*

---

## 7. HSV (Hue, Saturation, Value)

HSV is a way to represent colours that is more **perceptually uniform** for humans compared to RGB. It is closer to how humans perceive colours.

- **Hue** represents the type of colour, measured in degrees on a colour wheel from 0 to 360. For example: red = 0°, yellow = 60°, green = 120°, cyan = 180°, blue = 240°, magenta = 300°, red = 360°.
- **Saturation** measures intensity, ranging from 0% to 100%. 0% represents grey and 100% represents pure colour. Higher saturation means more vibrant colour.
- **Value** represents brightness, ranging from 0% to 100%. 0% is pure black and 100% is full brightness of the hue. At 0% it becomes black regardless of hue and saturation.

HSV has an advantage over RGB for extracting grayscale information from a colour image, since each band/channel can be separated in HSV.

![HSV — hue, saturation, value.](/images/digital-image-fundamentals/fig6-p3.png)
*Figure 6 — HSV: hue selects the base colour on the wheel (0–360°); saturation is the amount/depth of colour; value is the brightness (0–100%).*

---

## 8. Image Coordinates

Most image processing libraries and computer vision applications use a coordinate system that might feel slightly different from the Cartesian coordinates learned in mathematics. The standard convention is:

- **Origin (0, 0)** — located at the **top-left corner** of the image.
- **X-axis** — runs horizontally from left to right. The x-coordinate represents the **column number**.
- **Y-axis** — runs vertically from top to bottom. The y-coordinate represents the **row number**.

So, a pixel's location is typically specified by a pair of values `(x, y)`, where `x` is the horizontal position (column) and `y` is the vertical position (row), both starting from 0.

![Image coordinate system — origin top-left.](/images/digital-image-fundamentals/fig7-p3.png)
*Figure 7 — Buffer/pixel coordinates (integer). Used to identify the exact location of a pixel inside an image with coordinates (x, y). The origin (0, 0) is the top-left corner.*

> ⚠️ Unlike maths class: **y grows downwards**.

---

## 9. Pixel Intensity

**Pixel intensity** refers to the sum, mean, or median intensity of pixels within a region of interest (ROI) in an image.

- In **grayscale** images, intensity is directly proportional to the pixel value (0 = black, 255 = white).
- In **colour** images, intensity can be computed from the RGB channels.

Pixel intensity is a fundamental concept in image processing. It is used for tasks such as **thresholding, segmentation, and feature extraction**. The mean intensity of an image gives a measure of its overall brightness. The sum of all pixel intensities gives the total brightness. Median intensity is robust against noise.

---

## 10. Image Operations

These geometric transformations of images do not change the image content but deform the pixel grid and map this deformed grid to the destination image.

### 10.1 Resize

Scaling is just resizing of the image. Preferable interpolation methods are `cv.INTER_AREA` for shrinking and `cv.INTER_CUBIC` (slow) and `cv.INTER_LINEAR` for zooming.

Example: 800 × 600 → resize (×0.5) → 400 × 300; pixels: 480,000 → 120,000.

The OpenCV signature is:

```python
cv.resize(src, dsize[, dst[, fx[, fy[, interpolation]]]]) -> dst
```

```python
import cv2 as cv
img = cv.imread("messi5.jpg")
res = cv.resize(img, None, fx=2, fy=2, interpolation=cv.INTER_CUBIC)
# OR
height, width = img.shape[:2]
res = cv.resize(img, (2*width, 2*height), interpolation=cv.INTER_CUBIC)
```

### 10.2 Crop

Cropping means selecting only a particular region of an image and removing the rest. Cropping does not resize the selected content; it simply selects a region. There is no dedicated `crop()` function. OpenCV uses NumPy slicing: `image[y1:y2, x1:x2]`.

```python
# NumPy slicing: image[y1:y2, x1:x2]
ball = img[280:340, 330:390]
```

### 10.3 Rotate

Rotation means turning an image around a particular point by a certain angle. Parameters: centre of rotation, angle, scale. A positive angle means counter-clockwise.

```python
import cv2 as cv
img = cv.imread("image.jpg")
height, width = img.shape[:2]
center = (width // 2, height // 2)
matrix = cv.getRotationMatrix2D(center, 45, 1.0)
rotated = cv.warpAffine(img, matrix, (width, height))
```

### 10.4 Flip

Flipping creates a mirror-like transformation of an image.

```python
import cv2 as cv
horizontal = cv.flip(img, 1)  # Horizontal flip
vertical = cv.flip(img, 0)    # Vertical flip
both = cv.flip(img, -1)       # Both directions
```

### 10.5 Translate

Translation is the shifting of an object's location.

```python
import numpy as np
import cv2 as cv
M = np.float32([[1, 0, 100], [0, 1, 50]])
dst = cv.warpAffine(img, M, (cols, rows))
```

---

## References

1. Bayer filter: <https://www.whatdigitalcamera.com/technology_guides/bayer-filter-work-60461>
2. Demosaicing: <https://en.wikipedia.org/wiki/Demosaicing>
3. Pixel, Bit depth: <https://graphics-pro.com/feature/the-anatomy-of-a-pixel/>
4. Resolution, Bits and Channels: <https://blogs.ubc.ca/visa110/files/2017/06/ResolutionBitsChannels.pdf>
5. Pixel density, image resolution: <https://medium.com/conspectushub/digital-image-representation-inside-a-computer-3481f87d348c>
6. Grayscale: <https://www.lenovo.com/us/en/glossary/grayscale/>
7. RGB: <https://vincmazet.github.io/bip/digital-images/color-models/>
8. HSV: <https://zenn.dev/yuto_mo/articles/2f4e8168cc817f>
9. HSV image: <https://medium.com/@dijdomv01/a-beginners-guide-to-understand-the-color-models-rgb-and-hsv-244226e4b3e3>
10. Image co-ordinate system: <https://apxml.com/courses/introduction-to-computer-vision/chapter-2-digital-image-fundamentals/image-coordinate-systems>
11. Resize, Translate, Rotate (geometric transformations): <https://docs.opencv.org/4.13.0/da/d6e/tutorial_py_geometric_transformations.html>
12. Crop/ROI via NumPy slicing: <https://docs.opencv.org/4.12.0/d3/df2/tutorial_py_basic_ops.html>
13. Flip (flipCode): <https://docs.opencv.org/4.5.4/d2/de8/group__core__array.html>
