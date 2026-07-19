# 🔬 Research Insights Platform

A Google Colab notebook that goes beyond simple semantic search — it analyzes machine learning research papers and generates useful insights: summaries, keywords, named entities, cross-topic comparisons, and dataset-level statistics.

Built as a portfolio project to demonstrate practical NLP engineering: embeddings, vector search, summarization, keyword extraction, and NER combined into one coherent analysis pipeline.

---

## ✨ Features

| Feature | Description |
|---|---|
| **Semantic Search** | Find papers by meaning, not just keywords, using sentence embeddings + FAISS |
| **Summarization** | Auto-generate short summaries of retrieved abstracts |
| **Keyword Extraction** | Pull the top 5 keywords/keyphrases from each paper using KeyBERT |
| **Named Entity Recognition** | Detect Models, Organizations, Technologies, Datasets, and Researchers |
| **Research Insights** | Aggregate most common keywords/entities across a set of search results |
| **Topic Comparison** | Compare two research topics side-by-side (keywords, entities, similarity) |
| **Research Statistics** | Summary stats — avg abstract length, avg similarity, most frequent keyword/entity |

---

## 🗂 Dataset

[`CShorten/ML-ArXiv-Papers`](https://huggingface.co/datasets/CShorten/ML-ArXiv-Papers) from HuggingFace — machine learning papers with `title` and `abstract` fields. The notebook uses a subset of ~15,000 papers for fast execution in Colab.

---

## 🧠 Models & Libraries

- **Embeddings:** `sentence-transformers` — `all-MiniLM-L6-v2`
- **Vector Search:** `faiss-cpu` (`IndexFlatIP` / cosine similarity on normalized vectors)
- **Summarization:** `transformers` — `sshleifer/distilbart-cnn-12-6`
- **Keyword Extraction:** `KeyBERT`
- **NER:** `spaCy` — `en_core_web_sm`
- **Data handling:** `pandas`, `numpy`, `datasets`

---

## 🚀 How to Run

1. Open the notebook in [Google Colab](https://colab.research.google.com/).
2. Run all cells top to bottom (**Runtime → Run all**). A GPU runtime is recommended but not required.
3. The notebook will:
   - Install dependencies
   - Load and clean the dataset
   - Generate embeddings and build the FAISS index
   - Load the summarization, keyword extraction, and NER models
4. Try it yourself by editing the query variables, e.g.:
   ```python
   user_query = "transformer models for text classification"
   enriched_results = display_enriched_results(user_query, top_k=5)
   ```

No API keys, no external services, and no UI framework required — everything runs inside the notebook.

---

## 📓 Notebook Structure

**Part 1 — Backend Foundation**
1. Install libraries
2. Load dataset & convert to DataFrame
3. Clean text and build `paper_text`
4. Generate embeddings with SentenceTransformer
5. Build FAISS index
6. `semantic_search(query, top_k)` — core search function

**Part 2 — Research Insights**
7. `summarize_paper(text)` — abstractive summarization
8. `extract_keywords(text)` — top-5 keyword extraction
9. `extract_entities(text)` — NER across 5 entity types
10. `display_enriched_results(query, top_k)` — search + summary + keywords + entities per paper
11. `generate_insights(results)` — most common keywords/entities/technologies/organizations/datasets
12. `compare_topics(topic1, topic2)` — side-by-side topic comparison
13. `research_statistics(results)` — aggregate stats over a result set

---

## 📌 Example Output

```
Search Query: "transformer models for text classification"

Result 1
Title: ...
Similarity Score: 0.7421
Abstract: ...

Summary: ...
Top Keywords: transformer, text classification, attention, fine-tuning, bert
Entities:
  Models: bert, transformer
  Technologies: natural language processing
  Datasets: glue
```

---

## 🔧 Reusable Core Functions

```python
semantic_search(query, top_k=5)
summarize_paper(text)
extract_keywords(text, top_n=5)
extract_entities(text)
generate_insights(results)
compare_topics(topic1, topic2, top_k=5)
research_statistics(results)
```

---

## ⚠️ Notes & Limitations

- Entity categorization for Models/Technologies/Datasets uses a curated term list combined with spaCy's `ORG`/`PERSON` detection — it's a lightweight heuristic, not a trained domain-specific NER model.
- Embeddings and the FAISS index are held in memory for the session; re-run the notebook (or persist to disk) to reuse them in a new session.
- Built and tested for a single-notebook Colab workflow — no backend server, API, or UI.

---

## 📄 License

This project is for educational/portfolio purposes. Dataset and model licenses belong to their respective owners (HuggingFace, arXiv, Anthropic/Facebook/spaCy model authors, etc.).
