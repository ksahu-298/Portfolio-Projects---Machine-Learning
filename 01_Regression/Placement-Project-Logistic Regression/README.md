<div align="center">

<img src="https://img.shields.io/badge/Project-Placement_Prediction-6B8F71?style=for-the-badge" />
<img src="https://img.shields.io/badge/algorithm-Logistic_Regression-87A96B?style=flat-square" />
<img src="https://img.shields.io/badge/part_of-01_Regression-4A5D45?style=flat-square" />

</div>

<br/>

# 🎓 Placement Prediction using Logistic Regression

A binary classification project that predicts whether a student gets placed based on their **CGPA** and **IQ** — a classic entry point into classification, built to understand decision boundaries and the difference between regression and classification tasks.

Part of the [**Portfolio Projects - Machine Learning**](../../) repository, under the [`01_Regression`](../) module.

<br/>

## 🎯 Problem Statement

Given a student's **CGPA** and **IQ score**, predict whether they will be **placed (1)** or **not placed (0)** — a supervised binary classification problem.

> Note: this lives inside `01_Regression` as a bridge project — it uses Logistic Regression (which, despite the name, is a classification algorithm) to contrast against the linear regression models earlier in this module and show why a linear model isn't suited to predicting a categorical outcome.

<br/>

## 📊 Dataset

| Feature | Description |
|---|---|
| `cgpa` | Student's CGPA (continuous) |
| `iq` | Student's IQ score (continuous) |
| `placement` | Target — 1 if placed, 0 if not placed |

> ✏️ Confirm the exact column names and dataset source match your CSV — update if different.

<br/>

## 🧠 Approach

1. **Exploratory Data Analysis** — scatter plot of CGPA vs IQ, colored by placement outcome
2. **Train-Test Split** — separating data for unbiased evaluation
3. **Feature Scaling** — standardizing CGPA and IQ using `StandardScaler`
4. **Model Training** — fitting a `LogisticRegression` classifier
5. **Decision Boundary Visualization** — plotting the learned boundary that separates placed vs. not-placed students
6. **Evaluation** — accuracy score on the test set

<br/>

## 🛠️ Tech Stack

<div align="center">

![Python](https://img.shields.io/badge/Python-4A5D45?style=for-the-badge&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-6B8F71?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-87A96B?style=for-the-badge&logo=pandas&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-4A5D45?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-6B8F71?style=for-the-badge&logo=plotly&logoColor=white)

</div>

<br/>

## 🚀 How to Run

```bash
# From the repo root
cd "01_Regression/Placement-Project-Logistic Regression"

# Install dependencies
pip install numpy pandas scikit-learn matplotlib mlxtend jupyter

# Launch the notebook
jupyter notebook
```

<br/>

## 📈 Results

| Metric | Score |
|---|---|
| Accuracy | 0.9 |
| Confusion Matrix | _—_ |


<br/>

## 🔑 Key Takeaways

- Why linear regression fails for classification problems (unbounded output, no probability interpretation)
- How the sigmoid function maps linear output to a 0-1 probability range
- How the decision boundary is learned and visualized in 2D feature space
- Why feature scaling matters when using gradient-based optimizers like logistic regression's solver

<br/>

## 📌 Notes

- Dataset used: [add source — e.g. CampusX 100 Days of ML placement dataset]
- This is a small/toy dataset intended for learning the classification workflow, not production use

<br/>

<div align="center">
<i>⬅️ Back to <a href="../">01_Regression</a> · <a href="../../">Portfolio Projects - Machine Learning</a></i>
</div>
