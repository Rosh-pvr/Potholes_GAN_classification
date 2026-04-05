
# 🛣️ Pothole-Guard: Metric-Aware Semantic Segmentation & Severity Assessment

[![Colab](https://img.shields.io/badge/Colab-Run%20Notebook-orange?logo=googlecolab)](https://colab.research.google.com/) 
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![YOLOv9](https://img.shields.io/badge/YOLOv9-GELANC-blue)](https://github.com/WongKinYiu/yolov9)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end computer vision pipeline designed for real-time infrastructure monitoring. This project integrates **Relativistic GANs**, **SegFormer-B4**, and **YOLOv9** with a **Mamdani Fuzzy Inference System** to not only detect potholes but physically measure them for maintenance prioritization.

---

## 🚀 Key Performance Benchmarks
* **Accuracy:** `99.14%` across diverse datasets (Japan & China).
* **mAP@0.5:** `99.23%` for high-precision localization.
* **Training Efficiency:** `1.07 Hours` (Optimized with AMP & RaGAN).
* **Output:** Actionable maintenance recommendations (Crack Sealing vs. Reconstruction).

---

## 🏗️ The 5-Phase Architecture

### 🛡️ Phase 1: Environment & Data Supply
* **Multi-Source Data:** Integration of Japan CV, POTHOLEV3, and Kaggle v2-2022 datasets (~9,862 images).
* **Strategic Partitioning:** 70:10:20 split to ensure unbiased testing on raw, unenhanced data.
* **Task-Aware Augmentation:** Specialized Salt-and-Pepper and ColorJitter to simulate adverse road conditions.

### ⚡ Phase 2: GAN-Based Preprocessing
* **Relativistic average GAN ($D_{Ra}$):** High-fidelity image restoration for low-quality infrastructure captures.
* **Optimization:** 200-epoch training loop utilizing **Automatic Mixed Precision (AMP)** for maximum GPU throughput.

### 🎯 Phase 3: Metric-Aware Segmentation
* **SegFormer-B4:** Leveraging a hierarchical transformer encoder for multi-scale feature extraction.
* **Boundary Precision:** Fine-tuning on enhanced data to extract the precise pixel-radius ($R_{ops}$).

### 📏 Phase 4: Object Detection & Physical Extraction
* **YOLOv9 (GELAN-C):** State-of-the-art localization providing programmable gradient information (PGI).
* **MiDaS Depth Mapping:** Relative depth estimation to distinguish surface distance ($DoPSFE$) from cavity depth ($DoPDP$).
* **Physical Formulas:**
    * $PD_{rms} = R_{ops} \times HZ_{scale}$ (Diameter)
    * $Potholedth = DoPSFE - DoPDP$ (Depth)

### 🧠 Phase 5: Fuzzy Logic Severity Engine
* **Inference Engine:** Mamdani FIS that handles real-world measurement uncertainty.
* **Decision Logic:** Categorizes severity into **Low, Medium, or High** to recommend repair actions (e.g., "Patching Work").

---

## 🛠️ Tech Stack
| Component | Technology |
| :--- | :--- |
| **Deep Learning** | PyTorch, torchvision |
| **Architectures** | YOLOv9, SegFormer-B4, MiDaS, Relativistic GAN |
| **Fuzzy Logic** | scikit-fuzzy |
| **Preprocessing** | OpenCV, PIL, NumPy |
| **Data Engine** | Roboflow API |

---

## 📋 Installation & Usage

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/yourusername/Pothole-Guard.git
    ```
2.  **Run in Google Colab**
    * Open `Realtime_POC_potholes.ipynb` in Colab.
    * Ensure Hardware Accelerator is set to **T4 GPU**.
    * Mount Google Drive and set up the `/Pothole_Project/checkpoints` directory.
3.  **Execute the Pipeline**
    * Run **Phase 1** to pull data.
    * Run **Phase 2** for the 200-epoch GAN enhancement.
    * Run **Phase 3-5** for inference and report generation.

---

## 📊 Maintenance Guidelines (Table 1)
| Severity | Diameter | Depth | Action |
| :--- | :--- | :--- | :--- |
| **Low** | 10–15 cm | 10–20 mm | Crack Sealing |
| **Medium** | 15–40 cm | 20–35 mm | Patching Work |
| **High** | 45+ cm | 35+ mm | Patching & Reconstruction |

---

## 📜 Research Reference
This implementation is based on the research paper: 
*"Real-time Pothole Measurement and Severity Assessment using Relativistic GAN and SegFormer-B4"* (2026).

---


