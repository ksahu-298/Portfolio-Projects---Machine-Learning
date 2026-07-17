<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:06b6d4,100:9333ea&height=200&section=header&text=Email/SMS%20Spam%20Classifier&fontSize=42&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=A%20Binary%20Text%20Classification%20Project&descAlignY=55&descSize=18" width="100%"/>

<a href="https://git.io/typing-svg">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&color=9333EA&center=true&vCenter=true&width=550&lines=Classifying+Spam+vs+Ham+with+NLP;TF-IDF+%2B+Naive+Bayes+Pipeline;Precision-Focused+Evaluation" alt="Typing SVG" />
</a>

<br/>

![Python](https://img.shields.io/badge/Python-3.10+-06b6d4?style=for-the-badge&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-9333ea?style=for-the-badge&logo=scikitlearn&logoColor=white)
![NLTK](https://img.shields.io/badge/NLTK-NLP-06b6d4?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-In%20Progress-9333ea?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-06b6d4?style=for-the-badge)

</div>

---

## 📌 Overview

This project builds a **binary text classifier** that labels an incoming SMS/email message as **Spam** or **Ham (Not Spam)**. Unlike regression tasks that predict continuous values, this is a **classification problem** — the model outputs a discrete category, and the entire pipeline (features, loss function, and evaluation metrics) is built around that distinction.

The project follows the standard applied-NLP workflow: clean raw text → engineer features → vectorize → train multiple classifiers → select the best one by **precision**, not just accuracy (a false positive here means a real message gets buried in spam).

---

## 🎯 Problem Statement

> Given the raw text of a message, predict whether it is **Spam (1)** or **Ham (0)**.

| Aspect | Detail |
|---|---|
| Task type | Binary Classification |
| Input | Raw message text (string) |
| Output | Label — `Spam` / `Ham` |
| Primary metric | **Precision** (minimize false positives) |
| Secondary metrics | Accuracy, Recall, F1-score, Confusion Matrix |

---

## 🗂️ Dataset

- **Source:** [SMS Spam Collection Dataset (UCI / Kaggle)](https://archive.ics.uci.edu/dataset/228/sms+spam+collection)
- **Size:** ~5,500 labeled messages
- **Columns:** `label` (spam/ham), `message` (raw text)
- **Class distribution:** Imbalanced — roughly 87% ham / 13% spam, which is why accuracy alone is a misleading metric here

---

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.10+ |
| Data Handling | Pandas, NumPy |
| NLP / Preprocessing | NLTK (stopwords, stemming), `re`, `string` |
| Feature Extraction | Bag of Words, TF-IDF (`CountVectorizer`, `TfidfVectorizer`) |
| Modeling | Scikit-learn (Naive Bayes, Logistic Regression, SVM, Random Forest) |
| Visualization | Matplotlib, Seaborn, WordCloud |
| Environment | Jupyter Notebook |

---

## 🔄 Project Pipeline

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
3. Text Preprocessing    → lowercase → tokenize → remove stopwords/punctuation → stemming
   │
   ▼
4. Feature Extraction    → Bag of Words vs TF-IDF comparison
   │
   ▼
5. Model Building        → train & compare multiple classifiers
   │
   ▼
6. Evaluation            → precision-first comparison, confusion matrix
   │
   ▼
7. Model Selection        → pick best precision/accuracy tradeoff
   │
   ▼
8. Deployment (optional)  → Streamlit app for live predictions
```

---

## 🤖 Models Compared

| Model | Accuracy | Precision | Notes |
|---|---|---|---|
| Multinomial Naive Bayes | _TBD_ | _TBD_ | Classic baseline for text/word-count data |
| Logistic Regression | _TBD_ | _TBD_ | Strong linear baseline |
| Support Vector Machine (SVM) | _TBD_ | _TBD_ | Often competitive on sparse TF-IDF vectors |
| Random Forest | _TBD_ | _TBD_ | Ensemble comparison |

> Fill this table in once your notebook runs — precision is the tie-breaker, since a legitimate message misclassified as spam is the costlier error.

---

## 📊 Results

_(To be added after training — include final confusion matrix, precision/recall/F1, and the chosen model with justification.)_

---

## ⚙️ Installation & Usage

```bash
# Clone the repository
git clone https://github.com/ksahu-298/<repo-name>.git
cd <repo-name>

# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the notebook
jupyter notebook spam_classifier.ipynb
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

---

## 📁 Project Structure

```
├── data/
│   └── spam.csv
├── notebooks/
│   └── spam_classifier.ipynb
├── model.pkl
├── vectorizer.pkl
├── requirements.txt
└── README.md
```

---

## 🚀 Future Improvements

- [ ] Deploy as a Streamlit web app for live message checking
- [ ] Try word embeddings (Word2Vec/GloVe) instead of TF-IDF
- [ ] Experiment with a lightweight transformer (DistilBERT) for comparison
- [ ] Add a Flask/FastAPI backend for API-based predictions

---

## 🙏 Acknowledgements

- Dataset: UCI Machine Learning Repository — SMS Spam Collection
- Project structure inspired by CampusX's *100 Days of Machine Learning* series

---

<div align="center">

### 👤 Author

**Karan Sahu**
[![GitHub](https://img.shields.io/badge/GitHub-ksahu--298-06b6d4?style=for-the-badge&logo=github)](https://github.com/ksahu-298)

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:9333ea,100:06b6d4&height=100&section=footer" width="100%"/>

</div>
