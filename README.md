<img width="160" height="179" alt="image" src="https://github.com/user-attachments/assets/36f68cc1-1194-4445-998d-52116e196fff" />

# 1-Hop Question Answering & Similar Fact Retrieval in Knowledge Graphs

This project provides a custom implementation of two classic knowledge graph embedding models, **TransE** and **TransR**, to perform two key tasks: 1-hop Question Answering (link prediction) and Similar Fact Retrieval. The models are built from scratch using PyTorch and evaluated on the standard `Nations` and `Kinships` datasets provided by the `pykeen` library.

---

## Project Tasks

The primary objectives accomplished in this notebook are:
1.  **Implement TransE and TransR:** Build the models from the ground up, including their unique scoring functions and training loops.
2.  **Perform 1-Hop Question Answering:** Use the trained models to infer missing head or tail entities in test triplets (e.g., `(?, relation, tail)` or `(head, relation, ?)`).
3.  **Evaluate and Compare:** Rigorously evaluate the performance of both models using standard link prediction metrics (Mean Rank and Hits@10).
4.  **Perform Similar Fact Retrieval:** Design an unsupervised system to find the top-5 most similar facts for a given query fact using vector embeddings and dot-product similarity.

---

## Datasets Used

-   **Nations:** A small knowledge graph with 14 entities (countries), 55 relations (political relationships), and 1,992 triples.
-   **Kinships:** A dataset describing kinship relationships between 104 members of the Australian Alyawarra tribe with 26 relationship types and 10,686 triples.

---

## Methodology

### Model Implementation
-   **Embedding Dimension:** 100 for Question Answering, 30 for Fact Retrieval.
-   **Optimizer:** Adam with a learning rate of 0.001.
-   **Loss Function:** Margin-based ranking loss.
-   **Negative Sampling:** A custom implementation of Bernoulli Negative Sampling was used to generate negative triples for training, corrupting either the head or tail based on relation-specific probabilities.

### Evaluation Metrics
-   **Mean Rank (MR):** The average rank of the correct entity when scored against all other possible entities. *(Lower is better.)*
-   **Hits@10:** The proportion of correct entities that appear in the top-10 ranked results. *(Higher is better.)*

### Final Results on Nations Dataset

| Model | Mean Rank (MR) | Hits@10 |
| :--- | :---: | :---: |
| **TransE** | **7.83** | **73.88%** |
| **TransR** | 7.93 | 71.89% |

### Final Results on Kinships Dataset

| Model | Mean Rank (MR) | Hits@10 |
| :--- | :---: | :---: |
| TransE | 18.87 | 38.59% |
| **TransR** | **14.85** | **46.00%** |

---
