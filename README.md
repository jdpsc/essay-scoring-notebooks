# Automated Essay Scoring Notebooks

This repository contains notebooks for two approaches to the Automated Essay Scoring Kaggle competition. The goal of this competition is to train a model to score student essays efficiently and accurately. A reliable automated scoring system can significantly reduce the time and cost of grading, allowing the inclusion of essay questions in standardized testing, which are crucial indicators of student learning but often avoided due to grading challenges.

Evaluation is based on the [quadratic weighted kappa](https://www.kaggle.com/code/aroraaman/quadratic-kappa-metric-explained-in-5-simple-steps), a metric that measures the agreement between two outcomes.

For more details about the competition, see the [official Kaggle page](https://www.kaggle.com/competitions/learning-agency-lab-automated-essay-scoring-2).

## Approach 1: Fine-tuned DeBERTa-v3-small
- **Base model(s):** deberta-v3-small
- **Methodology:**
  - Used the HuggingFace Trainer API to fine-tune the model.
  - Added new tokens to the tokenizer to handle "new paragraph" and "double space" as DeBERTa removes these from essays.
- **Score:** 0.80

## Approach 2: Multi-LLM Embedding Extraction + LightGBM
- **Base model(s):** deberta-base, deberta-large, deberta-v3-large, longformer-base-4096, bigbird-roberta-base, bigbird-roberta-large
- **Methodology:**
  - Extracted embeddings using the HuggingFace API.
  - Used concatenated embeddings as input for a LightGBM model.
  - Applied threshold post-processing as discussed [here](https://www.kaggle.com/competitions/learning-agency-lab-automated-essay-scoring-2/discussion/502279).
- **Score:** 0.81

## Common Techniques Used in Both Approaches
- **Cross-Validation:** Employed Stratified K-Fold Cross-Validation.
- **Evaluation Metric:** Implemented Quadratic Weighted Kappa (QWK) as the evaluation metric.
