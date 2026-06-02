# ML Fundamentals

## Scenario

You're training a binary classifier and observe:

| Dataset | Accuracy |
|----------|----------|
| Training | 99% |
| Validation | 72% |

### Questions

1. What hypotheses would you form about what's happening?
2. What evidence would you gather to test each hypothesis?
3. What interventions would you try, and in what order?

---

## Analysis

### Possible Causes

#### 1. Overfitting

The model may have memorized the training data and failed to generalize.

**Evidence to gather:**
- Compare training vs validation learning curves
- Check whether validation loss starts increasing while training loss continues decreasing

#### 2. Data Distribution Mismatch

Training and validation datasets may come from different distributions.

**Evidence to gather:**
- Inspect how data was split
- Compare feature distributions between training and validation datasets
- Verify that preprocessing is identical across both datasets

#### 3. Label Noise

Incorrect labels can hurt validation performance.

**Evidence to gather:**
- Manually inspect a sample of labels
- Look for systematic labeling errors
- Measure inter-annotator agreement if available

### Intervention Order

1. Verify data quality and labels
2. Check train/validation split and feature distributions
3. Analyze learning curves
4. Apply regularization (dropout, weight decay)
5. Reduce model complexity if necessary
6. Collect additional training data

---

## Follow-up Scenario

Suppose you train for 100 epochs and observe:

| Epoch | Train Loss | Validation Loss |
|--------|-----------|----------------|
| 10 | 0.45 | 0.50 |
| 20 | 0.30 | 0.35 |
| 30 | 0.15 | 0.25 |
| 40 | 0.08 | 0.40 |
| 50 | 0.03 | 0.65 |

### Questions

1. What do these curves tell you?
2. Which epoch's model would you deploy and why?
3. If management insists on training for all 100 epochs, how could you still obtain a good model?

---

## Interpretation

### What do these curves tell us?

The model learns useful patterns up to approximately **epoch 30**.

After that:

- Training loss continues to decrease
- Validation loss begins to increase

This is a classic sign of **overfitting**.

> [!NOTE]
> The model keeps improving on the training set while its ability to generalize to unseen data deteriorates.

---

## Which Model Would You Deploy?

**Deploy the model from approximately epoch 30.**

Reason:

- It has the lowest validation loss
- Validation performance is the best estimate of real-world performance
- Lower training loss after epoch 30 does not translate into better generalization

---

## If Training Must Continue to 100 Epochs

Even if training continues, you can still recover the best-performing model.

### Strategy: Checkpointing + Model Selection

#### 1. Save Checkpoints

Store model weights at every epoch (or every N steps).

#### 2. Track Validation Loss

Evaluate validation performance after each checkpoint.

#### 3. Select the Best Checkpoint

After training completes:

```text
Choose the checkpoint with the lowest validation loss
(approximately epoch 30 in this example)
```

This provides the benefits of early stopping without actually terminating training.

---

## Stronger Interview Answer

Additional techniques worth mentioning:

- Early stopping as a regularization method
- Learning curves for diagnosing overfitting
- Dropout
- Weight decay (L2 regularization)
- Data augmentation
- Reducing model capacity

---

## Key Interview Takeaway

> [!IMPORTANT]
> Training longer is not necessarily better.
>
> Model selection should be based on validation performance, not training performance.

The best model is often the one that generalizes best, not the one with the lowest training loss.
