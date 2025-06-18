# Cotton Yield Prediction Using UAV Image Segmentation

This research project presents an end-to-end machine learning pipeline for **cotton yield prediction** using high-resolution UAV (drone) images and **semantic segmentation**. We segment cotton pixels using deep learning models and predict yield based on segmented pixel area using linear regression.

---

## 🤝 Research Collaboration

This project was conducted as part of a **research collaboration** under the guidance of **Dr. Haoyu Niu** and **Dr. Lan Zhou** at **Texas A&M University**. The study explores the intersection of **remote sensing, computer vision, and precision agriculture** for sustainable cotton farming.

---

## 📌 Objective

- To accurately segment cotton bolls from UAV images using state-of-the-art deep learning models.
- To calculate cotton-covered pixel areas and use them to estimate actual cotton yield.
- To evaluate segmentation performance and yield prediction accuracy.

---

## 🛰️ Data Overview

- UAV imagery captured on **Nov 9, 2022**, using **DJI Phantom 4** (4096×2160 resolution).
- Field located in the **Texas High Plains**, divided into 12 drip zones with different irrigation treatments.
- **5376 images** collected; **1866 labeled** using **AnyLabeling + Segment Anything Model (SAM)**.
- Each image corresponds to a physical cotton row with known yield (lbs/row).

> ⚠️ Due to data restrictions, we have only included 2–3 **sample raw images and masks** in `data/sample_images/`.

---

## 🧠 Methodology

### 🔹 Step 1: Image Labeling
- Used **SAM (ViT-B)** in **AnyLabeling** to auto-segment cotton bolls with polygon annotations.
- Generated binary masks from polygon coordinates using OpenCV.

### 🔹 Step 2: Image Preprocessing
- Resized all images to 128×128 or 256×256 depending on the model.
- Converted masks to binary (0 and 1) format for segmentation training.

### 🔹 Step 3: Segmentation Models Used
We experimented with both **TensorFlow** and **PyTorch-based** segmentation models:
- **Attention U-Net** (TensorFlow/Keras)
- **MAnet**, **LinkNet**, **FPN**, **PAN** (using `segmentation-models-pytorch`)
- **YOLOv11 segmentation** (via Ultralytics)

> All models were evaluated using **IOU (Jaccard Index)**.

### 🔹 Step 4: Yield Prediction
- Counted total **white pixels** (cotton area) from segmented masks.
- Aggregated image patches per row.
- Used **Linear Regression** to predict cotton yield (lbs/row) from pixel counts.

---

## 📊 Results

### 📍 IOU Scores (Segmentation Performance)

| Model         | IOU Score |
|---------------|-----------|
| Attention U-Net | **0.70** |
| MAnet          | 0.68      |
| LinkNet        | 0.677     |
| FPN            | 0.676     |
| PAN            | 0.66      |

> Despite trying multiple models, the best IOU plateaued at ~70%. Future improvements may include advanced encoders or dataset augmentation.

---

### 📈 Yield Prediction

- Linear regression on pixel count achieved:
  - **R² = 0.88**
  - **MAE = 3.9**
  - **MSE = 23.1**

This demonstrates that, even with moderate segmentation accuracy, a strong linear relationship exists between segmented cotton area and yield.

---

### 📸 Sample Visualizations

#### Regression Fit:
![Regression](results/yield_regression_results.png)

#### Actual vs Predicted Segmentation:
![Segmentation](results/Actual_vs_Predicted_cotton_pixels.png)

#### IOU Comparison:
![IOU Comparison](results/Segmentation_models_IOU_Comparision.png)


