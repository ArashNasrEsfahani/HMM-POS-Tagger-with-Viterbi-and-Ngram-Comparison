# 🏷️ Part-of-Speech Tagging with N-Gram Markov Models

This project implements a robust Part-of-Speech (POS) tagger from scratch using a Hidden Markov Model (HMM) framework. It explores and compares three n-gram models (Unigram, Bigram, and Trigram) to assign the most probable sequence of POS tags to a sentence, with decoding performed by the Viterbi algorithm.

## 📝 Project Overview

The core task is to build a statistical model that can accurately predict the POS tag (e.g., Noun, Verb, Adjective) for each word in a given text. This is achieved by calculating emission and transition probabilities from a tagged training corpus and then finding the optimal tag sequence for new, untagged sentences.

### Models Implemented
The project constructs and evaluates three models with increasing contextual complexity:

1.  **Unigram Model**: The simplest approach. It tags words based only on emission probabilities `P(word|tag)` and the base probability of the tag `P(tag)`. It ignores the context of surrounding tags.
2.  **Bigram Model**: A more context-aware model that considers the previous tag. It uses the transition probability `P(tag_i | tag_i-1)`.
3.  **Trigram Model**: The most complex model, considering the two previous tags to predict the current one. It uses the transition probability `P(tag_i | tag_i-2, tag_i-1)`.

### Key Algorithms & Techniques
-   **Viterbi Algorithm**: At the heart of the tagger, this dynamic programming algorithm efficiently computes the most likely sequence of hidden states (tags) given a sequence of observations (words).
-   **Laplace Smoothing**: Applied to emission probabilities to handle the data sparsity problem, ensuring that words not seen during training can still be assigned a tag.
-   **Parallel Processing**: Implemented for the Trigram model's evaluation to mitigate its heavy computational cost and long processing time.

---

## 📊 Evaluation and Results

The models were trained on ~80% of the provided dataset and evaluated on the remaining ~20% (the validation set). Performance was measured by accuracy and the time taken for evaluation.

| Model | Accuracy (%) | Evaluation Time |
|---|---|---|
| **Unigram** | **94.89%** | **13 seconds** |
| Bigram | 93.88% | 4 minutes 30 seconds |
| Trigram | 93.93% | Approx. 3 hours 14 minutes|

### Conclusion
Surprisingly, the **Unigram model achieved the highest accuracy**. This result highlights a key challenge in statistical NLP: data sparsity.

-   The Bigram and Trigram models, while theoretically more powerful, likely suffered from overfitting. The training data was not large enough to reliably estimate the vast number of tag-pair and tag-triplet probabilities, leading to poorer generalization on unseen data.
-   The Unigram model, due to its simplicity, was more robust and less prone to overfitting, making it the best choice for this specific dataset.

The best model (Unigram) was then used to tag the final `test_notags.txt` file.

---

## 🚀 How to Run

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ArashNasrEsfahani/HMM-POS-Tagger-with-Viterbi-and-Ngram-Comparison
    cd HMM-POS-Tagger-with-Viterbi-and-Ngram-Comparison
    ```

2.  **Create a virtual environment and install dependencies:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    pip install -r requirements.txt
    ```

3.  **Run the Jupyter Notebook:**


## 🛠️ Technologies Used

-   Python 3.x
-   Standard Libraries (`collections`, `multiprocessing`)
-   NumPy (for potential numerical operations)
-   NLTK (optional, for tokenization or comparison)
-   Jupyter Notebook (for demonstration)
