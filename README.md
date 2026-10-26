# 🌍 Sentinel-2 Land Type Classification

> **3rd place** out of all teams in the DEPI national Data Science track (Round 3)

An automated, high-accuracy deep learning system for classifying land cover types 
using multispectral satellite imagery from the European Space Agency's Sentinel-2 
mission.

---

## 🏆 Results

| Metric | Value |
|--------|-------|
| Test Accuracy | **97.12%** |
| Validation Accuracy | **97.00%** |
| Dataset | EuroSAT (20,000 images, 10 classes) |
| Final Model | EfficientNet-B0 (PyTorch) |
| Deployment | Flask REST API |

---

## 📌 Overview

The system classifies satellite images into 10 land cover types:
Annual Crop, Forest, Herbaceous Vegetation, Highway, Industrial,
Pasture, Permanent Crop, Residential, River, Sea/Lake.

Built for critical real-world applications including smart urban planning, 
environmental monitoring, resource management, and disaster response.

---

## 🔬 Methodology

### 1. Data Preprocessing
- Resized all images to EfficientNet-B0 input dimensions
- Applied atmospheric correction and pixel normalization across all 13 spectral bands
- Data split: 70% training / 15% validation / 15% test
- Augmentation on training set: rotations, horizontal/vertical flips, cropping

### 2. Baseline — Traditional ML
Before deep learning, 5 traditional models were benchmarked using 
manually engineered features (NDVI, spectral band statistics):

| Model | Accuracy |
|-------|----------|
| Random Forest | 0.813 |
| SVM | 0.776 |
| KNN | 0.757 |
| Decision Tree | 0.694 |
| Logistic Regression | 0.631 |

### 3. Deep Learning — Model Selection
Two CNN architectures tested:
- **ResNet-50** — strong baseline using skip connections
- **EfficientNet-B0** ✅ — selected for best accuracy/efficiency ratio via 
compound scaling of depth, width, and resolution

### 4. Training Strategy
- Transfer learning using ImageNet pretrained weights
- Fine-tuned top layers for EuroSAT classification task
- Adam optimizer with hyperparameter tuning (learning rate, batch size)
- Early stopping based on validation loss
- Dropout layers for overfitting prevention

---

## 🚀 Deployment

For the final demo, the trained model was served as a REST API with Flask,
with a web page where users upload a satellite image and get the land class back.
(The deployment code is not part of this repository.)

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| Deep Learning | PyTorch, EfficientNet-B0 |
| Data Handling | NumPy, Pandas |
| Image Processing | Torchvision, PIL, OpenCV |
| Visualization | Matplotlib, Seaborn |
| Deployment | Flask |

---

## ⚙️ How to Run

1. Clone the repository
```bash
git clone https://github.com/Tadrous-William/sentinel2-land-classification.git
cd sentinel2-land-classification
```

2. Install the packages
```bash
pip install torch torchvision pandas scikit-learn matplotlib seaborn pillow tqdm jupyter
```

3. Open the final notebook (it downloads EuroSAT through `torchvision.datasets`)
```bash
jupyter notebook "Final Notebook.ipynb"
```

## 📂 What's in the repo

| Path | Contents |
|---|---|
| `Final Notebook.ipynb` | Full pipeline: data loading, training, evaluation |
| `overview.ipynb` | Dataset overview |
| `Class_Notebooks/` | One EDA notebook per land class |
| `Final Folder DEPI/` | Preprocessing and model-testing notebooks, report, documentation and presentation |
| `Final Project Proposal.pdf` | Original project proposal |

---

## 👥 Team

| Name | Role |
|------|------|
| **Tadrous Adel William** (Leader) | Project management, Flask deployment, final integration |
| Maria Ashraf Haleem | Data preprocessing pipeline, augmentation |
| Abd-elaziz Hassan Fouad | Custom CNN baseline, evaluation metrics |
| Karen Medhat Zaher | EDA, spectral band analysis, model selection |
| Mohamed Essam | EfficientNet-B0 training, hyperparameter tuning |
| Mohamed Kamal | Documentation, presentation |

---

## 🔮 Future Work

- Integrate Landsat and SAR data for cloud-cover robustness
- Experiment with Vision Transformers (ViT)
- Migrate to AWS Lambda / Azure Functions with Docker containerization
