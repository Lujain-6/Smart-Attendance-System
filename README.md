# Smart Attendance (Privacy-First) 🎯👁️
### Computer Vision Project | AI3302
**Department of Computer Science and Artificial Intelligence — Umm Al-Qura University**

---

## 📌 Project Overview
Attendance tracking is essential in organizations and educational institutions. Traditional methods (manual registration or card systems) are time-consuming and inefficient, while modern facial recognition solutions compromise user privacy and raise compliance and ethical concerns.

**Our Solution:** An intelligent, automated attendance system that counts attendees in lecture halls without relying on facial recognition or personal identity metrics. By utilizing advanced Object Detection focusing solely on **head detection**, the system answers *"How many people are present?"* rather than *"Who is present?"*, ensuring total anonymity through an automated real-time privacy-preserving mechanism.

---

## 👥 Authors & Project Context
* **Course:** Computer Vision Project
* **Project Number:** 11
* **Submission Date:** May 17, 2026
* **Instructor:** Seereen Noorwali

### Team Members & Contributions:
* **Lujain Omar Bakkar (Leader):** Implementation, File Organization, Model Description.
* **Maha Ahmed:** Introduction, Data Description.
* **Hebah Fahad Almatarafi:** Related Work, Comparison with Previous Approach.
* **Halima Abdullah Mohammed:** Gaps, Error Analysis.
* **Maryam Alessi:** Results, Experimental Results & Discussion, Future Work, Conclusion.

---

## 🚀 How It Works (System Architecture)

The system is deployed in **Google Colab** using a sequential, highly-optimized deep learning pipeline:

```text
[Input Data] ➡️ [Data Loading (OpenCV)] ➡️ [Ground Truth Mapping] 
     ➡️ [YOLOv8m Architecture] ➡️ [Post-Processing (Gaussian Blur ROI)] ➡️ [Final Count Output]
```

* **Ground Truth Processing:** Reads normalized annotation coordinates and calculates total line items per file to map real counts against input visual data.  
* **YOLOv8 Object Detection:** Extracts spatial and contextual features to define head coordinates even under crowd occlusion.  
* **Anonymization Engine:** Extracts the Region of Interest (ROI) and automatically applies a mathematical Gaussian Blur to obscure facial profiles while keeping the structural detection bounding box intact.  

---

## 🛠️ Tech Stack & Training Configuration
* **Environment:** Google Colab (T4 GPU Accelerator).  
* **Core Libraries:** `Ultralytics` (YOLOv8 framework), `OpenCV` (Image processing & Blurring), `NumPy` (Matrix manipulation), `Matplotlib`, `OS & Pathlib`.  

### Hyperparameter Settings:
| Parameter | Value | Parameter | Value |
| :--- | :--- | :--- | :--- |
| **Image Size** | 640 x 640 | **Initial Learning Rate** | 0.01 |
| **Batch Size** | 16 | **Final Learning Rate** | 0.00001 |
| **Workers** | 45 | **Momentum** | 0.937 |

### Data Augmentation Techniques:
To ensure high generalization against real-world variations without adding raw images, the following online augmentations were mapped:  
* **Hue:** 0.015 | **Saturation:** 0.7 | **Brightness:** 0.4  
* **Rotation:** 5.0 degrees | **Translation:** 0.1 | **Scaling:** 0.5  
* **Horizontal Flip:** 0.5 (50% probability)  

---

## 📊 Data & Dataset Shift
Initially, the *Classroom-Data* dataset was selected. However, during implementation, we shifted to the **SCUT-HEAD Dataset (Part A)** because the original dataset lacked location-based bounding boxes. SCUT-HEAD provides precise coordinate layout masks, teaching the model *where* the head is rather than just guessing numbers.  
* **Total Class Images Used:** 2000 images (Average resolution: 1076 x 605 pixels).  
* **Split Layout:** Training (1100 images) \| Validation (400 images) \| Testing (500 images).  

---

## 📈 Experimental Results & Metrics
Evaluated across 500 unseen test images, the system demonstrated phenomenal robustness under dynamic real-world classroom conditions:  
* **Mean Absolute Error (MAE):** 1.49 (Deviation of approx. 1-2 people per class)
* **Root Mean Square Error (RMSE):** 2.81  
* **Precision:** 0.971 \| **Recall:** 0.986 \| **F1-Score:** 0.979  
* **Strict Tolerance Margin (Within +/-3 people):** 87.2% Accuracy  
* **Loose Tolerance Margin (Within +/-5 people):** 94.2% Accuracy  
* **Exact Matches:** 231 Images  
* **Inference Speed:** 0.02 seconds (25ms) per image, proving real-time readiness.  

### Environmental Adaptation Highlights:
* **Camera Angles:** Successfully tracks targets from low side angles to overhead standard surveillance points.  
* **Lighting Variations:** Handles heavy natural light/shadows from windows as well as dim artificial lighting.  
* **Student Distributions:** Accurate whether the hall is packed or sparse with scattered seating.  

---

## 🔄 Technical Evolution: Watershed vs. YOLOv8
Our system evolved significantly from its initial design stage:  

| Feature | Traditional Approach (Watershed) | Our Current Approach (YOLOv8m) |
| :--- | :--- | :--- |
| **Methodology** | Pixel similarity, thresholding, morphology | Deep Learning object detection (learned features) |
| **Crowded Scenes** | Weak; fails to separate touching objects | Excellent; robust spatial feature distinction |
| **Lighting Changes** | Poor; easily distorted by shadows/noise | Highly Robust |
| **Inference Speed** | Slow / High computational complexity | Real-time (0.02 sec/image) |
| **Privacy Integration** | Manual intervention needed | Automated, automated ROI Gaussian Blurring |

---

## 🔍 Comprehensive Error Analysis
Through structural evaluation, 5 primary edge-case anomalies were identified:  
1. **Undercounting:** Occurs in hyper-congested zones where deep rows create massive overlapping occlusions.  
2. **Overcounting:** Occurs when background structures (like rounded chair backs in empty rows) reflect human-head visual properties at specific angles.  
3. **Occlusion:** Back-row student tracking drops off if preceding rows block the camera's line-of-sight.  
4. **Overlapping Heads:** Heads merging visually when students sit extremely close to one another.  
5. **Close-up Proximity:** Oversized head structures directly beneath low overhead cameras sometimes fail to trigger anchor-free layer limits because they differ from average dataset dimensions.

---

## 🛠️ Code Structure Overview
The pipeline inside `Computer_Vision_Project_Code.ipynb` executes via these steps:
* **Step 1:** Install and Import Libraries  
* **Step 2:** Download Dataset from Kaggle  
* **Step 3:** Load Ground Truth Labels  
* **Step 4:** Load YOLO Model  
* **Step 5:** Count Students with YOLO and Apply Blurring  
* **Step 6:** Evaluation & Statistical Mapping  

---

## 🚀 Future Enhancements
* Incorporating real-time tracking algorithms like **DeepSORT** for live video monitoring.  
* Adopting multi-camera architectures to solve single-view blind spots and occlusions.  
* Deploying Super-Resolution preprocessing filters to boost small-head detection in low-quality frames.  

---

## 📜 References
1. Chan, A. B., et al. (2008). *Privacy preserving crowd monitoring: Counting people without people models or tracking.* CVPR.  
2. Li, Y., et al. (201
