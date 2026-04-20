# Optimal Battery Health Estimation using SVMD with CNN-BiGRU Hybrid Architecture

> **Pasala Varshitha** — PG Scholar, Department of Computer Science, Christ University, Bengaluru, India  
> **Vijay Babu Pamshetti** — Singapore Institute of Technology, Singapore

---

## Overview

This repository contains the research and implementation of a novel hybrid deep learning model for **State of Health (SOH) estimation** of lithium-ion batteries. The proposed architecture integrates:

- **SVMD** — Self-adaptive Variational Mode Decomposition for signal preprocessing
- **CNN** — Convolutional Neural Network for spatial/local degradation feature extraction
- **BiGRU** — Bidirectional Gated Recurrent Unit for capturing temporal dependencies across charge-discharge cycles

The model targets applications in **electric vehicles (EVs)**, **renewable energy grids**, and **portable electronics**.

---

## Abstract

Accurate battery health estimation is essential to ensure the reliability, safety, and efficiency of modern energy storage systems. Traditional electrochemical models often fail to represent complex, nonlinear degradation processes. This paper proposes a novel hybrid deep learning model integrating SVMD, CNN, and BiGRU for optimal battery SOH estimation.

Unlike conventional VMD, SVMD adaptively determines the number of modes (*K*) and balancing parameter (*α*) without manual tuning. CNN extracts spatial and local degradation patterns, while BiGRU captures bidirectional temporal dependencies. Experimental results demonstrate that the proposed SVMD-CNN-BiGRU model outperforms traditional VMD-based and standalone deep learning models.

**Keywords:** Battery Health Estimation, SVMD, CNN, BiGRU, Hybrid Deep Learning, State of Health (SOH), Energy Storage Systems, Adaptive Decomposition

---

## Methodology

### 1. Successive Variational Mode Decomposition (SVMD)
SVMD extracts intrinsic mode functions (IMFs) one at a time from the battery discharge voltage signal by solving a successive variational optimization problem. It adaptively determines decomposition parameters based on residual energy distribution, eliminating the need for manual tuning of *K* and *α*.

### 2. Spatial Feature Extraction (CNN)
1D convolutional layers with dilated filters detect local degradation patterns (voltage plateaus, inflection points, capacity shifts) at multiple temporal scales. Pooling layers compress local features while preserving essential temporal correlations.

### 3. Temporal Modeling (BiGRU)
BiGRU processes CNN feature maps with two parallel GRU layers — one advancing forward through cycles and one in reverse — to capture both historical degradation trends and future context. This bidirectional awareness significantly outperforms unidirectional RNN approaches.

### 4. Training & Evaluation
| Split | Proportion |
|-------|-----------|
| Training | 70% |
| Validation | 15% |
| Testing | 15% |

A **cross-dataset rotation strategy** is used: batteries B0005, B0006, B0007, and B0018 are rotated as the held-out test set to ensure generalization across different degradation patterns.

---

## Dataset

**NASA PCoE Lithium-Ion Battery Aging Dataset**  
- Battery cells: B0005, B0006, B0007, B0018 (commercial 18650 Li-ion cells)
- Nominal voltage: 3.7 V | Max charge: 4.2 V | Discharge cut-off: 2.7–3.0 V
- Measurements: voltage, current, temperature, time, capacity
- Cycles: 90–250+ complete charge-discharge cycles per cell
- Protocols: CC-CV charging; constant, pulsed, and randomized discharge loads

---

## Results

### Performance Comparison (SOH Prediction)

| Model | Dataset | MAE | RMSE | R² |
|-------|---------|-----|------|-----|
| CNN-LSTM | B0007 | 0.0030 | 0.0030 | 0.9985 |
| CNN-BiLSTM | B0007 | 0.0021 | 0.0031 | 0.9984 |
| CNN-GRU | B0007 | 0.0024 | 0.0033 | 0.9982 |
| **CNN-BiGRU (Proposed)** | **B0007** | **0.0016** | **0.0022** | **0.9997** |
| CNN | B0007 | 0.0018 | 0.0027 | 0.9987 |
| LSTM | B0007 | 0.0021 | 0.0031 | 0.9983 |
| GRU | B0007 | 0.0022 | 0.0031 | 0.9983 |

### Model Size Comparison

| Model | Parameters |
|-------|-----------|
| CNN | 69,252 |
| GRU | 59,777 |
| LSTM | 76,419 |
| CNN-GRU | 255,620 |
| CNN-LSTM | 164,545 |
| CNN-BiLSTM | 312,321 |
| **CNN-BiGRU (Proposed)** | **477,700** |

The CNN-BiGRU model achieves the best accuracy across all tested battery cells, with an R² of **0.9997** and MAE as low as **0.0016** on the B0007 cell.

---

## Key Contributions

- Adaptive signal decomposition via SVMD, eliminating manual hyperparameter tuning
- Hybrid CNN-BiGRU architecture combining spatial and bidirectional temporal learning
- State-of-the-art SOH estimation on NASA benchmark datasets
- Cross-dataset generalization across diverse degradation conditions

---

## References

Key references include:
- Nazari & Sakhaei (2020) — Successive Variational Mode Decomposition
- Dragomiretskiy & Zosso (2014) — Variational Mode Decomposition
- Chung et al. (2014) — Empirical Evaluation of Gated Recurrent Neural Networks
- Pamshetti et al. (2025) — Optimal Signal Decomposition-based Multi-Stage Learning for Battery Health Estimation

See the full paper for the complete reference list.

---

## Citation

If you use this work, please cite:

```
Pasala Varshitha, Vijay Babu Pamshetti,
"Optimal Battery Health Estimation using SVMD with CNN-BiGRU Hybrid Architecture",
2025.
```

---

## Contact

- **Pasala Varshitha** — pasala.varshitha@msam.christuniversity.in  
- **Vijay Babu Pamshetti** — vijaybabu.pamshetti@singaporetech.edu.sg
