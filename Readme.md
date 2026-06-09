# ML Fundamentals

---

## Scenario

You're training a binary classifier and observe:

| Dataset    | Accuracy |
|------------|----------|
| Training   | 99%      |
| Validation | 72%      |

---

### Questions

1. What hypotheses would you form about what is happening?
2. What evidence would you gather to test each hypothesis?
3. What interventions would you try, and in what order?

---

## Analysis

### Possible Causes

---

#### 1. Overfitting

The model may have memorized the training data and failed to generalize to unseen data.

**Evidence to gather:**
- Compare training vs validation learning curves
- Check whether validation loss starts increasing while training loss continues decreasing
- Look for a persistent gap between training and validation performance

---

#### 2. Data Distribution Mismatch

The training and validation datasets may come from different distributions, causing poor generalization.

**Evidence to gather:**
- Inspect how the dataset was split
- Compare feature distributions between training and validation sets
- Verify that preprocessing steps are identical for both datasets
- Check for temporal or sampling bias in the split

---

#### 3. Label Noise

Incorrect or inconsistent labels can significantly reduce validation performance.

**Evidence to gather:**
- Manually inspect a sample of labels
- Look for systematic labeling errors
- Measure inter-annotator agreement if available
- Check for ambiguous or borderline samples

---

### Intervention Order

1. Verify data quality (labels, leakage, corruption)
2. Validate train/validation split strategy
3. Compare feature distributions across datasets
4. Analyze learning curves
5. Apply regularization techniques:
   - Dropout
   - Weight decay (L2 regularization)
6. Reduce model complexity if necessary
7. Collect more data or apply data augmentation

---

## Follow-up Scenario

Suppose you train for 100 epochs and observe:

| Epoch | Train Loss | Validation Loss |
|--------|-----------|----------------|
| 10     | 0.45      | 0.50           |
| 20     | 0.30      | 0.35           |
| 30     | 0.15      | 0.25           |
| 40     | 0.08      | 0.40           |
| 50     | 0.03      | 0.65           |

---

### Questions

1. What do these curves tell you?
2. Which epoch's model would you deploy and why?
3. If management insists on training for all 100 epochs, how would you still obtain a good model?

---

## Interpretation

### What do these curves tell us?

The model learns useful patterns until approximately **epoch 30**.

After that:

- Training loss continues to decrease
- Validation loss starts increasing

This is a classic sign of **overfitting**.

> The model continues improving on training data but loses generalization ability on unseen data.

---

## Which Model Would You Deploy?

You would deploy the model from approximately **epoch 30**.

**Reason:**
- It achieves the lowest validation loss
- Validation performance is the best proxy for real-world performance
- Later epochs overfit the training data

---

## If Training Must Continue to 100 Epochs

Even if training continues, the best model can still be recovered.

### Strategy: Checkpointing + Model Selection

#### 1. Save Checkpoints

Store model weights at regular intervals (e.g., every epoch).

#### 2. Track Validation Loss

Evaluate validation performance after each checkpoint.

#### 3. Select Best Model

After training completes:

```text
Choose the checkpoint with the lowest validation loss
(approximately epoch 30 in this case)
```

This allows you to continue training while still retaining the best-performing model.

---

## Stronger Interview Answer (Additional Techniques)

Other useful techniques include:

- Early stopping
- Learning curves analysis
- Dropout for regularization
- Weight decay (L2 regularization)
- Data augmentation
- Reducing model capacity

---

## Key Interview Takeaway

> Training longer does not necessarily improve performance.
>
> The best model is the one that generalizes best, not the one with the lowest training loss.

---

## Core Concepts

---

## 1. Backpropagation

Backpropagation is an algorithm used to compute the gradient of the loss function with respect to each weight and bias in a neural network.

It works by propagating the error backward from the output layer to the input layer using the chain rule of calculus.

These gradients are then used by optimization algorithms such as SGD or Adam to update the model parameters and minimize loss.

---

## 2. Neural Networks

A neural network is a computational model inspired by the structure of the human brain. It consists of layers of interconnected neurons, where each connection has a learnable weight.

### Training process:

**Forward pass:**
Input data flows through the network to produce predictions, and a loss is computed against the true labels.

**Backward pass (Backpropagation):**
The error is propagated backward through the network to compute gradients.

**Optimization step:**
Gradients are used to update weights using optimizers like SGD, Adam, or Adagrad, improving model performance over time.

---

## 3. Attention Mechanism

### Intuition

Attention allows a model to focus on the most relevant parts of the input when making predictions, rather than treating all inputs equally.

---

### Mechanism

