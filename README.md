<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A0F1E,50:16255C,100:00897B&height=230&section=header&text=QMed&fontSize=78&fontColor=FFFFFF&fontAlignY=36&desc=Hybrid%20Quantum%20Machine%20Learning%20for%20Early%20Disease%20Detection&descSize=20&descAlignY=57&descColor=BFE7EF&animation=fadeIn" alt="QMed - Hybrid Quantum Machine Learning for Early Disease Detection" width="100%">
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=18&duration=3000&pause=900&color=22A7C2&center=true&vCenter=true&width=720&lines=Quantum+kernels+%C2%B7+Variational+circuits+%C2%B7+Hybrid+QNN;Leak-free+benchmarking+on+real+medical+data;5+datasets+%C2%B7+4+qubits+%C2%B7+nested+tuning+%C2%B7+paired+statistics" alt="Quantum kernels, variational circuits, leak-free benchmarking">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.13-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/PennyLane-0.45-6C2DC7" alt="PennyLane">
  <img src="https://img.shields.io/badge/scikit--learn-1.6-F7931E?logo=scikitlearn&logoColor=white" alt="scikit-learn">
  <img src="https://img.shields.io/badge/PyTorch-ResNet--18-EE4C2C?logo=pytorch&logoColor=white" alt="PyTorch">
  <img src="https://img.shields.io/badge/Google%20Colab-notebooks-F9AB00?logo=googlecolab&logoColor=white" alt="Colab">
  <img src="https://img.shields.io/badge/qubits-4-00897B" alt="4 qubits">
  <img src="https://img.shields.io/badge/datasets-5-16255C" alt="5 datasets">
</p>

<p align="center">
  <b>Problem Statement SIH26139</b> · Egreen Quanta · MedTech / BioTech / HealthTech · Team <b>Dark-47</b>
</p>

---

## Overview

**QMed** is a hybrid quantum–classical machine learning platform for early disease detection. It asks a simple question that is often skipped: *when quantum and classical models are compared fairly, does a quantum kernel actually help on real medical data?*

To answer it, QMed puts quantum kernel classifiers, a variational quantum classifier and a hybrid quantum neural network side by side with tuned classical models on **five medical datasets** — clinical tables, cytology, gene expression and breast ultrasound images. Every preprocessing step is fitted inside each training fold, every kernel gets the same tuning budget, and every comparison is backed by paired statistical tests over repeated cross-validation.

The platform also studies *why* quantum kernels behave the way they do — through encoding bandwidth, kernel spectrum and geometric difference — and how sensitive medical machine learning results are to data leakage.

## At a glance

| | |
|---|---|
| **Quantum models** | QSVM with ZZ feature map (entangling), QSVM with angle encoding (classical control), VQC, hybrid QNN |
| **Classical models** | RBF-SVM, logistic regression, random forest, and all-feature baselines |
| **Datasets** | Cleveland heart disease · Pima diabetes · Wisconsin breast cytology · BreastMNIST ultrasound · Golub leukaemia |
| **Qubits** | 4 (one per principal component) |
| **Protocol** | 5 seeds × stratified 5-fold CV, identical folds for every model, nested tuning of *C* and bandwidth |
| **Statistics** | Corrected resampled *t*-test, TOST equivalence test (±0.02 AUC), Holm correction, 200-permutation label test |
| **Stack** | PennyLane, scikit-learn, imbalanced-learn, PyTorch / torchvision, NumPy, pandas, Matplotlib |

## How the platform works

1. **Data** — five public medical datasets. Ultrasound images are turned into 512 features by a frozen ImageNet-pretrained ResNet-18 that never sees the labels.
2. **Leak-free preprocessing** — imputation → one-hot encoding and standardisation → ANOVA *F* feature selection (*k* = 10) → PCA to 4 components → min–max scaling to rotation angles [0, α] → SMOTE. All of it is refitted inside the training part of every fold.
3. **Models** — quantum and classical models receive exactly the same four inputs.
4. **Nested tuning** — an inner 3-fold CV picks *C* ∈ {0.1, 1, 10} and the bandwidth (α ∈ {π/8, π/4, π/2} for quantum kernels, γ ∈ {¼, 1, 4} × default for RBF).
5. **Evaluation** — held-out ROC-AUC, accuracy, sensitivity, specificity, Brier score and train–validation gap, followed by paired statistical testing.
6. **Mechanism and validity** — bandwidth sweep, kernel spectrum, geometric difference, noise simulation, learning curves, permutation tests and a leakage demonstration.

### Quantum feature maps

The **angle encoding** applies one *R<sub>Y</sub>* rotation per qubit and gives a product state whose kernel can be written in closed form — a built-in classical control. The **ZZ feature map** adds Hadamard layers and nearest-neighbour entangling blocks, repeated twice, and is the main quantum model. The fidelity kernel *K*(*x*, *x′*) = |⟨φ(*x*)|φ(*x′*)⟩|² feeds a support vector machine.

## Repository contents

| Notebook | What it contains |
|---|---|
| `QMed_V1.ipynb` | First version of the platform: data pipeline, quantum models, benchmark and explainability |
| `QMed_Journal.ipynb` | Full multi-dataset benchmark with statistical testing, validity checks and publication figures |
| `QMed_Journal_V2.ipynb` | Final benchmark with nested bandwidth tuning, revised validity criteria and the complete result package |

## Datasets

| Dataset | Samples | Features | Task |
|---|:-:|:-:|---|
| Cleveland heart disease | 303 | 13 | Coronary artery disease |
| Pima diabetes | 768 | 8 | Diabetes onset |
| Wisconsin diagnostic breast cancer | 569 | 30 | Malignant vs benign mass |
| BreastMNIST (ultrasound) | 780 images | 512 (CNN features) | Malignant vs benign lesion |
| Golub leukaemia | 72 | 7,129 genes | ALL vs AML |

All datasets are public (UCI Machine Learning Repository, OpenML and MedMNIST).

## Author

**Md. Abu Sayem** · Manav Rachna International Institute of Research and Studies, Faridabad, India

---

<p align="center"><sub>Built with PennyLane, scikit-learn and PyTorch · Results will be added after publication</sub></p>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:00897B,50:16255C,100:0A0F1E&height=110&section=footer" alt="" width="100%">
</p>
