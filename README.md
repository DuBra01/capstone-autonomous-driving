# capstone-autonomous-driving
# 🚗🧠 Autonomous Driving Capstone

This repository contains my capstone project on **autonomous driving**, implemented in a single Jupyter Notebook:

- **`Autonomous_Driving.ipynb`**

> GitHub profile: [@DuBra01](https://github.com/DuBra01)

---

## 🧩 Project Overview

This project has **two main parts**:

1. **Part 1 – Vehicle Detection with YOLOv8**
2. **Part 2 – Exploratory Data Analysis (EDA) on Tesla Fatal Crash Data**

The goal is to combine **computer vision** and **data analysis** to study risks and patterns related to autonomous driving and Tesla vehicles.

---

## 🔹 Part 1 – YOLOv8 Vehicle Detection

In this part, I worked with a dataset of road images containing vehicles of multiple types (cars, buses, trucks, motorcycles, etc.) and trained custom YOLOv8 models.

### Main steps

- **Data preparation**
  - Unzipped and organized raw images into a clean folder structure.
  - Loaded a large `labels.csv` and filtered it to keep only rows that correspond to the available images.
  - Standardized annotation format (image name, class, bounding box coordinates).

- **Annotation standardization**
  - Converted bounding boxes from `(xmin, ymin, xmax, ymax)` pixel format into **YOLO format** `(class_id, x_center, y_center, width, height)` normalized by image size.
  - Saved standardized annotations for reuse.

- **Train / Validation / Test split**
  - Created **stratified splits**, preserving the class distribution across:
    - `train/`
    - `val/`
    - `test/`

- **Model training**
  - Trained **YOLOv8n (nano)** as a fast baseline:
    - Partial backbone freeze.
    - ~25 epochs.
  - Then trained **YOLOv8s (small)** for better accuracy:
    - Pretrained COCO backbone.
    - First 10 layers frozen (transfer learning).
    - Cosine learning rate schedule.
    - AdamW optimizer.
    - ~20 epochs.

- **Evaluation**
  - Evaluated both models and compared:
    - **mAP@0.50 (mAP50)**  
    - **mAP@0.50:0.95 (mAP50–95)**  
    - Precision & recall.
    - Per-class AP (for cars, buses, trucks, pedestrians, cyclists, etc.).
  - Generated:
    - PR curves.
    - Confusion matrix.
    - Example predictions on **test images** and a few **external images from the web**.

### Final result (YOLOv8s, partial freeze, img 640)

- **Validation performance (val set)**  
  - `mAP50` ≈ **0.59**  
  - `mAP50–95` ≈ **0.41**  
  - Good performance especially on:
    - **Car, bus, pickup_truck**, and **bicycle** classes.
  - Lower but usable performance on rare classes like:
    - `non-motorized_vehicle`, `single_unit_truck`, etc.

- **Test performance (held-out test set)**  
  - `mAP50` ≈ **0.59**  
  - `mAP50–95` ≈ **0.40**  
  - Per-class test AP highlights:
    - Strong for **car**, **bus**, **pickup_truck**, **bicycle**.
    - Weaker for very rare categories and pedestrians in complex scenes.

> Overall, YOLOv8s with partial backbone freezing gave the best trade-off between speed and accuracy within the available compute.

---

## 🔹 Part 2 – Tesla Fatal Crash EDA

In this part, I analyze a CSV dataset of **Tesla-related fatal accidents**, including fields such as date, country, state, number of deaths, model, and whether Autopilot was involved.

### Data cleaning

- Loaded the original dataset (`Tesla - Deaths.csv`).
- Performed:
  - Type inspection.
  - Missing value analysis.
  - Duplicate removal (4 duplicate rows found and removed).
- Removed columns with extremely sparse or non-analytical content (e.g., individual deceased names, very sparse notes).
- Saved a cleaned version for analysis.

### Time and geography analysis

- **By year**:
  - Count of fatal events per year.
  - Noted **increasing trends** over time (also influenced by growing Tesla fleet size and adoption).
- **By country and state**:
  - Aggregated events by **country** (USA dominating the counts).
  - Within the USA, explored **state-level** patterns.
  - Created bar charts and rankings for top states.

### Event characteristics

For each accident, I analyzed:

- **Number of deaths per event**  
  - Most events involve **1 death**.
  - A smaller number involve **2+ fatalities**.

- **Tesla driver fatalities**  
  - Counted how many events included a death of the **Tesla driver**.

- **Tesla occupant fatalities**  
  - Calculated proportion of events where **Tesla occupants** (driver and/or passengers) died.

- **Cyclists / pedestrians involvement**  
  - Filtered events where the vehicle hit a **cyclist or pedestrian**.
  - Studied their distribution and proportion of total events.

- **Combined Tesla + vulnerable road users**  
  - Isolated cases where **both**:
    - A Tesla driver or occupant died, **and**
    - A cyclist or pedestrian died.
  - These events are especially critical from a safety and policy point of view.

- **Collisions with other vehicles**
  - Counted events where crashes involved **other vehicles** (multi-vehicle accidents).

### Model- and Autopilot-focused analysis

- **By Tesla model**:
  - Grouped events by `Model` (e.g., Model S, Model 3, Model X, Model Y, unknown).
  - Looked at the **event counts per model**.

- **Autopilot-related vs non-Autopilot**:
  - Cleaned the `Autopilot claimed` column into a binary flag.
  - Counted:
    - Events with Autopilot **reported or claimed**.
    - Events without Autopilot involvement.
  - Compared **Autopilot vs non-Autopilot accidents per model**, using grouped bar charts.

---

## 🧪 How to Run This Project

> This repository is designed around a **single notebook workflow** for easy reproduction.
