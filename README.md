# Question answering-DistilBERT、RoBERTa、XLNet


### Goal
Comparing the performance of different BERT models on QA tasks.


### Dataset
https://huggingface.co/datasets/rajpurkar/squad_v2

Stanford Question Answering Dataset (SQuAD) is a reading comprehension dataset, consisting of questions posed by crowdworkers on a set of Wikipedia articles, where the answer to every question is a segment of text, or span, from the corresponding reading passage, or the question might be unanswerable.

SQuAD 2.0 combines the 100,000 questions in SQuAD1.1 with over 50,000 unanswerable questions written adversarially by crowdworkers to look similar to answerable ones. To do well on SQuAD2.0, systems must not only answer questions when possible, but also determine when no answer is supported by the paragraph and abstain from answering.

```
This example was too long and was cropped:

{
    "answers": {
        "answer_start": [94, 87, 94, 94],
        "text": ["10th and 11th centuries", "in the 10th and 11th centuries", "10th and 11th centuries", "10th and 11th centuries"]
    },
    "context": "\"The Normans (Norman: Nourmands; French: Normands; Latin: Normanni) were the people who in the 10th and 11th centuries gave thei...",
    "id": "56ddde6b9a695914005b9629",
    "question": "When were the Normans in Normandy?",
    "title": "Normans"
}
```

### Evaluation

* Exact Match <br>
This metric is as simple as it sounds. For each question+answer pair, if the characters of the model's prediction exactly match the characters of (one of) the True Answer(s), EM = 1, otherwise EM = 0. This is a strict all-or-nothing metric; being off by a single character results in a score of 0. When assessing against a negative example, if the model predicts any text at all, it automatically receives a 0 for that example.

* F1 Score <br>
F1 score is a common metric for classification problems, and widely used in QA. It is appropriate when we care equally about precision and recall. In this case, it's computed over the individual words in the prediction against those in the True Answer. The number of shared words between the prediction and the truth is the basis of the F1 score: precision is the ratio of the number of shared words to the total number of words in the prediction, and recall is the ratio of the number of shared words to the total number of words in the ground truth.

$$
F1 \; Score = \frac{2 \cdot \text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}
$$

$$
\text{Precision} = \frac{TP}{TP + FP}
$$

$$
\text{Recall} = \frac{TP}{TP + FN}
$$



### Results
The results indicate that RoBERTa outperforms the other models in both metrics, achieving the highest Exact Match score of **0.656** and the highest F1 score of **0.73**. XLNet follows with an Exact Match of 0.636 and an F1 score of 0.72, while DistilBERT lags behind, showing significantly lower performance with an Exact Match of 0.492 and an F1 score of 0.57. This suggests that RoBERTa is the most effective model among the three for this QA task.
| Model      | Exact Match | F1 Score |
|------------|-------------|----------|
| DistilBERT | 0.492       | 0.57     |
| XLNet      | 0.636       | 0.72     |
| **RoBERTa**    | **0.656**      | **0.73**     |

