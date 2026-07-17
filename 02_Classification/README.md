<div align="center">
<img src="https://img.shields.io/badge/Module-02_Classification-6B8F71?style=for-the-badge" />
<img src="https://img.shields.io/badge/status-in_progress-87A96B?style=flat-square" />
<img src="https://img.shields.io/badge/part_of-Portfolio_Projects--Machine_Learning-4A5D45?style=flat-square" />
</div>
<br/>

# 🧮 Classification

This module covers classification algorithms — predicting discrete class labels from input features. Each notebook builds on the last, moving from simple binary classifiers to probabilistic, margin-based, and ensemble approaches.

Part of the [**Portfolio Projects - Machine Learning**](../) repository.

<br/>

## 📂 Contents

| # | Notebook | Concept Covered |
|---|---|---|
| 1 | `01_sms_spam_classifier.ipynb` | Text preprocessing, TF-IDF, Naive Bayes for binary classification |
| 2 | `02_logistic_regression.ipynb` | Sigmoid function, decision boundary, log loss |
| 3 | `03_knn_classifier.ipynb` | Distance metrics, choosing k, curse of dimensionality |
| 4 | `04_decision_tree_classifier.ipynb` | Entropy, Gini impurity, tree pruning |
| 5 | `05_svm_classifier.ipynb` | Margin maximization, kernel trick |
| 6 | `06_naive_bayes.ipynb` | Bayes' theorem, conditional independence assumption |
| 7 | `07_evaluation_metrics.ipynb` | Confusion matrix, precision, recall, F1, ROC-AUC |

> ✏️ Rename/reorder the rows above to match your actual notebook filenames.

<br/>

## 🧠 Key Concepts

- **Decision Boundaries** — linear vs non-linear separation of classes
- **Probabilistic vs Discriminative Models** — Naive Bayes/Logistic Regression vs SVM/Decision Trees
- **Class Imbalance** — why accuracy alone is misleading, and how precision/recall/F1 correct for it
- **Confusion Matrix** — true/false positives & negatives, and their real-world cost tradeoffs
- **Bias-Variance Tradeoff** — underfitting vs overfitting in classifiers (e.g. tree depth, k in KNN)
- **Feature Engineering for Text** — Bag of Words, TF-IDF, stemming/lemmatization

<br/>

## 🛠️ Tech Stack

<div align="center">

![Python](https://img.shields.io/badge/Python-4A5D45?style=for-the-badge&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-6B8F71?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-87A96B?style=for-the-badge&logo=pandas&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-4A5D45?style=for-the-badge&logo=scikitlearn&logoColor=white)
![NLTK](https://img.shields.io/badge/NLTK-6B8F71?style=for-the-badge&logo=python&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-87A96B?style=for-the-badge&logo=plotly&logoColor=white)

</div>

<br/>

## 🚀 How to Run

```bash
# From the repo root
cd 02_Classification

# Install dependencies (if not already installed at repo root)
pip install numpy pandas scikit-learn nltk matplotlib jupyter

# Launch notebooks
jupyter notebook
```

<br/>

## 📊 Results Summary

| Model | Dataset | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|---|
| Email Spam Classifier (Naive Bayes) | _dataset name_ | _—_ | _—_ | _—_ | _—_ |
| Logistic Regression | _dataset name_ | _—_ | _—_ | _—_ | _—_ |
| KNN Classifier | _dataset name_ | _—_ | _—_ | _—_ | _—_ |
| Decision Tree | _dataset name_ | _—_ | _—_ | _—_ | _—_ |
| SVM | _dataset name_ | _—_ | _—_ | _—_ | _—_ |

> ✏️ Fill in your actual scores once notebooks are finalized — this table is the fastest way for a reviewer to judge your results without opening every notebook. For imbalanced datasets (like spam detection), lead with precision/F1 over raw accuracy.

<br/>

## 📌 Notes

- Datasets used are sourced from [add source, e.g. Kaggle / UCI ML Repository / sklearn built-in datasets]
- Each notebook includes EDA, preprocessing, model training, and evaluation sections
- Text-based notebooks (e.g. spam classifier) include an additional NLP preprocessing stage: lowercasing → tokenization → stopword removal → stemming → vectorization

<br/>

<div align="center">
<i>⬅️ Back to <a href="../">Portfolio Projects - Machine Learning</a></i>
</div>
