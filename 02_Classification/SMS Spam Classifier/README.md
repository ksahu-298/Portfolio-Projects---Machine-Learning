<div align="center">
<img src="https://img.shields.io/badge/Project-SMS_Spam_Classifier-6B8F71?style=for-the-badge" />
<img src="https://img.shields.io/badge/status-complete-87A96B?style=flat-square" />
<img src="https://img.shields.io/badge/part_of-02_Classification-4A5D45?style=flat-square" />
</div>
<br/>

# 📩 SMS Spam Classifier

A binary text classifier that labels an incoming SMS/email message as **Spam** or **Ham (Not Spam)**. This is a classification problem — the target is a discrete label, not a continuous value — so the whole pipeline (features, model choice, evaluation metric) is built around that.

Part of the [**02_Classification**](../) module in [**Portfolio Projects - Machine Learning**](../../).

<br/>

## 🎯 Problem Statement

> Given the raw text of a message, predict whether it is **Spam (1)** or **Ham (0)**.

| Aspect | Detail |
|---|---|
| Task type | Binary Classification |
| Input | Raw message text (string) |
| Output | Label — `Spam` / `Ham` |
| Primary metric | **Precision** (minimize false positives) |
| Secondary metrics | Accuracy, Recall, F1-score, Confusion Matrix |

<br/>

## 🗂️ Dataset

