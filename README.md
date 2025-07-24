# NoiseRobustClassifier
This is a group project, which investigates noise-robust classifiers trained on image datasets with class-conditional label noise. The objective is to evaluate different methods to **mitigate the impact of noisy labels** and improve classification accuracy on clean test data.  

---

## 📦 Dataset

We used the three image datasets provided:

- `FashionMNIST0.5.npz`: with known transition matrix
- `FashionMNIST0.6.npz`: with known transition matrix
- `CIFAR.npz`: transition matrix unknown and to be estimated

Each dataset includes:
- Noisy training/validation labels: `Xtr_val`, `Str_val`
- Clean test labels: `Xts`, `Yts`

> **Note**: Due to privacy policy, the datasets are not included in this repository. Please place them manually under the `input_data/` directory.

---

## 🛠️ Methods Implemented

### ✅ 1. PCA + Random Forest (Ensemble Learning)
- Used PCA to reduce image feature dimensions.
- Trained a `RandomForestClassifier` on reduced data.
- Adjusted predictions using a known or estimated transition matrix.

### ✅ 2. CNN + Forward Correction
- Implemented simple CNN architectures for grayscale (FashionMNIST) and RGB (CIFAR) data.
- Applied **Forward Correction** by incorporating the label noise transition matrix into the loss function.
- Trained models to learn correct label distributions under noisy conditions.

---

## 📊 Experimental Results Summary
| Model         | Dataset             | Accuracy   | Precision | Recall | F1 Score |
| ------------- | ------------------- | ---------- | --------- | ------ | -------- |
| RF + PCA      | FashionMNIST0.5     | 0.5677     | 0.5674    | 0.5677 | 0.5672   |
| CNN + Forward | FashionMNIST0.5     | **0.8240** | 0.8524    | 0.8240 | 0.8191   |
| RF + PCA      | FashionMNIST0.6     | 0.4130     | 0.4153    | 0.4130 | 0.4115   |
| CNN + Forward | FashionMNIST0.6     | **0.7833** | 0.7848    | 0.7833 | 0.7799   |
| RF + PCA      | CIFAR (estimated T) | 0.3160     | 0.3125    | 0.3160 | 0.2627   |
| CNN + Forward | CIFAR (estimated T) | **0.4407** | 0.4200    | 0.4407 | 0.4144   |

---

## 🔭 Future Work & Improvements

To further improve noise robustness and generalization performance, the following strategies are suggested:

1. **Use deeper and pretrained CNN models**  
   Replace the basic CNN with more advanced architectures such as **ResNet**, **EfficientNet**, or **Vision Transformers**. These models offer stronger feature extraction and better robustness to complex noise.

2. **Explore advanced noise modeling techniques**  
   Incorporate methods such as:
   - **Co-teaching**: Train two models simultaneously, each filtering out noisy labels for the other.
   - **Gold Loss Correction (GLC)** or **CleanLab**: Automatically estimate and correct label noise using probabilistic modeling.
   - **DivideMix**: Use semi-supervised learning and Gaussian mixture modeling to separate clean and noisy labels.

3. **Leverage semi-supervised learning**  
   Apply techniques like **FixMatch**, **MixMatch**, or **pseudo-labeling** to make use of unlabeled or weakly-labeled data to reduce reliance on noisy labels.

4. **Self-supervised pretraining**  
   Use methods like **SimCLR**, **BYOL**, or **MoCo** to learn robust visual representations without labels, and fine-tune them on noisy datasets.

5. **Transfer learning**  
   Utilize pretrained models from clean datasets (e.g., ImageNet) and fine-tune on noisy data, benefiting from general visual features.

6. **Incorporate uncertainty modeling**  
   Introduce **Bayesian neural networks** or **Monte Carlo dropout** to estimate prediction confidence and identify mislabeled data.

7. **Improve transition matrix estimation**  
   Use better estimators such as anchor point methods, constrained optimization, or class-conditional probability smoothing to get more accurate noise transition matrices.

8. **Introduce adaptive sample reweighting**  
   Dynamically assign weights to samples during training based on prediction confidence or gradient norms to reduce the impact of noisy labels.

These future directions will help build more reliable and scalable machine learning systems, especially for real-world applications with imperfect data.

---

## ⚠️ Academic Integrity Notice

This repository contains code written for educational purposes.  

Please **do not copy** or reuse this work for academic submission in any course, as this may violate university academic honesty policies.  
You are welcome to use it as reference for personal learning, but not for plagiarism.
