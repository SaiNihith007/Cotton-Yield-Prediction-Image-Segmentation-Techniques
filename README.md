# Cotton Yield Prediction Using UAV Image Segmentation

This project builds an end-to-end machine learning pipeline for **cotton yield prediction** using high-resolution UAV (drone) images and **semantic segmentation** techniques. We segment cotton pixels using deep learning and predict yield using a simple regression model.

---

## 📌 Objective

- Segment cotton regions from UAV images using DL models
- Count white (cotton) pixels from masks
- Predict yield using linear regression

---

## 🛰️ Data Overview

- UAV imagery captured using **DJI Phantom 4** (4096×2160 resolution)
- Captured over a cotton field in **Texas High Plains** on Nov 9, 2022
- 5376 images total → 1866 labeled using **AnyLabeling + SAM**
- Each image linked to yield from a 20ft row of cotton

> ⚠️ Full dataset not shared due to restrictions. A few sample images and masks are provided under `data/sample_images/`.

---

## 📷 Pipeline Overview

```text
UAV Images → Labeling (SAM + AnyLabeling) → Segmentation (CNN Models) → Cotton Pixel Count → Linear Regression → Yield Prediction
