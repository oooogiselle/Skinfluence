# Skinfluence

## Project Goals

This project examines consumer perception of U.S. and Korean skincare brands in relation to each brand's stated mission and values. We analyze sentiment from Instagram captions and Reddit comments to assess whether users echo or diverge from brand-promoted ideals. By comparing U.S. and Korean brands, we investigate how cultural values and stereotypes shape consumer language, sentiment, and brand alignment.

---

## Repository Structure

```
Skinfluence/
├── 01_sentiment_analysis/
│   └── instagram/
│       ├── 01_clean_instagram_data.ipynb
│       └── 02_instagram_sentiment_analysis.ipynb
├── 02_cultural_analysis/
│   └── 02_sentimentAnalysis.ipynb
├── 03_alignment_analysis/
│   └── 01/
│       └── reddit/
│           ├── 01_load_brand_data.ipynb
│           ├── 02_load_reddit_data.ipynb
│           ├── 03_clean_reddit_data.ipynb
│           ├── 04_align_reddit_tfidf.ipynb
│           └── 05_align_reddit_st.ipynb
├── data/
│   ├── instagram/
│   │   └── elf_cosmetics.csv
│   ├── brand/
│   │   └── all_brands.csv
│   └── alignment_analysis/
│       ├── subreddit_data.csv
│       └── subreddit_comment_data.csv
├── output/
│   ├── sentiment_analysis/
│   │   ├── sentiment_vs_engagement.png
│   │   ├── sentiment_distribution_boxplot.png
│   │   └── hashtag_sentiment_barplot.png
│   ├── brand_image_analysis/
│   └── alignment_analysis/
│       └── tdidf_alignment_score_comparison.png
├── .env
└── README.md
```

---

## Order to Run

1. [`01_sentiment_analysis/instagram/01_clean_instagram_data.ipynb`](01_sentiment_analysis/instagram/01_clean_instagram_data.ipynb)
2. [`01_sentiment_analysis/instagram/02_instagram_sentiment_analysis.ipynb`](01_sentiment_analysis/instagram/02_instagram_sentiment_analysis.ipynb)
3. [`02_cultural_analysis/02_sentimentAnalysis.ipynb`](02_cultural_analysis/02_sentimentAnalysis.ipynb)
4. [`03_alignment_analysis/01/reddit/01_load_brand_data.ipynb`](03_alignment_analysis/01/reddit/01_load_brand_data.ipynb)
5. [`03_alignment_analysis/01/reddit/02_load_reddit_data.ipynb`](03_alignment_analysis/01/reddit/02_load_reddit_data.ipynb)
6. [`03_alignment_analysis/01/reddit/03_clean_reddit_data.ipynb`](03_alignment_analysis/01/reddit/03_clean_reddit_data.ipynb)
7. [`03_alignment_analysis/01/reddit/04_align_reddit_tfidf.ipynb`](03_alignment_analysis/01/reddit/04_align_reddit_tfidf.ipynb)
8. [`03_alignment_analysis/01/reddit/05_align_reddit_st.ipynb`](03_alignment_analysis/01/reddit/05_align_reddit_st.ipynb)

---

## Project Structure

### 1. Sentiment Analysis (`01_sentiment_analysis/`)

#### Instagram Data Cleaning

**File:** `01_sentiment_analysis/instagram/01_clean_instagram_data.ipynb`

**Takes in:**

- 10 Instagram brand CSVs from `data/instagram/` (e.g., `elf_cosmetics.csv`)

**What it does:**

- Concatenates all Instagram CSVs
- Applies NLTK-based text preprocessing
- Adds `brand` column for source tracking

**Outputs:**

- `data/instagram/all_instagram_cleaned.csv` – Cleaned and unified dataset

#### Instagram Sentiment Analysis

**File:** `01_sentiment_analysis/instagram/02_instagram_sentiment_analysis.ipynb`

**Takes in:**

- `all_instagram_cleaned.csv` from previous step

**What it does:**

- Applies VADER sentiment analysis to Instagram captions
- Compares sentiment across brands and hashtags
- Visualizes sentiment vs. engagement (likes/views)
- Includes hashtag-level sentiment breakdown
- Performs LDA topic modeling on captions