The attention mechanism works by computing relevance scores between different input tokens, converting them into weights, and using those weights to aggregate information.

In Transformer models, this is implemented using:

- Queries (Q)
- Keys (K)
- Values (V)

---

### Formula

```text
Attention(Q, K, V) = softmax(QKᵀ / √d) V
```

---

### Key Idea

- Query = what I am looking for
- Key = what I contain
- Value = actual information content


# Transformers Intuition (Why Each Component Exists)

---

## Why Transformers?

Transformers were introduced because older models like RNNs process words one at a time, which makes them slow and weak at handling long sentences.

The main problem with RNNs is that information has to travel step by step through every word. So if two words are far apart in a sentence, the connection between them becomes weak or even lost. Also, this step-by-step process cannot be parallelized, which makes training slow.

Transformers solve this by removing sequential processing completely. Instead, every word in the sentence can look at every other word at the same time using attention. This makes training much faster and allows the model to directly capture relationships between distant words.

If Transformers didn’t exist, we would still be stuck with slow training and weak long-range understanding.

---

## Why Self-Attention?

Self-attention is used because it allows each word to dynamically decide which other words in the sentence are important for understanding it.

Instead of treating every word equally or relying on fixed structure, self-attention lets the model learn relationships from data.

For example, in a sentence, the meaning of a word often depends on specific other words, not all words equally. Self-attention solves this by letting each word “look around” and pick relevant context.

Without self-attention, the model would either:

- lose context (like bag-of-words models), or  
- struggle to connect distant words (like RNNs)

So the model would not understand context properly.

---

## Why divide by √d in attention?

When we compute attention, we take dot products between Query and Key vectors. As the dimension of these vectors increases, these dot products become very large in magnitude.

When values become large, the softmax function becomes extremely sharp. That means it focuses almost entirely on one word and ignores others. This makes learning unstable because gradients become very small and the model stops learning properly.

Dividing by √d prevents this by keeping values in a reasonable range. It stabilizes training and ensures softmax produces smooth, meaningful weights instead of extreme decisions.

If we did not scale:

- softmax becomes too confident  
- gradients vanish  
- training becomes unstable  

---

## Why multi-head attention?

Single attention is limited because it tries to capture all relationships in one space. But language has multiple types of relationships happening at the same time:

- grammar relationships  
- meaning relationships  
- long-distance dependencies  

One attention mechanism cannot focus on all of these properly at once.

Multi-head attention solves this by creating multiple independent attention mechanisms. Each head learns to focus on different types of relationships. One head might focus on syntax, another on semantic similarity, another on long-range connections.

If we remove multi-head attention:

- the model becomes less expressive  
- it collapses different types of reasoning into one view  
- performance drops because it cannot specialize  

---

## Why positional encoding?

Self-attention does not understand word order. It only sees a set of words, not their sequence.

So without positional encoding, the sentence:

- “dog bites man”  
- “man bites dog”  

would look identical to the model.

Positional encoding fixes this by adding information about where each word is in the sequence. This allows the model to distinguish order and understand structure.

If positional encoding is removed:

- the model becomes permutation-invariant  
- word order is lost  
- grammar and meaning break completely  

So the model becomes a bag-of-words system.

---

## Why LayerNorm?

Deep neural networks become unstable during training because values inside the network can grow too large or too small, making learning difficult.

LayerNorm solves this by normalizing the values inside each token representation so that they stay stable during training.

Unlike BatchNorm, it works independently for each example, which is important because:

- batch sizes can be small  
- sequence lengths vary  
- generation happens one token at a time  

If LayerNorm is removed:

- training becomes unstable  
- gradients explode or vanish  
- model performance becomes inconsistent  

---

## Why residual connections?

As neural networks get deeper, earlier information can get lost, and gradients become harder to propagate backward.

Residual connections solve this by allowing the model to pass information directly from one layer to the next without forcing it to be fully transformed.

So instead of learning a completely new representation, each layer only learns how to refine the existing one.

If residual connections are removed:

- deep models become very hard to train  
- gradients vanish  
- performance collapses with depth  

Residuals make deep Transformers possible.

---

##  Why Feed-Forward Networks after attention?

Self-attention is responsible for mixing information between words. It tells each word what other words are important.

But after that, each word still needs to be processed individually to build richer representations.

That is what the Feed-Forward Network does. It applies a small neural network to each token separately, allowing non-linear transformation and feature refinement.

If FFN is removed:

- the model only mixes information but does not transform it deeply  
- representational power becomes limited  
- performance drops significantly  

So:

- attention = communication between words  
- FFN = computation inside each word  
