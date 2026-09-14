---
title: "NLP GitHub Issue Classifier"
date: 2025-11-20
date_display: "2025"
description: "An automated NLP pipeline to classify and triage open-source repository issues into functional categories based on issue text."
status: "prototype"
domain: "Natural Language Processing"
technologies:
  - "Python"
  - "NLP"
  - "scikit-learn"
  - "Text Preprocessing"
  - "GitHub API"
github: "https://github.com/akattri"
demo: ""
featured: true
weight: 40
---

## Overview

An experimental text classification system built to categorize open-source GitHub issues into labels (`bug`, `feature request`, `documentation`, `question`, `enhancement`) by analyzing the issue title and markdown body.

---

## Why I Built It

Maintainers of active open-source projects frequently spend considerable time reading, sorting, and tagging incoming issue submissions. 

This project explored how classical and modern NLP techniques handle unstructured developer writing, code blocks, stack traces, and informal conversational text to automate issue triage.

---

## What I Learned & Engineering Takeaways

- **Text Preprocessing in Code Contexts**: Standard NLP cleaning (like stripping punctuation or lowercasing everything) can destroy vital technical signal (such as function names, error codes, file paths, and syntax highlights).
- **Class Imbalance Handling**: Real-world bug reports heavily outnumber documentation or question issues, requiring stratified sampling and class-weighted loss metrics to prevent biased predictions.
- **Feature Representation**: Evaluating TF-IDF n-gram vectors against transformer embeddings, noting the tradeoff between inference speed and semantic nuance.

---

## Technical Architecture & Implementation

```
[GitHub Webhook / API] ──> [Text Preprocessor] ──> [TF-IDF / Vectorizer]
                                                            │
                                                            ▼
                                                [Classification Model]
                                                            │
                                                            ▼
                                              [Predicted Triage Label]
```

### Pipeline Details
- Ingests issue JSON payloads via the GitHub REST API.
- Cleans and isolates markdown headers, error traces, and prose.
- Extracts token features and evaluates multinomial naive Bayes and linear SVM classifiers as strong, interpretable baselines.

---

## Future Directions & Open Questions

- **Zero-Shot Fine-Tuning**: Testing lightweight encoder models (e.g. DeBERTa) for zero-shot categorization on uncurated repositories.
- **Automated Duplicate Detection**: Exploring cosine similarity across dense vector embeddings to flag duplicate bug reports.
- [Add technical details here]
