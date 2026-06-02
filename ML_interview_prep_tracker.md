# ML Interview Preparation Tracker

## Core ML Fundamentals

### 1. Overfitting vs Underfitting
- Definitions
- Symptoms in training/validation curves
- Bias-variance tradeoff
- Regularization techniques:
  - Dropout
  - Weight decay (L2)
  - Early stopping
  - Data augmentation

---

### 2. Data Leakage
Understand:
- Label leakage
- Train/validation contamination
- Future information leakage
- Leakage through preprocessing pipelines

Checklist:
- Verify splits
- Verify feature generation
- Verify preprocessing

---

### 3. Training / Validation / Test Sets

| Dataset | Purpose |
|----------|----------|
| Training | Learn parameters |
| Validation | Model selection & hyperparameter tuning |
| Test | Final unbiased evaluation |

Common interview question:
- Why should the test set not be used during model development?

---

### 4. Learning Curves

Know how to diagnose:
- Overfitting
- Underfitting
- Data limitations
- Optimization issues

Example:

Train loss ↓
Validation loss ↓ then ↑

Interpretation:
- Overfitting

---

## Neural Networks

### 5. Neural Networks

Definition:

A neural network is a parameterized function composed of layers of interconnected neurons. During the forward pass it transforms inputs into predictions. During training, backpropagation computes gradients of a loss function with respect to the network parameters, and an optimizer updates those parameters to improve performance.

Topics:
- Input layer
- Hidden layers
- Output layer
- Weights and biases
- Activation functions

---

### 6. Backpropagation

Definition:

Backpropagation computes the gradient of the loss with respect to every trainable parameter by repeatedly applying the chain rule from the output layer back to the input layer.

Important:
- Backpropagation computes gradients
- Optimizers update parameters

Know:
- Chain rule
- Computational graph
- Gradient flow

---

### 7. Gradient Descent

Know:
- Batch Gradient Descent
- Stochastic Gradient Descent (SGD)
- Mini-batch SGD

Questions:
- Why mini-batches?
- Why shuffle data?

---

### 8. Adam vs SGD

SGD:
- Simpler
- Often better final generalization

Adam:
- Adaptive learning rates
- Faster convergence

Interview question:
- When might you choose SGD over Adam?

---

### 9. Learning Rate

Know:
- Too high → divergence
- Too low → slow convergence

Concepts:
- Learning-rate schedules
- Warmup
- Cosine decay

---

### 10. Vanishing & Exploding Gradients

Know:
- Causes
- Symptoms
- Mitigation

Solutions:
- Residual connections
- Normalization
- Better initialization

---

## Attention & Transformers

### 11. Attention

Intuition:

Attention allows a model to focus on the most relevant parts of the input rather than treating every token equally.

Mechanism:

1. Compute similarity scores
2. Apply softmax
3. Generate weighted combination of values

Know:
- Queries
- Keys
- Values

---

### 12. Self-Attention

Understand:
- Every token attends to every other token
- Captures long-range dependencies

Complexity:

O(n²) with respect to sequence length

Common interview question:

What is the main computational bottleneck in transformers?

Answer:
- Quadratic attention matrix

---

### 13. Why Transformers Beat RNNs

Key idea:

RNNs must propagate information sequentially.

Transformers:

- Direct token-to-token communication
- Better long-range dependency modeling
- Highly parallelizable

---

### 14. Positional Encoding

Why needed:
- Self-attention alone has no notion of token order

Understand:
- Sinusoidal encodings
- Learned positional embeddings

---

## Model Evaluation & Debugging

### 15. Diagnosing High Train / Low Validation Performance

Possible causes:

1. Overfitting
2. Data leakage
3. Distribution mismatch
4. Label noise

Investigation order:

1. Verify metrics
2. Check leakage
3. Verify splits
4. Inspect labels
5. Analyze learning curves

---

### 16. Distribution Shift

Know:
- Covariate shift
- Label shift
- Concept drift

Questions:
- Why do models fail after deployment?
- How do you detect distribution shift?

---

### 17. Label Noise

Investigate:
- Incorrect annotations
- Ambiguous labels

Metrics:
- Human review
- Inter-annotator agreement

---

## Scaling & LLMs

### 18. Scaling Laws

Understand trade-offs between:

- Model size
- Dataset size
- Compute budget

Question:

Why does increasing model size often improve performance?

---

### 19. Emergent Capabilities

Know:
- Smooth loss improvements
- Sudden capability improvements

Examples:
- Reasoning
- Translation
- Tool use

---

### 20. Data vs Model Scaling

Tradeoffs:

Large model + little data:
- Overfitting
- Memorization

Small model + lots of data:
- Capacity limitations

Understand compute-optimal training.

---

## Research Thinking

### 21. Hypothesis-Driven Debugging

Structure answers as:

1. Hypotheses
2. Evidence
3. Experiments
4. Interventions

---

### 22. Experimental Design

Practice answering:

- What evidence would support your hypothesis?
- What experiment would falsify it?
- What would you try next?

---

## Interview Checklist

Be able to explain confidently:

- [ ] Overfitting vs underfitting
- [ ] Bias-variance tradeoff
- [ ] Data leakage
- [ ] Learning curves
- [ ] Backpropagation
- [ ] SGD
- [ ] Adam
- [ ] Learning rate
- [ ] Vanishing gradients
- [ ] Exploding gradients
- [ ] Attention
- [ ] Self-attention
- [ ] Transformers vs RNNs
- [ ] Positional encoding
- [ ] Distribution shift
- [ ] Label noise
- [ ] Scaling laws
- [ ] Emergent abilities
- [ ] Experimental design
- [ ] Research reasoning

