<div align="center">

<img src="https://img.shields.io/badge/Project-Movie_Recommender_System-06B6D4?style=for-the-badge" />
<img src="https://img.shields.io/badge/type-Content--Based_Filtering-7B2CBF?style=flat-square" />
<img src="https://img.shields.io/badge/deployed_on-Heroku-000000?style=flat-square&logo=heroku&logoColor=white" />

</div>

<br/>

# 🎬 Movie Recommender System

A content-based movie recommendation engine that suggests similar movies based on plot, genre, cast, crew, and keywords — built end-to-end from raw data to a deployed, interactive web app.

Give it any movie you like, and it recommends 5 similar titles using vector similarity over movie metadata — no user ratings or collaborative data required.

<br/>

## ✨ Features

| Feature | Description |
|---|---|
| 🎯 **Content-Based Recommendations** | Suggests movies based on overview, genres, keywords, cast & crew similarity |
| 🖼️ **Poster Fetching** | Pulls movie posters live via the TMDB API |
| 🔍 **Searchable Dropdown** | Pick any movie from the dataset via a simple UI |
| ⚡ **Precomputed Similarity** | Cosine similarity matrix precomputed and pickled for instant recommendations |
| ☁️ **Live Deployment** | Deployed on Heroku for public access |

<br/>

## 🧠 How It Works

1. **Data Collection** — TMDB 5000 Movies & Credits dataset (~5000 movies with metadata)
2. **Data Merging** — Combines the movies and credits datasets on the `title` column
3. **Feature Engineering** — Extracts and cleans:
   - Genres
   - Keywords
   - Top 3 cast members
   - Director (from crew)
   - Overview text
4. **Tag Creation** — Concatenates overview + genres + keywords + cast + crew into a single `tags` column per movie
5. **Vectorization** — Converts tags into vectors using `CountVectorizer` (`max_features=5000`, English stop words removed)
6. **Similarity Computation** — Calculates pairwise **cosine similarity** across all movie vectors
7. **Recommendation Function** — For a selected movie, returns the top 5 most similar movies by similarity score
8. **Web App** — Wraps the recommendation logic in a Streamlit interface with poster display
9. **Deployment** — Packaged and deployed on Heroku with `Procfile`, `setup.sh`, and `requirements.txt`

<br/>

## 🛠️ Tech Stack

<div align="center">

![Python](https://img.shields.io/badge/Python-06B6D4?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-000000?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-7B2CBF?style=for-the-badge&logo=numpy&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-06B6D4?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![Heroku](https://img.shields.io/badge/Heroku-430098?style=for-the-badge&logo=heroku&logoColor=white)
![TMDB API](https://img.shields.io/badge/TMDB_API-01B4E4?style=for-the-badge&logo=themoviedatabase&logoColor=white)

</div>

<br/>

## 📊 Dataset

- **Source:** [TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata) (Kaggle)
- **Files used:** `tmdb_5000_movies.csv`, `tmdb_5000_credits.csv`
- **Key columns used:** `title`, `overview`, `genres`, `keywords`, `cast`, `crew`

<br/>

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- pip
- A [TMDB API key](https://www.themoviedb.org/settings/api) (free, for poster fetching)

### Installation

```bash
# Clone the repository
git clone https://github.com/ksahu-298/movie-recommender-system.git
cd movie-recommender-system

# Create a virtual environment
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Add your TMDB API key
# (either as an environment variable or directly in the app config)
export TMDB_API_KEY=your_api_key_here

# Run the Streamlit app
streamlit run app.py
```

The app will be available at `http://localhost:8501`.

<br/>

## ☁️ Deploying to Heroku

```bash
# Login to Heroku
heroku login

# Create a new Heroku app
heroku create your-app-name

# Push to Heroku
git push heroku main

# Open the deployed app
heroku open
```

Required files for Heroku deployment:
```
Procfile          # web: sh setup.sh && streamlit run app.py
setup.sh          # Streamlit server configuration for Heroku
requirements.txt  # Python dependencies
runtime.txt       # Python version specification
```

<br/>

## 📁 Project Structure

```
movie-recommender-system/
├── app.py                    # Streamlit application
├── movie_recommender.ipynb   # Data preprocessing & model building notebook
├── movie_list.pkl            # Pickled processed movie data
├── similarity.pkl            # Pickled cosine similarity matrix
├── Procfile                  # Heroku process file
├── setup.sh                  # Heroku Streamlit config
├── requirements.txt          # Python dependencies
├── runtime.txt                # Python runtime version
└── README.md
```

<br/>

## 🌐 Live Demo

🔗 [Try the app here](#) — *add your Heroku deployment link*

<br/>

## 📸 Screenshots

*Add screenshots of the app UI here — movie selection dropdown and recommendation results with posters*

<br/>

## 🔑 Key Takeaways

- How content-based filtering works without needing user rating data
- Text vectorization with `CountVectorizer` and why stop words are removed
- Cosine similarity as a metric for measuring content closeness
- Precomputing and pickling models for fast inference in production
- End-to-end deployment of an ML app from notebook to live web service

<br/>

## 📄 License

This project is licensed under the MIT License.

<br/>

<div align="center">
<i>Built following CampusX's Movie Recommender System tutorial series 🎬</i>
</div>
