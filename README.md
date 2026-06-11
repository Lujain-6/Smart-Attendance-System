# Smart Attendance (Privacy-First) 🎯👁️
### AI3302 - Computer Vision Project

Welcome to the **Smart Attendance System**, an automated, AI-driven classroom attendance tracking solution built with a **privacy-first approach**. 

Unlike traditional automated systems that rely on facial recognition (which poses substantial privacy, data storage, and ethical concerns), this project utilizes advanced Object Detection to count students based on **head detection**. This ensures high accuracy in attendance monitoring while completely preserving individual identity and student privacy.

---

## 📌 Project Overview & Idea
In modern educational environments, manual attendance taking is time-consuming and prone to human error. Existing automated computer vision solutions usually track faces, which creates compliance risks with data privacy regulations.

**Our Solution:** By framing the problem as a specialized object detection task, this system identifies and counts **heads** within a classroom setting using the **YOLOv8** framework. 
* **Privacy by Design:** No faces are captured, stored, or analyzed. Students remain entirely anonymous.
* **Efficiency:** Instantly counts the total number of students present in a classroom from a standard wide-angle overhead image or video feed.

---

## 🛠️ Tech Stack & Components

* **Core Framework:** Python 3.x
* **Deep Learning Model:** [YOLOv8 (Ultralytics)](https://github.com/ultralytics/ultralytics) — Chosen for its state-of-the-art real-time object detection capabilities and exceptional speed/accuracy trade-off.
* **Dataset:** [SCUT-HEAD Dataset](https://github.com/HUST-Alpha/SCUT-HEAD) — A large-scale head detection dataset containing thousands of annotated heads in various crowded and classroom-like environments.
* **Tools & Utilities:** * `kagglehub` (for seamless dataset acquisition)
  * `OpenCV` & `Matplotlib` (for image processing and bounding box visualization)

---

## 🚀 How It Works (Pipeline)

1. **Environment Setup & Dependencies:** Installation of crucial vision libraries including `ultralytics`, `opencv-python`, and `kagglehub`.
2. **Dataset Acquisition:** Programmatic download and extraction of the **SCUT-HEAD Dataset** to train and validate the object detection model on classroom-oriented head layouts.
3. **Model Initialization:** Loading the pre-trained `YOLOv8` architecture, adapting its final detection layer to isolate a single class: `Head`.
4. **Training / Fine-tuning:** Training the network on the head annotations to learn distinct features of human heads from various viewing angles, lighting conditions, and partial occlusions.
5. **Inference & Head Counting:** Processing classroom images/video frames. The model predicts bounding boxes around every detected head and calculates the total count, which represents the automated attendance log.

---

## 📂 Repository Structure

```text
├── Computer_Vision_Project_Code.ipynb  # Main Jupyter Notebook containing the full pipeline
├── Project_Report.pdf                  # Comprehensive Project Report and Documentation 📄
├── README.md                           # Documentation and Project Guide
└── requirements.txt                    # Project Dependencies
