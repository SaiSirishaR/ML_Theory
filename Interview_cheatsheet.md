# Research Scientist / GenAI Interview Master Sheet

---

## 1. RESEARCH

### Deep Dive
- Tell me about your PhD
- Biggest contribution?
- What would you do next?
- How do you evaluate subjective perception?

### Paper Decomposition
- Motivation: Why was this problem important?
- Why had previous work failed?
- Methodology: Why this experimental design?
- Why these metrics / participants / baselines?
- Results: What surprised you?
- What failed?
- Limitations: What are threats to validity?
- Future work: What would you do next with unlimited resources?

### Human-Centered AI
- How do you measure subjective perception scientifically?
- How do you study trust in AI systems?
- What is missing in current GenAI evaluation?

---

## 2. EXPERIMENTATION & SCIENTIFIC METHOD

### Experiment Design
- Hypothesis design
- Dataset creation
- Controls
- Baselines
- Ablation studies
- Error analysis
- Reproducibility

### Statistical Thinking
- Significance testing
- Confidence intervals
- Effect sizes
- ANOVA
- Correlation

### Causal Reasoning
- How do you isolate causal factors?
- What ablations would you run?
- How do you avoid overfitting benchmarks?

---

## 3. RAG (RETRIEVAL-AUGMENTED GENERATION)

### Retrieval
- Dense vs sparse retrieval
- BM25
- Embeddings
- ANN search
- Vector databases

### Chunking
- Chunk size tradeoffs
- Overlap tradeoffs
- Parent-child chunking

### RAG Failures
- Retrieval miss
- Ranking miss
- Context truncation
- Hallucination despite evidence
- Contradictory documents

### Evaluation
- Recall@K
- Precision@K
- MRR
- NDCG

### System Questions
- Why hybrid retrieval?
- Why reranking?
- Why does RAG fail?
- How do you debug correct retrieval but wrong answer?

---

## 4. EVALUATION

### Human Evaluation
- When do you trust humans?
- When do humans disagree?
- Inter-rater reliability
- Pairwise ranking vs Likert scales
- Annotator bias

### LLM Evaluation
- Faithfulness
- Groundedness
- Factuality
- Robustness
- Hallucinations

### LLM-as-a-Judge
- Position bias
- Verbosity bias
- When does it fail?

### Statistical Evaluation
- Significance testing
- Confidence intervals
- Effect sizes
- Correlation vs causation

### Production Evaluation
- Offline evaluation
- Online evaluation
- A/B testing
- Regression testing
- Monitoring

### Meta-Evaluation
- How do you know a metric is valid?
- How do you validate evaluation criteria?
- What makes a good benchmark?

---

## 5. LLMs

### Architecture
- Why transformers?
- Self-attention
- Positional encoding
- Scaling laws

### Training
- Pretraining
- SFT
- RLHF
- DPO
- LoRA

### Prompting
- Zero-shot
- Few-shot
- Chain-of-thought

### Inference
- Temperature
- Top-k
- Top-p
- Beam search

### Reliability
- Hallucinations
- Calibration
- Uncertainty
- Long-context issues

---

## 6. AGENTS

### Core Concepts
- ReAct
- Tool use
- Tool calling

### Planning
- Plan-and-execute
- Reflection
- Tree of Thoughts

### Memory
- Short-term memory
- Long-term memory
- Retrieval memory

### Multi-Agent Systems
- Why multiple agents?
- Failure modes

### Evaluation
- Success rate
- Task completion
- Tool efficiency

---

## 7. SYSTEM DESIGN FOR GENAI

### Design Questions
- Design a RAG system
- Design a customer support assistant
- Design a report generation system
- Design an AI research assistant
- Design an evaluation platform

### Architecture
- Retriever
- Reranker
- LLM
- Post-processing
- Guardrails
- Feedback loops

### Reliability
- Failure detection
- Drift monitoring
- Quality control

### Scaling
- Latency
- Throughput
- Cost optimization

### Debugging
- Why is output wrong?
- How do you trace failure in pipeline?

---

## 8. PRODUCTION GENAI SYSTEMS

### Experimentation
- Prompt versioning
- Model versioning
- Regression testing
- Evaluation pipelines

### Feedback Systems
- Human-in-the-loop
- Feedback storage
- Feedback reuse

### Reliability
- Monitoring
- Drift detection
- Failure analysis

### Structured Outputs
- JSON generation
- Schema validation
- Regeneration workflows

---

## 9. AI ALIGNMENT & SAFETY

### Core Concepts
- What is alignment?
- Why is alignment difficult?

### RLHF / DPO
- Limitations of RLHF
- Reward hacking
- DPO tradeoffs

### Safety Issues
- Jailbreaking
- Red teaming
- Tool misuse

### Evaluation
- How do you evaluate alignment?
- Safety benchmarks

### Research Questions
- What are open problems in AI safety?
- How do we improve current alignment methods?