**Outputs:**

- `sentiment_vs_engagement.png`
- `sentiment_distribution_boxplot.png`
- `hashtag_sentiment_barplot.png`
- Topic word list by brand from LDA

---

### 2. Brand Image Analysis (`02_cultural_analysis/`)

**File:** `02_sentimentAnalysis.ipynb`

**Takes in:**

- `data/instagram/all_instagram_cleaned.csv`

**What it does:**

- Performs LDA topic modeling on captions by brand
- Identifies top 5 topics per brand and extracts top 10 words for each

**Outputs:**

- Topic summaries stored in `output/brand_image_analysis/`
- Optional: Word clouds or CSVs for visualizing topic structure

---

### 3. Alignment Analysis (`03_alignment_analysis/`)

#### Load Brand Data

**File:** `03_alignment_analysis/01/reddit/01_load_brand_data.ipynb`

**Takes in:**

- Kaggle brand datasets (`data/brand/`)

**What it does:**

- Extracts and deduplicates brand names
- Compiles full brand list

**Outputs:**

- `data/brand/all_brands.csv`

#### Load Reddit Data

**File:** `03_alignment_analysis/01/reddit/02_load_reddit_data.ipynb`

**Takes in:**

- Reddit API credentials from `.env`

**What it does:**

- Searches multiple subreddits for top posts mentioning brands within the last 5 years
- Uses `rapidfuzz` to match brand names in post titles
- Filters out bots and saves top 10 user comments per post

**Outputs:**

- `data/alignment_analysis/subreddit_data.csv`

#### Clean Reddit Data

**File:** `03_alignment_analysis/01/reddit/03_clean_reddit_data.ipynb`

**Takes in:**

- `subreddit_data.csv`

**What it does:**

- Flattens `top_comments` to individual rows
- Applies text preprocessing
- Filters out unrelated brand mentions

**Outputs:**

- `data/alignment_analysis/subreddit_comment_data.csv`

#### TF-IDF Alignment

**File:** `03_alignment_analysis/01/reddit/04_align_reddit_tfidf.ipynb`

**Takes in:**

- `subreddit_comment_data.csv`
- `all_brands_cleaned.csv` containing standardized mission statements

**What it does:**

- Uses `TfidfVectorizer` to convert both comments and brand values into numerical vectors
- Computes cosine similarity between each comment and its corresponding brand's value
- Aggregates results to compute per-brand mean and z-scored alignment

**Outputs:**

- `output/alignment_analysis/tdidf_alignment_score_comparison.png` A bar chart of alignment score for each brand divided by brand region

#### Sentence Transformer Alignment

**File:** `03_alignment_analysis/01/reddit/05_align_reddit_st.ipynb`

**Takes in:**

- `subreddit_comment_data.csv`
- `all_brands_cleaned.csv` containing standardized mission statements

**What it does:**

- Encodes comments and brand values using `SentenceTransformer` (all-MiniLM-L6-v2)
- Same process as `03_alignment_analysis/01/reddit/04_align_reddit_tfidf.ipynb`, the cosine similarity is computed between semantic embeddings and aggregate result per brand
- Calculates cosine similarity between semantic embedding

**Outputs:**

- `output/alignment_analysis/tdidf_alignment_score_comparison.png` A bar chart of alignment score for each brand divided by brand region

---

## Data Sources

- Reddit API
- Instagram API
- Brand websites for official mission statements and values
- Manual data collection for brand categorization

---

## Notes

- Ensure your `.env` file is properly configured with Reddit API credentials (Will share in Slack)
- The data and output files used in this analysis are available in the following [Google Drive folder](https://drive.google.com/drive/folders/1VYgkBRTadV36eDl3bhuAFxh7K9SxPxSi?dmr=1&ec=wgc-drive-hero-goto).
- Comment filtering excludes bots, deleted posts, and unrelated brands.
- Code not directly cited in the final paper may still demonstrate iterative work or exploratory analysis.
- Visuals are saved in respective folders and used in reporting insights on alignment and sentiment.
