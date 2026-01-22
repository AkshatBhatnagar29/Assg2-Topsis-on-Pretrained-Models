# 📘 Text Sentence Similarity using TOPSIS on Pretrained Hugging Face Models

## 📌 Problem Statement
Text Sentence Similarity is a fundamental task in Natural Language Processing (NLP) that measures how semantically similar two sentences are. It is widely used in applications such as semantic search, plagiarism detection, question answering, and recommendation systems.

Multiple pretrained transformer-based models are available for this task, each with different strengths in terms of accuracy, speed, and resource usage. Selecting the best model based on a single metric is often misleading.

To address this, this project applies **TOPSIS (Technique for Order Preference by Similarity to Ideal Solution)** to rank multiple pretrained Hugging Face models based on conflicting evaluation criteria.

## 🎯 Objective
- Evaluate multiple pretrained sentence similarity models.
- Compare them using performance (correlation) and efficiency (time/size) metrics.
- Apply TOPSIS to rank the models objectively.
- Identify the most optimal model for sentence similarity tasks.

## 🧠 Models Evaluated
The following pretrained Hugging Face models were evaluated as alternatives in the TOPSIS framework:

1. **paraphrase-MiniLM-L6-v2**
2. **all-MiniLM-L6-v2**
3. **multi-qa-MiniLM-L6-cos-v1**
4. **all-distilroberta-v1**
5. **all-mpnet-base-v2**

## 📊 Evaluation Criteria
Each model was evaluated using the following criteria:

| Criterion | Description | Impact |
| :--- | :--- | :--- |
| **Pearson Correlation** | Measures linear correlation with ground truth similarity | Benefit (+) |
| **Spearman Correlation** | Measures rank correlation with ground truth | Benefit (+) |
| **Avg Inference Time** | Average time taken per sentence pair | Cost (−) |
| **Embedding Dimension** | Size of the sentence embeddings | Cost (−) |
| **Model Size (MB)** | Memory footprint of the model | Cost (−) |

## 🧪 Dataset & Methodology
### Dataset
A sentence-pair similarity dataset was used where each data point contains:
- Sentence 1
- Sentence 2
- Ground truth similarity score

### Methodology
1. **Sentence Encoding:** Each sentence pair is encoded using a pretrained transformer model.
2. **Similarity Computation:** Cosine similarity is computed between the embeddings.
3. **Metric Evaluation:** Pearson/Spearman correlations, inference time, and model size are recorded.
4. **TOPSIS Application:** - Normalize the decision matrix.
    - Apply weights to each criterion.
    - Compute distance from ideal best and ideal worst solutions.
    - Calculate TOPSIS score and rank.

## ⚖️ TOPSIS Parameters
- **Weights:** `[0.3, 0.3, 0.15, 0.1, 0.15]`
- **Impacts:** `['+', '+', '-', '-', '-']`

*Higher weight is given to performance metrics (correlations), while efficiency metrics are also considered.*

## 📋 Result Table
The table below shows the performance metrics and the final TOPSIS ranking for each model.

| Rank | Model | Pearson | Spearman | Avg Time (s) | Emb Dim | Size (MB) | TOPSIS Score |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **1** | `paraphrase-MiniLM-L6-v2` | 0.8695 | 0.8705 | 0.0237 | 384 | 90 | **0.9802** |
| **2** | `all-MiniLM-L6-v2` | 0.8696 | 0.8672 | 0.0251 | 384 | 90 | **0.9748** |
| **3** | `multi-qa-MiniLM-L6-cos-v1` | 0.7947 | 0.8046 | 0.0225 | 384 | 90 | **0.8900** |
| **4** | `all-distilroberta-v1` | 0.8829 | 0.8830 | 0.0762 | 768 | 305 | **0.4960** |
| **5** | `all-mpnet-base-v2` | 0.8806 | 0.8811 | 0.1610 | 768 | 420 | **0.1075** |

## 📈 Result Visualization
*(Place your bar graph image here, e.g., `![TOPSIS Ranking Graph](images/graph.png)`)*

The visualization highlights that while larger models (like `all-mpnet-base-v2`) have slightly higher correlation scores, their high computational cost (Time & Model Size) significantly penalizes their TOPSIS rank.

## 🏆 Final Conclusion
Using TOPSIS provides a robust multi-criteria decision-making approach. 

- **Winner:** `paraphrase-MiniLM-L6-v2` emerged as the best overall model.
- **Reasoning:** It strikes the perfect balance between high accuracy (Pearson ~0.87) and high efficiency (low inference time and small model size).
- **Scalability:** This ranking methodology can be easily extended to other NLP tasks and model selections.

---
*Created for the Text Similarity Model Selection Project.*
