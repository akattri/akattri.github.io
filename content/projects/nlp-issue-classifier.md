---
title: "GitHub Issue Security Classifier"
date: 2025-11-20
date_display: "2025"
description: "An exploratory NLP pipeline using NLTK and Naive Bayes to classify GitHub issues as security-related or non-security."
status: "prototype"
domain: "Natural Language Processing"
technologies:
  - "Python"
  - "NLP / NLTK"
  - "scikit-learn"
  - "TF-IDF Vectorization"
  - "GitHub API"
github: "https://github.com/akattri/github-issue-classifier"
demo: ""
featured: true
weight: 50
---

## Overview

**GitHub Issue Security Classifier** is an exploratory Natural Language Processing pipeline designed to classify open-source repository issues into **security** and **non-security** categories based on issue titles and markdown bodies.

The project investigates whether classical bag-of-words and TF-IDF representations paired with Multinomial Naive Bayes can assist maintainers in prioritizing security-sensitive issue disclosures.

---

## Why I Built It

Maintainers of active open-source projects receive a continuous stream of bug reports, feature suggestions, and documentation edits. Security disclosures and vulnerability reports require expedited triage and confidential patch coordination.

This project was built as an undergraduate machine learning experiment to explore:
- How text preprocessing (URL stripping, tokenization, stopword filtering, and Porter stemming) conditions technical prose for classification.
- The performance of TF-IDF feature extraction on structured developer descriptions.
- The methodological limitations and lexical leakage risks inherent in keyword-queried datasets.

---

## Dataset Provenance & Preprocessing

The dataset ($N = 200$) was harvested from public GitHub repositories using the GitHub REST Search API across four balanced query categories:
- **Security Label Queries**: `label:security` ($n=50$) and `label:vulnerability` ($n=50$).
- **Non-Security Label Queries**: `label:documentation` ($n=50$) and `label:enhancement` ($n=50$).

### Preprocessing Pipeline (NLTK)
1. **URL Elimination**: Regex removal of hyperlinks to prevent domain-specific overfitting.
2. **Text Normalization**: Lowercase conversion and alphabetic token isolation.
3. **Stopword Pruning**: Standard English stopwords removed via NLTK.
4. **Morphological Stemming**: NLTK `PorterStemmer` reducing morphological variations (e.g., `vulnerabilities` &rarr; `vulner`).

---

## Technical Architecture & Model Evaluation

```
[GitHub REST API] ──> [Text Preprocessor] ──> [TF-IDF Vectorizer (1-2 n-grams)]
                                                               │
                                                               ▼
                                                    [Multinomial Naive Bayes]
                                                               │
                                                               ▼
                                                    [Security / Non-Security]
```

### Stratified Evaluation ($80/20$ Split, $N_{\text{test}} = 40$)
- **Overall Accuracy**: $87.5\%$
- **Security Class**: Precision = $0.94$, Recall = $0.80$, F1-Score = $0.86$ ($n=20$)
- **Non-Security Class**: Precision = $0.83$, Recall = $0.95$, F1-Score = $0.88$ ($n=20$)
- **Confusion Matrix**: 19 True Negatives, 1 False Positive, 4 False Negatives, 16 True Positives.

---

## Methodological Limitations & Research Takeaways

An honest assessment reveals key constraints:
1. **Lexical Leakage**: Because training data was sampled using labels like `label:security`, issues frequently contained these exact words in titles, giving the TF-IDF model high lexical cues that may not appear in subtler real-world vulnerability reports.
2. **Sample Size ($N=200$)**: The small sample size serves as an educational pipeline demonstration rather than a generalized, production-ready classifier.
3. **Asymmetric Risk**: In security triage, a false negative rate of $20\%$ (misclassifying a real vulnerability as benign) is operationally costly, indicating that future iterations should incorporate recall-weighted loss functions or probabilistic threshold tuning.
