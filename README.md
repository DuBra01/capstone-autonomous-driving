# 🚗🧠 Autonomous Driving Capstone Project  
**Computer Vision + Data Analysis (Caltech Bootcamp)**  
GitHub: [@DuBra01](https://github.com/DuBra01)

---

## 📌 Project Overview

This capstone project is divided into **two major parts**, combining deep learning and real-world accident analysis:

1. **Vehicle Detection with YOLOv8 (Part 1)**  
2. **Exploratory Data Analysis of Tesla Fatal Crashes (Part 2)**  

All work is contained inside a single notebook:  
👉 **`notebook/Autonomous_Driving.ipynb`**

The project uses image-based detection to understand autonomous-driving environments and then analyzes Tesla crash data for safety trends.

---

# 🔹 Part 1 — YOLOv8 Vehicle Detection

Custom training of a YOLOv8 model to detect 11 vehicle categories: cars, buses, pickup trucks, trucks, motorcycles, bicycles, pedestrians, etc.

### **Dataset (Part 1)**  
Located in:  
datasets/part1/
Images.zip
labels.csv

(Images.zip stored via **Git LFS**)

---

## ✔️ Steps Performed

### **1. Data Preparation**
- Unzipped images and validated all 5,626 files.
- Cleaned and filtered `labels.csv` to include only valid image references.
- Standardized image paths and annotation structure.

### **2. Annotation Standardization**
Converted bounding boxes from pixel format  
`(xmin, ymin, xmax, ymax)`  
to **YOLO format**:  
class_id, x_center, y_center, width, height

All normalized by image dimensions.

### **3. Train/Validation/Test Split**
Created **stratified** splits to preserve class balance in:
train/
val/
test/

### **4. Model Training**
Two YOLO models were trained:

#### **A. YOLOv8n (nano baseline)**
- Partial backbone freeze  
- ~10 epochs  
- Fast & lightweight  
- mAP50 ≈ **0.57**

#### **B. YOLOv8s (final model)**
- Pretrained COCO backbone  
- First 10 layers frozen  
- AdamW optimizer  
- Cosine LR schedule  
- 20 epochs  
- Best accuracy–speed trade-off

### **5. Evaluation**
Generated:
- Precision–Recall curves  
- Confusion matrix  
- Per-class AP table  
- Detection examples on:
  - test set  
  - external images from the web  

---

## 📊 Final Model Performance (YOLOv8s)

### **Validation set**
- **mAP50:** ~**0.59**  
- **mAP50–95:** ~**0.41**

### **Test set**
- **mAP50:** ~**0.59**  
- **mAP50–95:** ~**0.40**

### **Best-detected classes**
- Car  
- Bus  
- Pickup truck  
- Bicycle  

### **Challenging classes**
- Non-motorized vehicle  
- Single unit truck  
- Pedestrians in complex scenes  

---

# 🔹 Part 2 — Tesla Fatal Crash EDA

Analyzed **303 cleaned entries** of Tesla-related fatal accidents.

### **Dataset (Part 2)**
Located in:
datasets/part2/
Tesla - Deaths.csv

---

## ✔️ Steps Performed

### **1. Data Cleaning**
- Removed duplicates (307 → 303 rows)  
- Inspected missing values  
- Dropped extremely sparse columns  
- Converted Autopilot-related fields into usable categories  

---

## **2. Temporal & Geographic Analysis**
- Events per **year** (increasing trend)  
- Fatal crashes by **country** (USA dominates)  
- State-level analysis for U.S. crashes  
- Identification of top accident states (CA, FL, TX)

---

## **3. Event Characteristics**
Analyzed:

- Number of deaths per event  
- Tesla driver death counts  
- Tesla occupant fatalities  
- Cyclist/pedestrian-involved events  
- Combined vulnerable-user + Tesla fatalities  
- Multi-vehicle collision frequency  

---

## **4. Tesla Model Analysis**
Grouped fatal events by Tesla model:
- Model S  
- Model 3  
- Model X  
- Model Y  
- Unknown / unspecified  

---

## **5. Autopilot vs Non-Autopilot**
- Cleaned “Autopilot claimed” into a binary flag  
- Counted Autopilot-related crashes  
- Compared **Autopilot vs non-Autopilot** events  
- Created grouped bar charts per model  

---

## 📁 Repository Structure

capstone-autonomous-driving/
├── notebook/
│   └── Autonomous_Driving.ipynb
│
├── datasets/
│   ├── part1/
│   │   ├── Images.zip
│   │   └── labels.csv
│   │
│   └── part2/
│       └── Tesla - Deaths.csv
│
└── README.md

---

# ▶️ How to Run the Project

### **1. Clone the Repository**
```bash
git clone https://github.com/DuBra01/capstone-autonomous-driving.git
cd capstone-autonomous-driving

2. Install Dependencies
pip install ultralytics pandas numpy matplotlib seaborn scikit-learn

3. Open the Notebook
jupyter notebook notebook/Autonomous_Driving.ipynb

4. Run the Notebook
Execute cells from top to bottom.

⚠️ Note:
Training YOLOv8 requires a GPU.
Weights and outputs are provided — retraining is optional.

⸻

🏁 Conclusion

This capstone demonstrates:
	•	A complete YOLOv8 detection pipeline
	•	Data science applied to real-world Tesla fatal crash data
	•	Clean, reproducible analysis
	•	A strong blend of deep learning and analytical safety investigation
