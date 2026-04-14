# KIN 7518 – Project 3: Political Engagement on Athlete Instagram Posts

**Course:** KIN 7518 Social Issues in Sport  
**Group:** GeauxTigers (Antoine · Areli · Ethan)  
**Status:** Plan phase, submitted April 10, 2026. Report and presentation due later in the semester.

---

## Overview

This project investigates how audience engagement varies across politically charged comments under athletes' Instagram posts. Using a dataset of 11,833 Instagram comments, we apply keyword-based sentiment coding to flag politically engaged comments and classify them by tone, then compare likes across tone categories.

**Preliminary pattern (plan-phase figures, subject to revision):** Of the 1,848 comments flagged by the political keyword list (15.6% of the corpus), positive outnumber negative by roughly 2-to-1, and the Neutral bucket (comments with a political keyword but no sentiment keyword) has the highest mean likes. These are descriptive numbers from a first pass; the Neutral bucket, the likes measure, and any interpretation of why Neutral shows higher engagement will all be audited against a hand sample before the final report.

---

## Repository Structure

```
├── Project 3 - Geaux Tigers KIN 7518.pdf   # Full research plan and methodology
└── README.md
```

The analysis script, visualization files, and raw dataset are maintained locally during the plan phase and are not committed to this repository. Per the P3 brief, the raw `B50_INS_COMMENT` dataset will not be pushed to the public repo at any point. The analysis code and visualization outputs will be committed before the final report.

---

## Research Question

> Do athletes face more positive or negative audience engagement when making politically charged posts on social media?

This is a plan-phase framing and is likely to be tightened before the final report. In particular, the team is still deciding whether the unit of analysis is the comment (likes a comment receives from other commenters) or the post (overall engagement on the athlete's original content), which changes what "audience engagement" means in the RQ.

---

## Methodology

### Dataset
Instagram comment data (`B50_INS_COMMENT`) from the *Politics in Sport* dataset. Each row is a comment with a `text` field and a `likes` count.

### Keyword Lists

| Category | Example terms | Plan-phase count |
|----------|---------------|------------------|
| Political (18 terms) | trump, biden, president, maga, obama, election, vote, republican, democrat, conservative, liberal, kamala, … | 1,848 comments flagged |
| Positive (47 terms) | love, great, amazing, goat, legendary, inspired, champion, … | 414 comments |
| Negative (49 terms) | hate, disgusting, horrible, corrupt, liar, embarrassing, fraud, … | 183 comments |

Lists were built by combining three methods:

1. **Bottom-up word frequency analysis** of the politically engaged comments
2. **AFINN sentiment lexicon** cross-referencing for validated coverage
3. **Iterative expansion**, where frequent unscored words were reviewed and added when sentiment was unambiguous

### Tone Classification
Each politically engaged comment is assigned one of four tone categories:

| Tone | Rule |
|------|------|
| Positive | ≥1 positive keyword, zero negative keywords |
| Negative | ≥1 negative keyword, zero positive keywords |
| Mixed | ≥1 positive and ≥1 negative keyword |
| Neutral | Political keyword present, no positive or negative keywords |

The Neutral category is defined by the absence of sentiment keywords rather than by a positive criterion. Before the final report, the team will hand-sample comments from this bucket to document what it actually contains (e.g., short reactions, questions, emojis, sarcasm) and decide whether to treat it as a substantive tone category or label it as unclassified.

---

## Preliminary Results (Plan Phase)

> These figures come from a first pass of the keyword classifier and are reported so reviewers can see the pipeline running. They are not final. The Neutral bucket definition, the likes measure, the distributional reporting, and the interpretation will all be revised before the final report.

| Tone | Count | % of Political | Mean Likes | Median Likes | IQR |
|------|-------|---------------|-----------|--------------|-----|
| Neutral | 1,162 | 62.9% | 20.82 | TBD | TBD |
| Positive | 414 | 22.4% | 6.97 | TBD | TBD |
| Negative | 183 | 9.9% | 4.37 | TBD | TBD |
| Mixed | 89 | 4.8% | 3.91 | TBD | TBD |
| **Total** | **1,848** | **100%** | — | — | — |

Median and IQR columns will be populated before the final report because likes on social media content are heavily skewed and the mean alone will not describe the distribution fairly.

**Top political keywords:** trump (1,121), biden (326), president (324)  
**Top positive keywords:** good (102), great (80), love (78)  
**Top negative keywords:** ew (67), lie (61), hate (37)

---

## Planned Implementation

The analysis code and visualization outputs are maintained locally during the plan phase and will be committed before the final report:

- `analysis/keyword_analysis.py`: keyword coding pipeline using the three-method lexicon described above, reading the local `B50_INS_COMMENT` CSV (latin1 encoding) and producing the tone counts and likes summary.
- `visualizations/`: a donut chart of the tone distribution, a bar chart of likes per tone (with median and IQR overlays), and a horizontal bar chart of political keyword frequency across the full 11,833-comment corpus.

The raw CSV path will be supplied to the script as a local argument rather than committed to the repo.

---

## Limitations

- **Platform bias.** Instagram skews younger and more active online, so findings may not generalize to all sports fans.
- **Engagement is not sentiment.** High like counts on Neutral-coded comments may reflect agreement, but may also reflect algorithmic amplification or a length-likes correlation that has nothing to do with tone.
- **Keyword gaps.** Sarcasm, irony, platform slang, and non-English comments are not captured by the current lexicon. Future work could apply VADER or a fine-tuned BERT classifier.
- **Temporal clustering.** 1,679 of the 1,848 politically flagged comments concentrate in July 2024, suggesting event-driven spikes rather than a stable baseline. The final report will either scope the analysis to that event window or report within-window and out-of-window patterns separately.
- **Neutral as residual category.** Because Neutral is defined by the absence of sentiment keywords, any interpretation of the Neutral bucket's engagement will require a hand-sample audit before the report.

---

## AI Assistance

Claude (Anthropic, `claude-sonnet-4-6`) assisted with Python and pandas keyword coding, AFINN-based lexicon expansion, data visualization (Chart.js), and document formatting. All keyword counts and tone classifications were checked by manual spot-check against random comment samples. Engagement-weighted arithmetic was hand-verified (e.g., 1,162 × 20.82 ≈ 24,192).

---

## Group Roles

| Member | Role | Responsibilities |
|--------|------|------------------|
| Antoine | Data Lead | Data cleaning, keyword list construction, frequency counts, file management |
| Areli | Theory Lead | Literature integration, RQ refinement, framing, written synthesis |
| Ethan | Methods Lead | Analysis design, coding scheme, tool implementation, cross-tabulation |
