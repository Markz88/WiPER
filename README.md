# Wi-PER81: A Benchmark Dataset for Wi-Fi Signal Image-based Person Re-Identification

This repository accompanies the paper:

> **A Benchmark Dataset for Radio Signal Image-based Person Re-Identification**  
> Marco Cascio, Luigi Cinque, Damiano Distante, Gian Luca Foresti, Alessio Fagioli  
> [DOI and publication details to be inserted here]

Wi-PER81 is a pioneering dataset and benchmark for Wi-Fi-based person re-identification (Re-ID). It provides a complete pipeline from raw Channel State Information (CSI) signal processing to deep learning benchmarking using image-based radio signatures.

---

## 🔍 Overview

Wi-Fi sensing enables privacy-preserving alternatives to camera-based Re-ID by exploiting the amplitude characteristics of wireless signals. Wi-PER81 captures CSI data from **81 individuals** across **two acquisition sessions**, amounting to **162,000 packets**. This dataset supports deep learning models trained on **signal magnitude heatmaps** for person Re-ID in realistic, noisy environments.

---

## 📁 Repository Structure

This repo contains three core Jupyter notebooks:

### 1. `WiPER-DataProcessing.ipynb`
Processes raw CSI to generate sanitized amplitude values:
- Builds CSI matrices from raw data.
- Applies Hampel, Z-score, and **IQR filtering** (recommended).
- Visualizes raw and sanitized amplitude values and heatmaps for the specified ID.

### 2. `WiPER-DatasetGeneration.ipynb`
Generates image-based datasets:
- Splits data into training (D1), validation (D2v), and test (D2t) sets.
- Converts sanitized amplitudes into **signal magnitude heatmaps**.
- Organizes probe/gallery pairs for benchmarking.

### 3. `WiPER-Benchmarking.ipynb`
Benchmarks deep learning models:
- Implements a **Siamese-like neural architecture** for person Re-ID.
- Tests multiple CNN backbones described in the WiPER81 paper.
- Computes standard Re-ID metrics (e.g., Rank-1, Rank-5, Rank-10, mAP).

---

## 🗂️ Wi-PER81 Dataset Structure

The ready-to-use Wi-PER81 dataset—comprising CSI measurements, raw and sanitized amplitude values, and corresponding signal magnitude heatmaps—is available in the output folder of this `repository` or on Figshare: https://doi.org/10.6084/m9.figshare.26984497.

### CSV Folders:
- `CSV/csi_matrices/`: Raw CSI values
- `CSV/raw_amplitudes/`: Extracted raw amplitudes
- `CSV/sanitized_amplitudes/IQR_amplitudes/`: Amplitudes filtered using the IQR method
- `CSV/sanitized_amplitudes/HF_amplitudes/`: Amplitudes filtered using the Hampel Filter
- `CSV/sanitized_amplitudes/zscore_amplitudes/`: Amplitudes filtered using the Z-score method

### Image Folders:
- `ImageData/D1/`: Training set (session A)
- `ImageData/D2v/`: Validation set (session B)
- `ImageData/D2t/`: Test set (session B)

Each identity has 10 signal magnitude heatmaps per session, generated from groups of 100 packets.

---

## 📊 Benchmark Results

| Model               | Rank #1 | Rank #5 | Rank #10 | mAP     | Test Time | Params |
|-------------------- |---------|---------|----------|---------|-----------|--------|
| VGG16               | 55.967% | 76.955% | 83.951%  | 76.680% | 9'06"     | 17.4M  |
| VGG19               | 48.971% | 75.309% | 85.597%  | 79.595% | 9'55"     | 22.7M  |
| DenseNet121         | 83.128% | 95.473% | 96.708%  | 65.364% | 6'57"     | 12.3M  |
| EfficientNetB0      | 63.786% | 83.951% | 92.181%  | 64.324% | 5'09"     | 11.9M  |
| MobileNetV3         | 41.564% | 67.078% | 75.720%  | 82.682% | 4'14"     | 4.5M   |
|---------------------|---------|---------|----------|---------|-----------|--------|
| Baseline            | 45.679% | 73.663% | 82.716%  | 80.967% | 4'21"     | 22.6M  |
| Baseline w/ dropout | 75.720% | 93.004% | 94.650%  | 68.450% | 4'31"     | 22.6M  |

DenseNet121 achieved the best accuracy. The dropout-enhanced baseline provided a strong speed-accuracy tradeoff.

> 🧪 To reproduce these results, use the **final code snippet in `WiPER-Benchmarking.ipynb`**, skipping the training and performance evaluation cells. This snippet loads the pre-trained weights and evaluates the models directly on the provided test set `D2t` (adjust the path if necessary).

---

## 📦 Installation

Install dependencies with:

```bash
pip install -r requirements.txt
```

---

## 📜 Citation

Please cite the following paper if you use this code or dataset:

```bibtex
@article{cascio2025wiper81,
  title={A Benchmark Dataset for Radio Signal Image-based Person Re-Identification},
  author={Cascio, Marco and others},
  journal={Scientific Data},
  year={2025}
}
```

---

## 📎 License
Released under the MIT License. See LICENSE for details.