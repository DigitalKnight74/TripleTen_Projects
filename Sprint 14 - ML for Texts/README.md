# Film Junky Union — Sentiment Classification

### Sprint 14 | TripleTen Data Science Bootcamp

---

## Project Overview

The Film Junky Union is a community platform for classic movie enthusiasts. This project develops an automated system for filtering and categorizing movie reviews by sentiment. Using a dataset of IMDB movie reviews with polarity labels, multiple machine learning models were trained and evaluated to classify reviews as positive or negative.

**Win Condition:** F1 Score ≥ 0.85 on the test set.

---

## Dataset

- **Source:** IMDB movie reviews dataset (`imdb_reviews.tsv`)  
- **Size:** 47,331 reviews across 17 features  
- **Target:** `pos` — binary label (1 \= positive, 0 \= negative)  
- **Split:** Pre-divided into train (23,796) and test (23,535) sets via `ds_part` column  
- **Class Balance:** 50.1% negative / 49.9% positive — effectively balanced, no resampling required

---

## Project Structure

Sprint-14-ML-for-Texts/

│

├── dataset/

│   └── imdb\_reviews.tsv

│

├── Film\_Junky\_Union.ipynb

└── README.md

---

## Methodology

### Data Preparation

- Self-detecting path logic for local vs. platform environments  
- Identified and documented data quality issues (`\N` strings in `end_year` and `runtime_minutes`) — neither column used downstream, no action taken  
- Text normalization: lowercase, stripped digits and punctuation via `re.sub()`

### EDA Findings

- Dataset is effectively balanced — no class imbalance intervention required  
- Train/test sets are near-mirror distributions — intentionally structured split  
- Ratings 5 and 6 deliberately excluded — ambiguous sentiment removed by design  
- Post-2000 sentiment shift explained by internet democratization broadening the reviewer pool

---

## Models

| Model | Preprocessing | Classifier | Test F1 | Train Time | Predict Time |
| :---- | :---- | :---- | :---- | :---- | :---- |
| Model 0 | None | DummyClassifier (baseline) | 0.50 | 0.0012s | 0.0029s |
| Model 1 | NLTK \+ TF-IDF | Logistic Regression | **0.88** ✅ | 0.3916s | 0.0024s |
| Model 2 | NLTK \+ TF-IDF | Multinomial Naive Bayes | 0.82 ❌ | 0.0645s | 0.0221s |
| Model 3 | spaCy \+ TF-IDF | Logistic Regression | **0.88** ✅ | 0.5165s \+ 754s preprocessing | 0.0043s |
| Model 4 | spaCy \+ TF-IDF | LGBMClassifier | **0.86** ✅ | 5.7084s \+ 754s preprocessing | 0.0724s |

---

## Results & Recommendations

### ✅ Recommended: Model 1 — Logistic Regression (NLTK \+ TF-IDF)

Model 1 is the clear winner across all three of the project's evaluation criteria:

- **Quality:** Highest test F1 score of 0.88 — exceeds the 0.85 threshold by 0.03  
- **Training Speed:** 0.3916 seconds — fast and efficient  
- **Prediction Speed:** 0.0024 seconds — fastest predictor of all models

### Key Findings

**Model 2 (Naive Bayes)** failed to meet the F1 threshold (0.82). While it was the fastest to train (6x faster than Model 1), it was surprisingly 9x slower on prediction and sacrificed accuracy for speed.

**Model 3 (spaCy \+ LR)** matched Model 1's test F1 of 0.88 but required 754 seconds of preprocessing time for spaCy lemmatization — a significant computational cost for no gain in prediction performance.

**Model 4 (spaCy \+ LightGBM)** barely passed the threshold (0.86) but trained 13x slower than Model 1 and predicted 30x slower. LightGBM underperformed on TF-IDF features due to **high dimensionality \+ sparsity** — tree-based models must evaluate tens of thousands of features at each split, making them poorly suited for sparse text matrices.

### Fundamental Limitation

All TF-IDF-based models share a common limitation: they treat text as a **bag of words**, losing context, sentence order, and negation. This was evident during personal review testing — phrases like "not a big fan" were misinterpreted because negation is invisible to word-count-based models. Models counted and weighted positive vs. negative words independently, unable to understand how words modify each other in context.

---

## Technologies Used

- **Python** 3.12 (local) / 3.9 (TripleTen platform)  
- **Libraries:** pandas, numpy, scikit-learn, NLTK, spaCy, LightGBM, matplotlib, seaborn, tqdm  
- **NLP Tools:** NLTK stopwords, spaCy `en_core_web_sm`, TF-IDF Vectorization

---

## Environment Notes

This notebook uses self-detecting path logic to handle the difference between local development and the TripleTen platform:

tripleten\_path \= '/datasets/imdb\_reviews.tsv'

local\_path \= 'your/local/path/imdb\_reviews.tsv'

if os.path.exists(tripleten\_path):

    dataset\_path \= tripleten\_path

else:

    dataset\_path \= local\_path

---

## Author

**George Knight** | DigitalKnight74  
TripleTen Data Science Bootcamp — Sprint 14  
[GitHub](https://github.com/DigitalKnight74)  
