<div align="center">
<img src="https://img.shields.io/badge/Project-SMS_Spam_Classifier-6B8F71?style=for-the-badge" />
<img src="https://img.shields.io/badge/status-in_progress-87A96B?style=flat-square" />
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
- **Size:** ~5,500 labeled messages
- **Columns:** `label` (spam/ham), `message` (raw text)
- **Class distribution:** Imbalanced — roughly 87% ham / 13% spam, which is why accuracy alone is misleading here

<br/>

## 🧠 Key Concepts

- **Text Preprocessing** — lowercasing, tokenization, stopword removal, stemming
- **Feature Extraction** — Bag of Words vs TF-IDF, and why sparse vectors work well here
- **Naive Bayes Assumption** — conditional independence between words, why it still performs well on text
- **Class Imbalance** — why precision/F1 matter more than raw accuracy for this dataset
- **Confusion Matrix** — the real-world cost of a false positive (real message flagged as spam) vs a false negative (spam that gets through)

<br/>

## 🔄 Pipeline

```
Raw Data
   │
   ▼
1. Data Cleaning        → remove duplicates, nulls, irrelevant columns
   │
   ▼
2. EDA                  → class balance, message length, word frequency, WordClouds
   │
   ▼
3. Text Preprocessing   → lowercase → tokenize → remove stopwords/punctuation → stemming
   │
   ▼
4. Feature Extraction   → Bag of Words vs TF-IDF comparison
   │
   ▼
5. Model Building       → train & compare multiple classifiers
   │
   ▼
6. Evaluation           → precision-first comparison, confusion matrix
   │
   ▼
7. Model Selection      → pick best precision/accuracy tradeoff
   │
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
![Matplotlib](https://img.shields.io/badge/Matplotlib-87A96B?style=for-the-badge&logo=plotly&logoColor=white)

</div>

<br/>

## 🚀 How to Run

```bash
# From the repo root
cd 02_Classification/SMS-Spam-Classifier

# Install dependencies (if not already installed at repo root)
pip install numpy pandas scikit-learn nltk matplotlib jupyter

# Launch notebook
jupyter notebook
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

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| Multinomial Naive Bayes | _—_ | _—_ | _—_ | _—_ |
| Logistic Regression | _—_ | _—_ | _—_ | _—_ |
| Support Vector Machine (SVM) | _—_ | _—_ | _—_ | _—_ |
| Random Forest | _—_ | _—_ | _—_ | _—_ |

> ✏️ Fill in your actual scores once the notebook is finalized. Precision is the tie-breaker for this project — a real message misclassified as spam is the costlier mistake.

<br/>

## 📁 Project Structure

```
SMS-Spam-Classifier/
├── data/
│   └── spam.csv
├── sms_spam_classifier.ipynb
├── model.pkl
├── vectorizer.pkl
├── requirements.txt
└── README.md
```

<br/>

## 🚀 Future Improvements

- [ ] Deploy as a Streamlit web app for live message checking
- [ ] Try word embeddings (Word2Vec/GloVe) instead of TF-IDF
- [ ] Experiment with a lightweight transformer (DistilBERT) for comparison
- [ ] Add a Flask/FastAPI backend for API-based predictions

<br/>

## 📌 Notes

- Dataset used is the SMS Spam Collection Dataset — [add exact source link once finalized]
- Notebook includes EDA, preprocessing, model training, and evaluation sections
- Precision is prioritized over accuracy throughout due to class imbalance

<br/>

<div align="center">
<i>⬅️ Back to <a href="../">02_Classification</a></i>
</div>