- **Source:** [SMS Spam Collection Dataset (UCI / Kaggle)](https://archive.ics.uci.edu/dataset/228/sms+spam+collection)
- **Size:** 5,572 raw messages → 5,169 after removing duplicates
- **Columns:** `v1` (ham/spam label), `v2` (raw text) — renamed to `target` (label-encoded) and `text` during cleaning
- **Class distribution:** Imbalanced — 4,516 ham vs 653 spam (~87.4% ham / 12.6% spam), which is why accuracy alone is misleading here

<br/>

## 🧠 Key Concepts

- **Text Preprocessing** — lowercasing, tokenization, stopword + punctuation removal, Porter stemming
- **Feature Extraction** — Bag of Words vs TF-IDF (`max_features=3000`), and why sparse vectors work well here
- **Naive Bayes Assumption** — conditional independence between words, why it still performs well on text
- **Class Imbalance** — why precision/F1 matter more than raw accuracy for this dataset
- **Confusion Matrix** — the real-world cost of a false positive (real message flagged as spam) vs a false negative (spam that gets through)
- **Ensembling** — Voting and Stacking classifiers to squeeze out extra precision over any single model

<br/>

## 🔄 Pipeline

```
Raw Data (spam.csv, 5,572 rows)
   │
   ▼
1. Data Cleaning        → dropped unnamed columns, renamed v1/v2 → target/text,
   │                        label-encoded target, removed 403 duplicate rows (5,169 left)
   ▼
2. EDA                  → class balance, message length/word/sentence stats,
   │                        pairplot + correlation heatmap, WordClouds, top-30 word frequency
   ▼
3. Text Preprocessing   → lowercase → tokenize → remove stopwords/punctuation → Porter stemming
   │
   ▼
4. Feature Extraction   → TF-IDF (max_features=3000) chosen over Bag of Words
   │
   ▼
5. Model Building       → trained & compared 11 classifiers (NB variants, SVM, LR, KNN, DT,
   │                        RF, AdaBoost, Bagging, Extra Trees, GBDT, XGBoost)
   ▼
6. Evaluation           → precision-first comparison, confusion matrix per model
   │
   ▼
7. Model Selection      → Soft Voting Classifier (SVM + MultinomialNB + Extra Trees) —
   │                        best accuracy/precision tradeoff; Stacking also tested
   ▼
8. Deployment (optional) → Streamlit app for live predictions
```

<br/>

## 🛠️ Tech Stack

<div align="center">

![Python](https://img.shields.io/badge/Python-4A5D45?style=for-the-badge&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-6B8F71?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-87A96B?style=for-the-badge&logo=pandas&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-4A5D45?style=for-the-badge&logo=scikitlearn&logoColor=white)
![NLTK](https://img.shields.io/badge/NLTK-6B8F71?style=for-the-badge&logo=python&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-4A5D45?style=for-the-badge&logo=xgboost&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-87A96B?style=for-the-badge&logo=plotly&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-6B8F71?style=for-the-badge&logo=python&logoColor=white)

</div>

<br/>

## 🚀 How to Run

```bash
# From the repo root
cd 02_Classification/SMS-Spam-Classifier

# Install dependencies (if not already installed at repo root)
pip install numpy pandas scikit-learn nltk xgboost matplotlib seaborn wordcloud jupyter

# Launch notebook
jupyter notebook model.ipynb
```

### Predict on a custom message

```python
import pickle

tfidf = pickle.load(open('vectorizer.pkl', 'rb'))
model = pickle.load(open('model.pkl', 'rb'))

message = ["Congratulations! You've won a free prize, click here to claim now."]
vector = tfidf.transform(message)
prediction = model.predict(vector)

print("Spam" if prediction[0] == 1 else "Ham")
```

<br/>

## 📊 Results Summary

TF-IDF (3,000 features) + 80/20 train-test split, evaluated on 1,034 held-out messages:

| Model | Accuracy | Precision |
|---|---|---|
| **Voting Classifier (SVM + NB + ExtraTrees, soft)** | **98.16%** | **98.37%** |
| Extra Trees Classifier | 97.78% | 98.32% |
| SVM (sigmoid kernel) | 97.78% | 97.52% |
| Stacking Classifier (SVM + NB + ExtraTrees → RF) | 97.97% | 93.98% |
| Random Forest | 97.29% | 97.41% |
| Multinomial Naive Bayes | 97.20% | 100.00% |
| XGBoost | 96.81% | 95.65% |
| K-Nearest Neighbors | 90.52% | 100.00% |
| Logistic Regression | 95.65% | 96.97% |
| Bagging Classifier | 95.65% | 86.61% |
| Gradient Boosting | 94.78% | 92.00% |
| AdaBoost | 92.17% | 82.02% |
| Decision Tree | 92.75% | 82.47% |

> **Chosen model: Soft Voting Classifier** (SVM + Multinomial NB + Extra Trees). Multinomial NB and KNN hit 100% precision but at the cost of recall/accuracy — with a mostly-ham dataset, a model that's too eager to predict "ham" inflates precision trivially. The voting ensemble gives the best precision without sacrificing accuracy, which fits the "minimize false positives, but still actually catch spam" goal.

<br/>

## 📁 Project Structure

```
SMS-Spam-Classifier/
├── spam.csv
├── model.ipynb
└── README.md
```

<br/>

## 🚀 Future Improvements

- [ ] Pickle the final vectorizer + voting classifier (`vectorizer.pkl`, `model.pkl`) for reuse outside the notebook
- [ ] Deploy as a Streamlit web app for live message checking
- [ ] Try word embeddings (Word2Vec/GloVe) instead of TF-IDF
- [ ] Experiment with a lightweight transformer (DistilBERT) for comparison
- [ ] Add a Flask/FastAPI backend for API-based predictions
- [ ] Re-run the max_features sweep for TF-IDF (only 3,000 was tested end-to-end)

<br/>

## 📌 Notes

- Dataset used is the SMS Spam Collection Dataset (UCI / Kaggle), loaded from `spam.csv` with `latin-1` encoding
- Notebook (`model.ipynb`) covers data cleaning, EDA, text preprocessing, feature extraction, model training/comparison, and voting/stacking ensembles
- Precision is prioritized over accuracy throughout due to class imbalance, but the final model was picked on precision *and* accuracy together — not precision alone

<br/>

<div align="center">
<i>⬅️ Back to <a href="../">02_Classification</a></i>
</div>
