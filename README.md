# A Comparative Evaluation of Text Representation Techniques for Content-Based Job Recommendation System

MSc in Data Analytics thesis, CCT College Dublin (2024). A content-based job recommender built with three text representations (TF-IDF + Bag-of-Words, Word2Vec and fine-tuned BERT), using 1,166 job ads collected in Dublin in January 2024 and evaluated against the ratings of 3 job seekers.

**Tools:** Python, Jupyter, pandas, NumPy, SciPy, scikit-learn, NLTK, gensim, Hugging Face Transformers, PyTorch, Selenium, matplotlib, seaborn.

## Research question

Which text representation (TF-IDF + Bag-of-Words, Word2Vec or BERT) ranks job ads in the way that agrees most with how job seekers themselves rate them?

## Data

| Dataset | How it was collected | Size |
|---|---|---|
| Job ads | Scraped from Indeed.ie with Selenium, Dublin, 10 and 20 January 2024 | 1,166 ads: registered nurse 644, data analyst 376, electrician 146 |
| Job seekers | 2 voice-call interviews and 1 Google Form, December 2023 | 3 participants (a nurse, an electrician, a data analyst), named `user_1` to `user_3` |

The raw data files are not included in this repository. The job ads are third-party content, and the participant data was collected for this thesis only.

## Method

| Step | What it does | Notebook |
|---|---|---|
| 1. Data collection | Scrapes the job ads, removes duplicates between the two dates, and prepares the job seekers' profiles. | [1_job_ads_collection](thesis/1_job_ads_collection.ipynb), [2_job_seekers_data](thesis/2_job_seekers_data.ipynb) |
| 2. Classification | Trains three models to sort the ads into the 3 occupations: fine-tuned BERT (`bert-base-uncased`), Word2Vec + logistic regression, and TF-IDF + Bag-of-Words + logistic regression. BERT uses a 734 / 82 / 350 train / validation / test split. | [3_classification](thesis/3_classification.ipynb) |
| 3. Ranking | Turns each job seeker's profile and every ad into vectors with each method, then ranks the ads by cosine similarity to the profile. | [4_job_ranking](thesis/4_job_ranking.ipynb) |
| 4. Evaluation | Each participant rated 30 ads per method on a 1–3 scale. Their ratings were compared with the model's ranking using Spearman's rank correlation and the Wilcoxon signed-rank test. | [5_evaluation](thesis/5_evaluation.ipynb) |

## Results (as reported in the thesis)

Spearman's rank correlation between each method's ranking and the participant's own rating (30 ads per participant per method):

| Participant | BERT | Word2Vec | TF-IDF + BoW |
|---|---|---|---|
| Nurse (`user_1`) | 0.83 | 0.76 | 0.60 |
| Electrician (`user_2`) | 0.85 | 0.78 | 0.70 |
| Data analyst (`user_3`) | 0.90 | 0.70 | 0.86 |

These results come from 3 people and 30 ads each, so they should be read together with the limitations below.

## Limitations

- Small study: 3 participants, each rating 30 ads per method on a 1–3 scale.
- BERT was fine-tuned on these job ads, while Word2Vec and TF-IDF were not trained on them, so BERT had more information about the ads.
- Each method was rated on its own set of 30 ads.
- The high correlations may mostly reflect telling the 3 occupations apart, not ranking ads well within one occupation.
- The ads come from one job site, one city and January 2024 only.

## Repository structure

```
text-representation-comparison-job-recommender/
├── thesis/
│   ├── 1_job_ads_collection.ipynb
│   ├── 2_job_seekers_data.ipynb
│   ├── 3_classification.ipynb
│   ├── 4_job_ranking.ipynb
│   └── 5_evaluation.ipynb
├── .gitignore
└── README.md
```

## Author

**Temuulen Bulgan** · [LinkedIn](https://www.linkedin.com/in/temulenbd/)

MSc in Data Analytics, CCT College Dublin (2024). Supervisor: Kislay Raj.
