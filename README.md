# Detecting Riboswitches with Diffusion + SOFM

**Murphy Angelo & Cyrus Tau**

## Overview

RNA flexibility is a key challenge in predicting RNA structures and is the defining characteristic of riboswitches, which show promise as selective gene regulation platforms. This project combines a diffusion model with Self-Organizing Feature Maps (SOFMs) to detect riboswitches from sequence data.

## Approach

1. **Structure generation** — A diffusion model generates 5,000 predicted structures (as L×L binary contact matrices) for each of 4,053 riboswitch sequences and 4,053 shuffled controls (~8,000 sequences total).
2. **Graph embedding** — Each contact matrix is converted to a graph, and Graph2Vec produces 128-dimensional embeddings summarizing the structural ensemble for each sequence.
3. **Conformational clustering** — A 2×2 SOFM is trained on the Graph2Vec embeddings to quantify how many alternative conformations each sequence adopts, capturing the hallmark flexibility of riboswitches.
4. **Classification** — Features (base-pair probability, SOFM quantization error) are fed into a logistic regression classifier with elastic-net regularization, evaluated via leave-one-family-out cross-validation across 25 riboswitch families.

## Key Results

- **Cross-validated AUC: 0.779** and **F1: 0.783** for riboswitch vs. shuffled-sequence classification.
- The method achieves **state-of-the-art performance** compared to the established Goodarzi et al. approach on overlapping riboswitch families.
- Structural ensemble diversity (captured by the SOFM) is a discriminative signal: riboswitches exhibit more conformational heterogeneity than shuffled controls.

## Dependencies

- `numpy`, `scipy`, `matplotlib`, `pandas`
- `networkx`, `karateclub` (Graph2Vec)
- `minisom` (Self-Organizing Maps)
- `scikit-learn` (logistic regression, metrics)
- `joblib` (parallel computation)
