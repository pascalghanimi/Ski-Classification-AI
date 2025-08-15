# Ski Turn Detection & Classification

This repository contains the code and documentation for my Master's thesis:  
**"Development of an AI-Based System for Detecting and Segmenting Turns in Alpine Skiing"**  
(_Entwicklung eines KI-gestützten Systems zur Erkennung und Segmentierung von Schwüngen im alpinen Skilauf_)

---

## 📌 Overview
The project develops a deep learning pipeline that:
- Detects ski turns in video footage.
- Classifies different turn types and directions.
- Uses only video input — no additional sensors needed.

<img width="944" height="531" alt="image" src="https://github.com/user-attachments/assets/6d889aad-0872-4952-a1d4-93a184b6c8e4" />

---

## 🎯 Goals
- Automate ski turn detection without invasive equipment.
- Achieve robust performance across various turn types and directions.
- Provide a scalable framework for sports analytics.

---

## 📂 Dataset
- **Source:** 1,059 skiing videos, reduced to 706 after quality checks.
- **Split:** 70% training, 15% validation, 15% test.
- **Classes:** CL, EKK, PD, PDK, PDL, PGK, PGL, PS.

---

## 🛠 Feature Extraction
From 3D joint coordinates, the following features were computed:
- Distance from Center of Mass (CoM) to ground.
- Knee angles (left & right).
- Segment-to-axis angles.
- Axes orientations for shoulders, hips, feet.
- Orientation vector from ankle midpoint to CoM.

<p align="center">
  <img src="https://github.com/user-attachments/assets/38c05b26-4ecb-4f65-be01-21892af43a39" width="48%">
  <img src="https://github.com/user-attachments/assets/c1893c7e-64b8-4906-afcf-cee4a3d0873c" width="48%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/8f124a93-920e-409c-b513-50373b8f6e85" width="48%">
  <img src="https://github.com/user-attachments/assets/1a4411d7-e329-4cf6-bba3-02ef74315bf0" width="48%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/2cde45d0-a025-4e23-a5d1-9d501d70bc14" width="48%">
</p>


---

## 🤖 Model Architectures

### 1. **Turn Type Classifier**
- **Model:** Bidirectional LSTM (2 layers, 128 hidden units each way).
- **Attention mechanism** after LSTM layers.
- **Loss:** Focal Loss for class imbalance.
- **Optimizer:** Adam (lr=0.001).
- **Training:** Up to 300 epochs with early stopping (patience=30).

### 2. **Turn Direction Classifier**
- **Model:** Bidirectional LSTM (same setup).
- **Loss:** Cross-entropy.
- **Optimizer:** Adam (lr=0.001).


---

## 📊 Results

### Turn Type Classifier:
- **Precision:** PD & PS = 1.00, PGL = 0.94, PDK = 0.75, rest between 0.83–0.89.
- **Recall:** PD & PGK = 1.00, PS = 0.92, PGL = 0.94, PDK = 0.86, rest between 0.79–0.81.
- **F1-Score:** PD = 1.00, PS = 0.96, PGL = 0.94, PGK = 0.91, PDL = 0.81, CL = 0.83, EKK = 0.84, PDK = 0.80.

<p align="center">
  <img src="https://github.com/user-attachments/assets/7aafe84a-d9ad-41f6-b27c-b67a43c20bed" width="48%">
  <img src="https://github.com/user-attachments/assets/19c93a74-5b10-4c86-ba8e-3f874514172b" width="48%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/dda2cd0f-d098-485a-9211-ac239d9b1f1d" width="48%">
  <img src="https://github.com/user-attachments/assets/7147976e-d20e-4053-96a8-f8600bed0a72" width="48%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/be3f0f92-ee8a-4fd1-9ab1-c724019eca3a" width="48%">
</p>



### Turn Direction Classifier:
- **Precision:** Left = 0.93, Right = 0.93.
- **Recall:** Left = 0.92, Right = 0.93.
- **F1-Score:** Left = 0.92, Right = 0.93.

|                | Precision | Recall | F1    |
|----------------|-----------|--------|-------|
| **Linksschwung** | 0.937     | 0.944  | 0.940 |
| **Rechtsschwung**| 0.940     | 0.933  | 0.936 |

<p align="center">
  <img src="https://github.com/user-attachments/assets/b734ecc5-0bed-42d8-976b-914c8ddb4f65" width="48%">
  <img src="https://github.com/user-attachments/assets/ec8afe61-71f4-4e87-8deb-1b8f18ae73ba" width="48%">
</p>


