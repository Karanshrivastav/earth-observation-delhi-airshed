# 🌍 Earth Observation AI Audit — Delhi Airshed 🌫️

## 🧭 Problem Statement

The **Ministry of Environment** has initiated an AI-based audit of the **Delhi Airshed** to identify **land use patterns** and potential **pollution sources**. The objective is to process satellite imagery and land cover data using spatial reasoning, data filtering, and supervised classification techniques.

You are provided with:
- **Shapefiles** of Delhi-NCR and Delhi-Airshed (EPSG:4326)
- **ESA WorldCover 2021** land cover raster (`land_cover.tif`, 10m resolution)
- **Sentinel-2 RGB image patches** (128×128 pixels, 10m/pixel)
- **Center coordinates** for each image patch

---

## 🧱 Directory Structure

```
project-root/
├── data/
│   ├── rgb/                         # Sentinel-2 image patches
│   ├── shapefiles/                 # GeoJSON shapefiles
│   └── tif/                        # land_cover.tif
├── notebooks/
│   ├── 01_spatial_analysis.ipynb
│   ├── 02_data_preparation.ipynb
│   └── 03_model_training.ipynb
├── outputs/
│   ├── figures/
│   │   ├── grid_overlay.png
│   │   ├── interactive_grid.html
│   │   ├── grid.geojson
│   │   ├── grid_centers.geojson
│   │   ├── class_distribution.png
│   │   ├── confusion_matrix.png
│   │   ├── f1_comparison.png
│   │   ├── sample_patch.png
│   │   ├── 5_correct_predictions.png
│   │   ├── 5_incorrect_prediction.png
│   │   ├── correct_predictions.png
│   │   └── incorrect_predictions.png
│   ├── models/
│   │   └── resnet18_model.pth
│   └── reports/
│       ├── filtered_images.geojson
│       ├── labeled_images.geojson
│       └── training_results.csv
├── requirements.txt
└── README.md
```

---

## ✅ Solution Breakdown

### 🔹 Q1: Spatial Reasoning & Data Filtering (5 Marks)

**Goal:** Overlay 60×60 km grid over Delhi-NCR, filter RGB images by spatial location.

📓 Notebook: [`01_spatial_analysis.ipynb`](notebooks/01_spatial_analysis.ipynb)  
📈 Outputs:
- 🗺️ [Grid Overlay (PNG)](outputs/figures/grid_overlay.png)
- 🌐 [Interactive Grid (HTML)](outputs/figures/interactive_grid.html)
- 🗂️ [Filtered Images GeoJSON](outputs/reports/filtered_images.geojson)
- 🗂️ [Grid Cells (GeoJSON)](outputs/figures/grid.geojson)
- 🗂️ [Grid Centers (GeoJSON)](outputs/figures/grid_centers.geojson)

**Steps Addressed:**
- Plotted Delhi-NCR shapefile with 60x60 km UTM grid.
- Overlaid on satellite basemap using `geemap`.
- Marked grid cell corners and centers.
- Filtered image files based on center location.
- Reported number of images before and after filtering.

---

### 🔹 Q2: Label Construction & Dataset Preparation (10 Marks)

**Goal:** Assign ESA land cover labels to image patches using mode of 128×128 land_cover.tif regions.

📓 Notebook: [`02_data_preparation.ipynb`](notebooks/02_data_preparation.ipynb)  
📈 Outputs:
- 📊 [Class Distribution Plot](outputs/figures/class_distribution.png)
- 🗂️ [Labeled Images GeoJSON](outputs/reports/labeled_images.geojson)
- 🖼️ [Sample Patch](outputs/figures/sample_patch.png)

**Steps Addressed:**
- Extracted 128×128 land cover patches using `rasterio`.
- Assigned class using most frequent ESA land cover label.
- Mapped ESA class codes to 11 meaningful labels.
- Discussed edge cases (e.g., mixed classes, no-data).
- Performed 60/40 train-test split.
- Visualized class distribution and noted imbalances.

---

### 🔹 Q3: Model Training & Evaluation (10 Marks)

**Goal:** Train a CNN model (ResNet18) and evaluate land cover classification accuracy.

📓 Notebook: [`03_model_training.ipynb`](notebooks/03_model_training.ipynb)  
📈 Outputs:
- 📉 [Confusion Matrix](outputs/figures/confusion_matrix.png)
- 📈 [F1 Score Comparison](outputs/figures/f1_comparison.png)
- ✅ [Correct Predictions](outputs/figures/5_correct_predictions.png)
- ❌ [Incorrect Predictions](outputs/figures/5_incorrect_prediction.png)
- 📦 [Saved Model (.pth)](outputs/models/resnet18_model.pth)
- 📊 [Training Results CSV](outputs/reports/training_results.csv)

**Steps Addressed:**
- Trained a ResNet18 CNN on the labeled dataset.
- Evaluated using custom F1-score and `torchmetrics.F1Score`.
- Plotted confusion matrix and F1 score comparison.
- Showcased 5 correct and 5 incorrect predictions with RGB samples.

---

## 🧪 Environment Setup

Install the required packages:

```bash
pip install -r requirements.txt
```

Make sure you have the following:
- `geopandas`, `rasterio`, `matplotlib`, `torch`, `torchvision`, `torchmetrics`, `scikit-learn`, `geemap`

---

## 📌 Conclusion

This project presents a scalable approach to auditing land use and pollution sources using Sentinel-2 and ESA WorldCover datasets for Delhi NCR. The trained model can now assist in detecting land cover changes and help support environmental planning and mitigation efforts.

---

## 📬 Contact

For questions, feel free to contact **Karan Shrivastava**  
✉️ Email: karanshrivastava00@gmail.com  
🔗 GitHub: [https://github.com/Karanshrivastav](https://github.com/Karanshrivastav)
