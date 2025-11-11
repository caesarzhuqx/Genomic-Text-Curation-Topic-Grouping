🧬 Genomic Text Curation & Topic Grouping

A lightweight NLP pipeline for 20–100 short biomedical texts (e.g., abstracts).
It extracts variants, genes, diseases, detects simple relations, and groups texts into topics for fast human curation.

Why this project?
Small teams often need a quick, reproducible way to structure small corpora without heavy infrastructure.
This repo provides a practical baseline you can run in minutes.

---

### ⚙️ Setup & Run

#### 🧩 Step 1. Install dependencies
```bash
pip install pandas scikit-learn matplotlib seaborn
pip install sentence-transformers bertopic
