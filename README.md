[README.md](https://github.com/user-attachments/files/26640259/README.md)
# KIN 7518 – Project 3: Political Engagement on Athlete Instagram Posts

**Course:** KIN 7518 Social Issues in Sport  
**Group:** GeauxTigers (Antoine · Areli · Ethan)  
**Due:** April 10, 2026

---

## Overview

This project investigates whether athletes face more positive or negative engagement when making politically charged posts on Instagram. Using a dataset of 11,833 Instagram comments, we applied keyword-based sentiment coding to classify politically engaged comments by tone and compare engagement (likes) across categories.

**Key finding:** Among the 1,848 politically engaged comments (15.6% of all comments), positive comments outnumber negative ones by more than 2-to-1. However, neutral comments attract the highest average likes (20.82), suggesting that observational or measured political responses earn broader audience endorsement than emotionally charged ones.

---

## Repository Structure

```
├── data/
│   └── B50_INS_COMMENT.csv       # Raw Instagram comment dataset (Sheet1)
├── analysis/
│   └── keyword_analysis.py       # Main analysis script (pandas keyword coding)
├── visualizations/
│   ├── GeauxTigers_Charts.html   # Interactive chart file (Chart.js)
│   └── GeauxTigers_Charts.pdf    # Print-ready chart export
├── GeauxTigers_PLAN.md           # Full research plan and methodology
└── README.md
```

---

## Research Question

> Do athletes face more positive or negative engagement when making politically charged posts on social media?

---

## Methodology

### Dataset
Instagram comment data (`B50_INS_COMMENT`) from the *Politics in Sport* dataset. Each row is a comment with a `text` field and a `likes` count.

### Keyword Lists

| Category | Terms | Count |
|----------|-------|-------|
| Political (18 terms) | trump, biden, president, maga, obama, election, vote, republican, democrat, conservative, liberal, kamala, … | 1,848 comments flagged |
| Positive (47 terms) | love, great, amazing, goat, legendary, inspired, champion, … | 414 comments |
| Negative (49 terms) | hate, disgusting, horrible, corrupt, liar, embarrassing, fraud, … | 183 comments |

Lists were built using three combined methods:
1. **Bottom-up word frequency analysis** of the 1,717 politically engaged comments
2. **AFINN sentiment lexicon** cross-referencing for validated coverage
3. **Iterative expansion** — frequent unscored words reviewed and added where sentiment was unambiguous

### Tone Classification
Each politically engaged comment was assigned one of four tone categories:

| Tone | Rule |
|------|------|
| Positive | ≥1 positive keyword, zero negative keywords |
| Negative | ≥1 negative keyword, zero positive keywords |
| Mixed | ≥1 positive and ≥1 negative keyword |
| Neutral | Political keyword present, no positive or negative keywords |

---

## Results

| Tone | Count | % of Political | Avg Likes | Engagement-Weighted Score |
|------|-------|---------------|-----------|--------------------------|
| Neutral | 1,162 | 62.9% | 20.82 | 24,192 |
| Positive | 414 | 22.4% | 6.97 | 2,886 |
| Negative | 183 | 9.9% | 4.37 | 800 |
| Mixed | 89 | 4.8% | 3.91 | 348 |
| **Total** | **1,848** | **100%** | — | — |

**Top political keywords:** trump (1,121) · biden (326) · president (324)  
**Top positive keywords:** good (102) · great (80) · love (78)  
**Top negative keywords:** ew (67) · lie (61) · hate (37)

---

## Running the Analysis

```bash
# Install dependencies
pip install pandas

# Run keyword analysis
python analysis/keyword_analysis.py
```

The script expects `data/B50_INS_COMMENT.csv` encoded as `latin1` (required for non-UTF-8 characters in comment text).

---

## Visualizations

Three coordinated charts address RQ1:

1. **Donut chart** — tone distribution across the 1,848 politically engaged comments
2. **Bar chart** — average likes per comment by tone category
3. **Horizontal bar chart** — political keyword frequency across all 11,833 comments

Open `visualizations/GeauxTigers_Charts.html` in any browser to view the interactive version, or see `GeauxTigers_Charts.pdf` for the print-ready export.

---

## Limitations

- **Platform bias** — Instagram skews younger and more active online; findings may not generalize to all sports fans.
- **Engagement ≠ sentiment** — high like counts on neutral comments may reflect agreement, but could also reflect algorithm amplification.
- **Keyword gaps** — sarcasm, irony, platform slang, and non-English comments are not captured. Future work could apply VADER or a fine-tuned BERT classifier.
- **Temporal clustering** — 1,679+ of the 1,848 political comments concentrated in July 2024, suggesting event-driven spikes that may not represent stable baseline engagement.

---

## AI Assistance

Claude (Anthropic, `claude-sonnet-4-6`) assisted with Python/pandas keyword coding, AFINN-based lexicon expansion, data visualization (Chart.js), and document formatting. All keyword counts and tone classifications were verified by manual spot-check against random comment samples. Engagement-weighted scores were hand-verified (e.g., neutral: 1,162 × 20.82 = 24,192).

---

## Group Roles

| Member | Role | Responsibilities |
|--------|------|-----------------|
| Antoine | Data Lead | Data cleaning, keyword list construction, frequency counts, file management |
| Areli | Theory Lead | Literature integration, RQ refinement, framing, written synthesis |
| Ethan | Methods Lead | Analysis design, coding scheme, tool implementation, cross-tabulation |
