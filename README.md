# EMG-Gesture-Recognition-Analysis

## Background
Electromyography (EMG) signals are widely used for hand gesture recognition in human–machine interaction and rehabilitation applications.  
One of the main challenges in EMG-based systems is **inter-subject variability**, meaning that signals recorded from different individuals can vary significantly even for the same gesture.

This project explores how well classical machine learning models generalize across subjects using a **cross-subject (LOSO)** evaluation strategy.

---

## Dataset
- **Dataset:** DB1 (NinaPro)
- **Subjects:** 7 (S1–S7)
- **Sessions:** A1, E1–E3
- **Sampling rate:** 200 Hz

Each subject is used once as the test set, while the remaining subjects are used for training.

---

## Methods

### Signal Processing
- Band-pass filtering: **20–45 Hz**
- Segmentation:
  - Window length: **200 ms**
  - Step size: **100 ms**

### Feature Extraction
Time-domain features were extracted from each EMG channel:
- Mean Absolute Value (MAV)
- Root Mean Square (RMS)
- Waveform Length (WL)
- Zero Crossing (ZC)

Total feature dimension: **40**

### Classification
The following classifiers were evaluated:
- Linear Discriminant Analysis (LDA)
- Linear Support Vector Machine (Linear SVM)
- Radial Basis Function Support Vector Machine (RBF SVM)

All features were standardized using **StandardScaler**.  
Evaluation was performed using **Leave-One-Subject-Out (LOSO)** cross-validation.

---

## Results

| Model | Average Accuracy | Std Dev |
|------|------------------|---------|
| LDA | 0.41 | 0.02 |
| **Linear SVM** | **0.42** | 0.02 |
| RBF SVM | 0.42 | 0.02 |

![Accuracy Comparison](img/results_accuracy.png)

---

## Confusion Matrix
An example confusion matrix for **Subject S1 using LDA** is shown below:

![Confusion Matrix](img/confusion_matrix_S1.png)

---

## Discussion
Although RBF SVM is a more complex model, it did not consistently outperform linear classifiers in the cross-subject setting.  
This suggests that **inter-subject variability in EMG signals is a dominant factor**, and increasing model complexity alone does not guarantee better generalization.

Linear SVM showed the most stable performance across subjects.

---

## Future Work
- Feature selection and channel reduction
- Frequency-domain and time–frequency features
- Domain adaptation and subject-invariant learning methods

---

## Run Online (Colab)
You can run the full pipeline and experiments in Google Colab:

[Open in Colab](https://colab.research.google.com/github/ali-mohamadpour/EMG-Gesture-Recognition-Analysis/blob/main/emg_cross_subject_classification.ipynb)

---

## File Structure
    ├── emg_cross_subject_classification.ipynb
    ├── emg_cross_subject_classification.py 
    ├── DB1/ 
    │     └── dataset files (.mat)             #https://ninapro.hevs.ch/instructions/DB1.html subject 1-7
    ├── img/    
    │     ├── results_accuracy.png
    │     └── confusion_matrix_S1.png               
    ├── LICENSE
    └── README.md
