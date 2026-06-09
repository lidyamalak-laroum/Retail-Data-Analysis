# 👗 Women's Clothing E-Commerce — Sentiment Analysis
> *Turning 22,641 customer reviews into actionable business intelligence*

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?style=flat&logo=powerbi)
![NLP](https://img.shields.io/badge/NLP-TextBlob%20%7C%20NLTK-green?style=flat)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat)

---

## 📖 Overview

An end-to-end data analysis project that processes raw e-commerce reviews through a custom NLP pipeline, extracts sentiment signals and keyword themes, and delivers findings through a 3-page interactive Power BI dashboard.

The core insight: **averages lie**. While the overall recommendation rate sits at 82%, drilling into sentiment by department, age group, and keyword reveals hidden friction points that aggregate numbers completely mask.

---

## ❓ Business Questions

This project was built to answer 4 specific questions:

| # | Question | Answered In |
|---|---|---|
| 1 | What percentage of customers recommend their purchase? | Page 1 — KPI Card + Donut Chart |
| 2 | Which departments generate the most positive/negative sentiment? | Page 1 — Bar Chart + Page 3 — Matrix |
| 3 | What keywords appear most in negative reviews? | Page 2 — Negative Keywords Treemap |
| 4 | Is there a mismatch between star ratings and written sentiment? | Page 1 — Mismatch Rate KPI |

---

## 📊 Key Findings

| Metric | Value | Interpretation |
|---|---|---|
| Total Reviews | 22,641 | After deduplication |
| Recommendation Rate | 81.89% | Strong baseline satisfaction |
| Avg Sentiment Score | 0.27 / 1.0 | Generally positive |
| Model Correlation | 0.451 |  Moderate positive validation |
| Mismatch Rate | 5.5% | Rating ≠ written sentiment |
| Lowest Sentiment Dept | Trend (0.22) | Needs quality audit |
| Top Complaint Themes | Fabric, Fit, Boxy | Communication crisis, not quality crisis |

---

## 🔄 Pipeline Architecture

```
Raw Data (Kaggle — 23,486 rows)
         ↓
Data Cleaning & Deduplication (→ 22,641 rows)
         ↓
Feature Engineering
(full_review, review_length)
         ↓
NLP Engine
(sentiment_polarity, sentiment_subjectivity, vibe_category)
         ↓
Dual Keyword Extraction
├── key_keywords        → general product attributes
└── negative_keywords   → word-level sentiment filtered
         ↓
Model Validation
(Pearson correlation: 0.451 with star ratings)
         ↓
Age Banding + Mismatch Flag
         ↓
Export (20 columns) → Power BI Dashboard (3 pages)
```

---

## 🛠️ Tech Stack

| Tool | Version | Purpose |
|---|---|---|
| Python | 3.x | Core pipeline language |
| Pandas | Latest | Data manipulation |
| NumPy | Latest | Numerical operations |
| NLTK | Latest | POS tagging + tokenization |
| TextBlob | Latest | Sentiment analysis |
| Matplotlib / Seaborn | Latest | Diagnostic visualizations |
| Power BI Desktop | Latest | Interactive dashboard |
| Git / GitHub | — | Version control |

---

## 📁 Project Structure

```
Retail-Data-Analysis/
│
├── 📁 Dashboards/
│   └── Retail-Reports.pbix          ← Power BI dashboard (3 pages)
│
├── 📁 Data/
│   ├── 📁 Raw/                      ← original dataset (see source below)
│   └── 📁 Processed/                ← enriched 20-column dataset
│
├── 📁 Notebooks/
│   └── Analysis_pipeline.ipynb      ← full documented pipeline
│
├── 📄 sentiment_analysis.png        ← diagnostic visualizations output
├── 📄 README.md
└── 📄 .gitignore
```

---

## 📈 Dashboard Pages

### Page 1 — Executive Summary
The 30-second overview for decision makers.
- 4 KPI cards: Total Reviews, Avg Sentiment, Rec Rate %, Mismatch Rate
- Recommendation Split donut chart
- Avg Sentiment & Rating by Department (clustered bar)
- Top 10 Keywords bar chart

### Page 2 — Sentiment Audit
Deep dive into the emotional patterns behind the numbers.
- Overall Sentiment Score gauge (-1 to +1 scale, target: 0.5)
- Review Length vs Sentiment scatter plot (by Vibe Category)
- Sentiment Heatmap by Department × Age Band (matrix)
- Negative Review Keywords treemap (word-level filtered)

### Page 3 — Strategic Action
Drill-down tool for product and category managers.
- Interactive slicers: Clothing ID + Department
- Performance matrix: Avg Rating, Avg Sentiment, Total Reviews
- Red-to-green conditional formatting on sentiment column

---

## 🧠 What Makes This Pipeline Different

Standard keyword extractors return noise like "i", "dress", "petite".

This pipeline uses **word-level sentiment scoring** to filter keywords automatically:

```python
# Instead of manually guessing stopwords:
word_sentiment = TextBlob(word).sentiment.polarity
if word_sentiment >= 0.1:  # skip positive words
    continue
```

Result:
```
Before → "i, petite", "great, quality", "i, hte"
After  → "disappointed, dress", "awful, fabric", "boxy, top"
```

No manual lists. No guessing. Automated polarity based filtering.

---

## ✅ Model Validation

The NLP model is validated by correlating sentiment polarity with star ratings:

```
1★ → 0.062 sentiment  (lowest — correct ✅)
2★ → 0.118 sentiment
3★ → 0.170 sentiment
4★ → 0.246 sentiment
5★ → 0.328 sentiment  (highest — correct ✅)

Pearson Correlation: 0.451 → MODERATE POSITIVE CORRELATION✅
```

If the model were random, this progression would not exist.

---

## ⚠️ Limitations

- **TextBlob cannot detect sarcasm or negation** — "not great" may score positively
- **Static dataset** — not connected to live review feed
- **1.7% negative vibe rate** may be underestimated due to TextBlob's conservative thresholds
- **Next step:** upgrade NLP to VADER or BERT for higher accuracy

---

## 📥 Dataset

Raw data is not committed due to file size (>50MB).

**Source:** [Women's Clothing E-Commerce Reviews — Kaggle](https://www.kaggle.com/datasets/nicapotato/womens-ecommerce-clothing-reviews)

Download and place in `Data/Raw/` then run the notebook to regenerate the processed dataset automatically.

---

## 🚀 How to Run

```bash
# 1. Clone the repo
git clone https://github.com/lidyamalak-laroum/Retail-Data-Analysis.git

# 2. Install dependencies
pip install pandas numpy nltk textblob tqdm matplotlib seaborn scipy

# 3. Download raw data from Kaggle → place in Data/Raw/

# 4. Open and run Notebooks/Analysis_pipeline.ipynb
#    (Kernel → Restart & Run All)

# 5. Open Dashboards/Retail-Reports.pbix in Power BI Desktop
#    (Home → Transform data → Refresh if needed)
```

---

## 👩‍💻 Author

**Lidya Malak Laroum**

[![LinkedIn]](https://www.linkedin.com/in/lidya-malak-laroum/)
[![GitHub]](https://github.com/lidyamalak-laroum)

---

*Built from scratch — Kaggle → Python → NLP → Power BI → GitHub*
