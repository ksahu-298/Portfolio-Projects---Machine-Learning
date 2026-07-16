<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:06B6D4,100:8B5CF6&height=220&section=header&text=CineMatch&fontSize=60&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=Content-Based%20Movie%20Recommender%20System&descAlignY=55&descSize=18" width="100%"/>

<a href="https://github.com/ksahu-298">
  <img src="https://readme-typing-svg.demolab.com/?font=Fira+Code&weight=600&size=22&duration=3000&pause=800&color=8B5CF6&center=true&vCenter=true&width=650&lines=Bag-of-Words+%2B+Cosine+Similarity;5%2C000-Movie+TMDB+Dataset;Genres+%C2%B7+Cast+%C2%B7+Crew+%C2%B7+Keywords+%C2%B7+Overview;Type+a+Movie+%E2%86%92+Get+5+Similar+Picks" alt="Typing SVG" />
</a>

<br/>

![Python](https://img.shields.io/badge/Python-3.10+-06B6D4?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-8B5CF6?style=for-the-badge&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Vectorization-06B6D4?style=for-the-badge&logo=scikit-learn&logoColor=white)
![NLTK](https://img.shields.io/badge/NLTK-Stemming-8B5CF6?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-06B6D4?style=for-the-badge&logo=jupyter&logoColor=white)

![Repo Size](https://img.shields.io/github/repo-size/ksahu-298/movie-recommender-system?style=flat-square&color=8B5CF6&label=Repo%20Size)
![Last Commit](https://img.shields.io/github/last-commit/ksahu-298/movie-recommender-system?style=flat-square&color=06B6D4&label=Last%20Commit)
![License](https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square)

</div>

<br/>

## 🎬 What This Is

**CineMatch** is a **content-based movie recommender system** built from the ground up on the **TMDB 5000 Movies** dataset. Give it a movie title, and it returns the **5 most similar films** — no ratings, no user history, purely based on *what a movie is about*: its plot, genres, cast, crew, and keywords.

> No collaborative filtering. No black-box embeddings. Just clean NLP feature engineering + vector similarity — built to understand the fundamentals before reaching for the fancy stuff.

<br/>

## 📑 Table of Contents

- [How It Works](#-how-it-works)
- [Pipeline Breakdown](#-pipeline-breakdown)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Usage](#-usage)
- [Sample Output](#-sample-output)
- [Dataset](#-dataset)
- [Roadmap](#-roadmap)
- [License](#-license)

<br/>

## ⚙️ How It Works

<div align="center">

```mermaid
flowchart LR
    A["🎞️ movies.csv\n+ credits.csv"] --> B["🔗 Merge on\ntitle"]
    B --> C["🧹 Select & clean\nkey features"]
    C --> D["🏷️ Extract genres,\nkeywords, top-3 cast,\ndirector"]
    D --> E["📝 Build unified\n'tags' column"]
    E --> F["🌱 Porter\nStemming"]
    F --> G["🔢 CountVectorizer\n(5,000 features)"]
    G --> H["📐 Cosine\nSimilarity Matrix"]
    H --> I["🎯 Top-5\nRecommendations"]

    style A fill:#06B6D4,color:#fff
    style E fill:#0891B2,color:#fff
    style G fill:#7C3AED,color:#fff
    style H fill:#8B5CF6,color:#fff
    style I fill:#A855F7,color:#fff
```

</div>

Every movie is boiled down into a single **"tag"** string — its overview, genres, keywords, top 3 cast members, and director, all lowercased, space-stripped, and stemmed. Each tag is vectorized into a **5,000-dimension bag-of-words vector**, and recommendations come from ranking every other movie by **cosine similarity** to the queried one.

<br/>

## 🧩 Pipeline Breakdown

<details>
<summary><b>1️⃣ Data Loading & Merging</b></summary>
<br/>

`movies.csv` (4,809 rows × 20 columns) and `credits.csv` are merged on `title` into a single DataFrame containing budget, genres, cast, crew, keywords, overview, and more.

</details>

<details>
<summary><b>2️⃣ Feature Selection</b></summary>
<br/>

Only the columns that matter for content similarity are kept:
`id`, `title`, `overview`, `genres`, `keywords`, `cast`, `crew`

</details>

<details>
<summary><b>3️⃣ Cleaning</b></summary>
<br/>

- Dropped rows with missing `overview` values
- Checked for duplicate entries (none found)

</details>

<details>
<summary><b>4️⃣ Structured Field Parsing</b></summary>
<br/>

The `genres`, `keywords`, `cast`, and `crew` columns arrive as **stringified JSON**. Custom parsers built on `ast.literal_eval` extract:
- All genre & keyword names
- Only the **top 3 billed cast members**
- Only the **director** from the crew list

</details>

<details>
<summary><b>5️⃣ Tag Engineering</b></summary>
<br/>

Every list field has whitespace stripped from its entries (so `"Sam Worthington"` → `"SamWorthington"`, preventing cross-name token collisions), then `overview + genres + keywords + cast + crew` are concatenated into one `tags` list, joined into a lowercase string.

</details>

<details>
<summary><b>6️⃣ Stemming</b></summary>
<br/>

A **Porter Stemmer** (NLTK) reduces every word in `tags` to its root form, so `"action"`, `"actions"`, and `"acting"` all collapse to the same token — shrinking vocabulary noise before vectorization.

</details>

<details>
<summary><b>7️⃣ Vectorization</b></summary>
<br/>

`CountVectorizer(max_features=5000, stop_words='english')` turns every movie's tag string into a **5,000-dimension bag-of-words vector**.

</details>

<details>
<summary><b>8️⃣ Similarity & Recommendation</b></summary>
<br/>

`cosine_similarity()` computes a full **4,809 × 4,809 similarity matrix**. The `recommend()` function looks up a movie's row, sorts every other movie by similarity score, and returns the **top 5 closest matches**.

</details>

<br/>

## 🛠️ Tech Stack

<div align="center">

| Layer | Tools |
|---|---|
| **Data Handling** | `pandas`, `numpy` |
| **Parsing** | `ast.literal_eval` |
| **NLP** | `nltk` (Porter Stemmer) |
| **Vectorization** | `scikit-learn` — `CountVectorizer` |
| **Similarity** | `scikit-learn` — `cosine_similarity` |
| **Environment** | Jupyter Notebook |

</div>

<br/>

## 📁 Project Structure

```
movie-recommender-system/
├── model.ipynb          # Full pipeline: load → clean → vectorize → recommend
├── movies.csv            # TMDB movie metadata
├── credits.csv            # Cast & crew data
└── README.md
```

<br/>

## 🚀 Getting Started

```bash
# 1. Clone the repo
git clone https://github.com/ksahu-298/movie-recommender-system.git
cd movie-recommender-system

# 2. Install dependencies
pip install pandas numpy scikit-learn nltk jupyter

# 3. Download the TMDB 5000 dataset (movies.csv + credits.csv)
#    from Kaggle and place both files in the project root

# 4. Launch the notebook
jupyter notebook model.ipynb
```

<br/>

## 💻 Usage

Run every cell top to bottom, then call the recommender directly:

```python
recommend('Avatar')
```

<br/>

## 🎯 Sample Output

<div align="center">

```
> recommend('Avatar')

🎬 Titan A.E.
🎬 Small Soldiers
🎬 Ender's Game
🎬 Aliens vs Predator: Requiem
🎬 Independence Day
```

</div>

Every result shares Avatar's sci-fi/action DNA — alien conflict, futuristic warfare, and overlapping cast/crew signals picked up purely from text features.

<br/>

## 📊 Dataset

<div align="center">

| Metric | Value |
|---|---|
| **Source** | TMDB 5000 Movie Dataset |
| **Movies after cleaning** | 4,809 |
| **Vocabulary size** | 5,000 tokens |
| **Features fused into tags** | overview, genres, keywords, cast (top 3), director |

</div>

<br/>

## 🗺️ Roadmap

- [ ] Swap Bag-of-Words for **TF-IDF** to weigh rarer, more distinctive terms higher
- [ ] Serialize `similarity` matrix + `new_df` with `pickle` for reuse without re-running the pipeline
- [ ] Wrap `recommend()` in a **Streamlit** app with poster fetching via the TMDB API
- [ ] Add fuzzy title matching so typos/partial titles still resolve
- [ ] Experiment with word embeddings (Word2Vec / sentence-transformers) as a similarity upgrade

<br/>

## 📄 License

Distributed under the **MIT License** — free to use, modify, and build on.

<br/>

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:8B5CF6,100:06B6D4&height=120&section=footer" width="100%"/>

**Built by [Karan Sahu](https://github.com/ksahu-298)**

</div>
