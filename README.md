# 🎬 Movie Recommender System

A content-based movie recommendation web app built with **Streamlit**. Pick any movie from the dropdown, and the app suggests 5 similar movies along with their posters, fetched live from **The Movie Database (TMDB)**.

🔗 **Live demo:** [https://movierecommendationsystem130308.streamlit.app/]

---

## How It Works

The app uses **content-based filtering**:

1. Each movie is represented by a `tags` field (a combination of genre, cast, crew, and plot keywords).
2. These tags are converted into numerical vectors using `CountVectorizer` (bag-of-words, top 5000 features, English stop words removed).
3. **Cosine similarity** is computed between every pair of movie vectors.
4. When you select a movie, the app looks up the 5 most similar movies based on this similarity score and displays them with posters pulled from the TMDB API.

The similarity matrix is computed **on app startup** (and cached with `@st.cache_data`) rather than stored as a file — this keeps the repo lightweight and avoids GitHub's file size limits.

---

## Project Structure

```
├── app.py              # Streamlit app
├── movies.pkl           # Preprocessed movie data (id, title, tags)
├── requirements.txt     # Python dependencies
└── README.md
```

---

## Tech Stack

- **Streamlit** – web app framework
- **Pandas** – data handling
- **scikit-learn** – vectorization (`CountVectorizer`) and similarity (`cosine_similarity`)
- **TMDB API** – movie poster images

---

## Running Locally

1. Clone the repo:
   ```bash
   git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
   cd YOUR_REPO
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the app:
   ```bash
   streamlit run app.py
   ```

4. Open the local URL shown in your terminal (usually `http://localhost:8501`).

---

## Deployment

This app is deployed for free on **Streamlit Community Cloud**:

1. Push this repo to GitHub.
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **Create app**, select this repository, branch `main`, and set the main file to `app.py`.
4. Click **Deploy**.

Any future `git push` to `main` automatically redeploys the app.

---

## Dataset

Movie metadata (titles, genres, cast, crew, keywords) is based on the [TMDB 5000 Movie Dataset](https://www.kaggle.com/tmdb/tmdb-movie-metadata).

---

## Notes

- The TMDB API key used for fetching posters should ideally be stored securely using `st.secrets` rather than hardcoded, especially in a public repository.
- The similarity matrix is recomputed at runtime instead of being stored as a `.pkl` file, since the original file exceeded GitHub's size limits (~185MB).

---

## License

This project is open source and available under the [MIT License](LICENSE).
