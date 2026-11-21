English | [Türkçe](README.tr.md)

# X Sentiment Analysis

An internship project for the Istanbul Chamber of Commerce (İTO): sentiment analysis of tweets about Istanbul across three topics, **tourism**, **transport** and **inflation**.

## Summary

- **Data:** 571 tweets (original set of 367 plus a pilot set of 204), cleaned of spam, ads and off-topic content.
- **Model comparison:** three Turkish sentiment models (savasy, saribasmetehan and TurkishBERTweet) were compared on a hand-labelled gold standard of 208 rows.
- **Fine-tuning:** the savasy model was retrained on the gold standard with LoRA.

| Metric | Before fine-tuning | After fine-tuning |
|---|---|---|
| Overall accuracy | 61.5% | 81% |
| Negative recall | 86.6% | 90% |
| Neutral recall | 23.9% | 62% |
| Positive recall | 63.6% | 89% |

For the full analysis and charts, open **[dashboard.html](dashboard.html)** in a browser (no internet connection needed). The dashboard is in Turkish.

### A note on these numbers

The two columns are not strictly comparable. The "before" figures were measured on all 208 gold-standard rows. The "after" figures were measured on the 20% of that data held out from training: 42 tweets (20 negative, 13 neutral, 9 positive). On a sample that small, a single tweet moves a class by several points, so read the result as a direction, not a precise gain. Scoring the base model on the same held-out 42 rows would make the comparison fair.

## About the data

The tweet files are not published here: X's developer terms restrict redistributing tweet content, and the files include account identifiers. The notebook's saved outputs were cleared for the same reason. The code, the fine-tuned LoRA adapter and the dashboard are included; to rerun the notebook you need your own collection of tweets in `veri/`.

## Folder structure

```
İTO_sentiment_analysisV2.ipynb   main notebook
dashboard.html                    interactive results dashboard
veri/                             raw and source data (tweet files are not in this repository)
ciktilar/                         generated output files (files containing tweet text are not in this repository)
model/                            fine-tuned LoRA adapter and preprocessing module
eski_denemeler/                   an abandoned alternative model experiment, kept for reference
```

## Methods

- Regex-based cleaning of spam, ads and off-topic tweets
- Turkish-specific preprocessing (the dotted/dotless İ/ı casing problem, stop-word removal)
- Detection of likely irony and sarcasm
- BERT-based sentiment classification (`savasy/bert-base-turkish-sentiment-cased`)
- Parameter-efficient fine-tuning with LoRA (Low-Rank Adaptation)

---
Begüm Çetin, internship assignment

## Contact

Begüm Çetin · begumcetin22@gmail.com · [GitHub](https://github.com/beguumcetin)
