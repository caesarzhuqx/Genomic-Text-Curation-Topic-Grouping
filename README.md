# 🧬 Genomic Text Curation & Topic Grouping

A lightweight NLP pipeline for 20–100 short biomedical texts (e.g., abstracts).  
It extracts **variants**, **genes**, **diseases**, detects **simple relations**, and groups texts into topics for fast human curation.

---

### ❓ Why This Project

Small teams often need a quick, reproducible way to structure small corpora without heavy infrastructure.  
This repository provides a **practical baseline** you can run in minutes.

## ⚙️ Setup & Run

✅ **Step 1. Install Dependencies**

pip install pandas scikit-learn matplotlib seaborn
pip install sentence-transformers bertopic

vbnet
Copy code

🧾 **Step 2. Input Format**  
Create a file at `data/text.csv` with one column named `text`.

Example:

text
"The APOE ε4 allele increases the risk of Alzheimer’s disease."
"Variants rs429358 and rs7412 define APOE isoforms associated with AD."

markdown
Copy code

🚀 **Step 3. Run Notebook**  
Open `genomic_text_curation.ipynb` in **Jupyter** or **Google Colab**,  
then execute all cells sequentially.

**Outputs generated:**
- `extracted_entities_full.csv`
- `curated_results.json`
- `topic_model_tfidf.csv`
- `topic_model_bertopic.csv`

Plots are saved under `images/` (e.g., `kmeans_topics.png`, `bertopic_topics.png`)

## 🧠 Description of Extraction and Topic Methods

### 🧬 1. Entity Extraction

Each input sentence is processed using **regular expressions** and **SpaCy’s biomedical language model** to extract structured entities.  
The extraction focuses on three major categories:

| Entity Type | Example | Detection Method |
|--------------|----------|------------------|
| Variant IDs | `rs429358`, `rs7412` | Regex pattern `r'rs\d+'` |
| Gene Symbols | `APOE`, `APP`, `MAPT` | Uppercase word filtering + biomedical lexicon |
| Diseases | `Alzheimer’s disease`, `Type 2 Diabetes` | SpaCy named entity recognition + capitalization heuristics |

All extracted entities are stored in `extracted_entities_full.csv` with columns:  
`text`, `gene`, `variant`, `disease`, and `relation_context`.

---

### 🧩 2. Relation Detection

Simple **pattern-based matching** is used to infer possible relations between entities.  
For instance:

- `"APOE ε4 allele increases the risk of Alzheimer’s disease"`  
  → Relation: *(gene → disease)*  
- `"Variants rs429358 and rs7412 define APOE isoforms"`  
  → Relation: *(variant → gene)*  

These extracted relations are saved in `curated_results.json` for downstream curation.

---

### 🧠 3. Topic Modeling

Two topic modeling pipelines are implemented for flexibility and comparison:

| Method | Vectorization | Clustering | Output File |
|--------|----------------|-------------|--------------|
| **TF-IDF + KMeans** | scikit-learn `TfidfVectorizer` | `KMeans(n_clusters=k)` | `topic_model_tfidf.csv` |
| **BERTopic** | Sentence-BERT embeddings (`all-MiniLM-L6-v2`) | HDBSCAN + UMAP | `topic_model_bertopic.csv` |

Each document is represented in embedding space and grouped into semantically coherent clusters.  
Visualization plots (e.g. `kmeans_topics.png`, `bertopic_topics.png`) show keyword distributions and topic similarity.

---

### 📊 4. Outputs Summary

| File | Description |
|------|--------------|
| `extracted_entities_full.csv` | Raw entities and their occurrence contexts |
| `curated_results.json` | JSON mapping of detected relations |
| `topic_model_tfidf.csv` | TF-IDF topic assignments per text |
| `topic_model_bertopic.csv` | BERTopic clustering and probabilities |

---

### ⚡ 5. Reproducibility

All methods are deterministic given the same random seed.  
Both pipelines can be reproduced by running:

```bash
python scripts/run_extraction.py
python scripts/run_topic_modeling.py
****

## 🧾 Curation Schema (Fields and Why They Matter)

> 🧩 This section describes the structure of curated outputs and why each field is important for downstream interpretation.

🧬 1. extracted_entities_full.csv
This file contains one row per processed sentence, with extracted entities and contextual information.

Field	Type	Example	Why It Matters
text_id	int	12	Unique identifier for cross-referencing.
text	str	"The APOE ε4 allele increases the risk of Alzheimer’s disease."	Retains original context for verification.
gene	str	APOE	Links extracted variants to known genetic markers.
variant	str	rs429358	Enables variant-level genomic analysis.
disease	str	Alzheimer’s disease	Connects genetic entities to clinical outcomes.
relation_context	str	"APOE ε4 increases the risk of AD"	Captures linguistic evidence of relationships.

🧩 2. curated_results.json
Encodes entity–relation triples extracted from text, designed for integration with knowledge graphs or downstream reasoning tools.

Example:
{
"relation_id": 5,
"gene": "APOE",
"variant": ["rs429358", "rs7412"],
"disease": "Alzheimer’s disease",
"relation_type": "gene–disease association",
"source_text": "Variants rs429358 and rs7412 define APOE isoforms associated with AD."
}

Field	Type	Why It Matters
relation_id	int	Enables linking across outputs.
gene	str	Biological anchor for mapping to ontology.
variant	list[str]	Captures multiple polymorphisms.
disease	str	Target phenotype entity.
relation_type	str	Describes the inferred semantic relation.
source_text	str	Preserves textual evidence for human validation.

📊 3. Topic Model Outputs
Summarizes clustering results from topic modeling pipelines.

File	Key Fields	Purpose
topic_model_tfidf.csv	text_id, topic_id, top_keywords	Interpretable topic clusters from TF-IDF + KMeans.
topic_model_bertopic.csv	text_id, topic_id, topic_prob, representative_terms	Semantic clusters derived from Sentence-BERT embeddings.

🧠 Why This Schema Matters

Bridges unstructured biomedical text with structured, machine-readable data.

Enables downstream analytics like gene–disease association mining or variant co-occurrence detection.

Ensures transparency — every record links back to its source text.

Ready for integration into knowledge graphs, annotation dashboards, or visualization pipelines.

yaml
Copy code
---
