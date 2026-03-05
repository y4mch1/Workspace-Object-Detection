# Workspace Object Detection

![Project Banner](https://img.shields.io/badge/Computer_Vision-YOLOv8-blue?style=for-the-badge&logo=opencv)
![Python](https://img.shields.io/badge/Python-3.10-yellow?style=for-the-badge&logo=python)
![Platform](https://img.shields.io/badge/Platform-Google_Colab-orange?style=for-the-badge&logo=googlecolab)
![Data](https://img.shields.io/badge/Data_Annotation-Roboflow-purple?style=for-the-badge&logo=roboflow)

> **"High-precision object detection system developed with limited data (<60 samples), utilizing aggressive data augmentation and transfer learning to achieve >0.9 mAP on edge devices."**

---

## Project Overview

This project demonstrates an end-to-end Computer Vision pipeline designed to detect common workspace objects (Mouse, Charger, Earphone, Mask, Laptop) in real time. 

The primary challenge was to build a robust model using a **sparse dataset** while maintaining high accuracy on difficult objects like thin cables and occluded items. This project highlights the importance of **high-quality data annotation** and **data engineering** in modern AI development.

### Demo
<!-- GANTI DENGAN LINK GIF/VIDEO DEMO KAMU -->
![Real-time Detection Demo](https://cdn.discordapp.com/attachments/1170650328950124618/1478997524336345199/Z.png?ex=69aa6f48&is=69a91dc8&hm=c934cb0bf21b87413720864a88da454b4a2f8ef29dbcc2a253138db9dc9c3add&)
*(Real-time inference running on standard CPU)*

---

## Tech Stack & Tools

*   **Model Architecture:** YOLOv8 Nano (Ultralytics) - Chosen for real-time inference speed.
*   **Data Annotation:** Roboflow & LabelImg.
*   **Training Environment:** Google Colab (Tesla T4 GPU).
*   **Language:** Python.
*   **Evaluation:** Confusion Matrix, mAP@50 curves.

---

## Data Strategy 

### 1. Precision Annotation
Manual annotation was performed with strict guidelines to ensure pixel-perfect bounding boxes, critical for reducing False Positives.
*   **Occlusion Handling:** Labeled visible parts of objects obscured by hands or other items.
*   **Tight Bounding Boxes:** Minimized background noise within labels to improve feature extraction efficiency.

<!-- GANTI DENGAN SCREENSHOT LABELING ROBOFLOW KAMU -->
![Annotation Process](https://media.discordapp.net/attachments/1170650328950124618/1478997081145348138/Screenshot_2026-03-05_095249.png?ex=69aa6ede&is=69a91d5e&hm=040268fa8c484a5712ede09457d55171539457da172fdf0b1bd38915779dfa78&=&format=webp&quality=lossless&width=1692&height=804)
![Annotation Process](https://media.discordapp.net/attachments/1170650328950124618/1478997080277254144/Screenshot_2026-03-05_092701.png?ex=69aa6ede&is=69a91d5e&hm=1570fd495f724d4ff9d2ea4902dfc20567287329fab7b45484d539d6c2f49a44&=&format=webp&quality=lossless&width=1445&height=815)
*(Snapshot of the annotation process handling complex cable shapes)*

### 2. Augmentation Pipeline
To combat the small dataset size (initial 50 images), I implemented a synthetic data generation pipeline using Roboflow:
*   **Horizontal Flip:** To generalize object orientation.
*   **Rotation (±15°):** To simulate varying camera angles.
*   **Brightness Adjustment:** To ensure model robustness across different lighting conditions (Day/Night simulation).
*   **Result:** Dataset expanded 3x (approx. 150 images) for training.

---

## Performance Results

Despite the limited data, the model achieved exceptional performance, proving the effectiveness of the data strategy.

### Confusion Matrix
<!-- GANTI DENGAN GAMBAR CONFUSION MATRIX BIRU TADI -->
![Confusion Matrix](https://media.discordapp.net/attachments/1170650328950124618/1478996758506901616/8BgbfKsl1mcFoAAAAASUVORK5CYII.png?ex=69aa6e91&is=69a91d11&hm=4113c8120c1e773aef0700de7ae562ed13cab67c9785be85afb7e2bb8a782bdf&=&format=webp&quality=lossless&width=611&height=465)

**Key Insights:**
*   **100% Accuracy on Rigid Objects:** The model perfectly identified `Mouse` and `TWS Case` with zero misclassifications.
*   **High Recall on Deformable Objects:** `Earphones` and `Mask Straps` were detected with >90% accuracy, a challenging feat for computer vision due to their thin structure.
*   **Low False Positives:** The model effectively distinguishes between similar white objects (e.g., Charger vs. Earphone case).

---
