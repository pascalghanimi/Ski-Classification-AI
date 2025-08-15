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

**Image here** (System overview diagram from thesis)

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

**Image here** (Example dataset frames & class distribution plot)

---

## 🛠 Feature Extraction
From 3D joint coordinates, the following features were computed:
- Distance from Center of Mass (CoM) to ground.
- Knee angles (left & right).
- Segment-to-axis angles.
- Axes orientations for shoulders, hips, feet.
- Orientation vector from ankle midpoint to CoM.

**Image here** (Feature extraction illustration from thesis)

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

**Image here** (Model architecture diagram)

---

## 📊 Results

### Turn Type Classifier:
- **Precision:** PD & PS = 1.00, PGL = 0.94, PDK = 0.75, rest between 0.83–0.89.
- **Recall:** PD & PGK = 1.00, PS = 0.92, PGL = 0.94, PDK = 0.86, rest between 0.79–0.81.
- **F1-Score:** PD = 1.00, PS = 0.96, PGL = 0.94, PGK = 0.91, PDL = 0.81, CL = 0.83, EKK = 0.84, PDK = 0.80.

### Turn Direction Classifier:
- **Precision:** Left = 0.93, Right = 0.93.
- **Recall:** Left = 0.92, Right = 0.93.
- **F1-Score:** Left = 0.92, Right = 0.93.

**Image here** (Confusion matrices & performance plots)

