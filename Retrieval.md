# RAG Pipeline

## Document Ingestion

```text
              PDF / HTML / Docs / Markdown
                        │
                        ▼
              Text extraction / cleaning
                        │
                        ▼
                 Chunking (+ overlap)
                        │
                        ▼
              Metadata attachment
      (source, page, section, timestamp)
                        │
                        ▼
                Embedding generation
                        │
                        ▼
         Vector index (FAISS, HNSW, Pinecone, etc.)
```

---

## Query Time

```text
User Question
      │
      ▼
Query preprocessing
(lowercase, rewrite, filters, etc.)
      │
      ▼
Query embedding
      │
      ▼
Similarity search
(cosine similarity / ANN)
      │
      ▼
Top-K candidate chunks
      │
      ▼
(Optional) Reranker
(cross-encoder)
      │
      ▼
Top-N chunks
      │
      ▼
Context assembly
      │
      ▼
LLM
```


# Edge cases

### If chunk size and overlap are same

chunk_size = 5
overlap = 5

what happens to?

step = chunk_size - overlap

Add this line:

```python
if overlap >= chunk_size:
   raise ValueError("overlap must be smaller than chunk_size")
```

### If chunk size is less than overlap

overlap > chunk_size

chunk_size = 5
overlap = 6


A negative step means "count backwards." But since you're starting at 0 and trying to go up to len(words), the range is empty


so write value error line for both overlap = chunk size and overlap > chunk size
