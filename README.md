🧬 Genomic Text Curation & Topic Grouping

A lightweight NLP pipeline for 20–100 short biomedical texts (e.g., abstracts).
It extracts variants, genes, diseases, detects simple relations, and groups texts into topics for fast human curation.

Why this project?
Small teams often need a quick, reproducible way to structure small corpora without heavy infrastructure.
This repo provides a practical baseline you can run in minutes.

# 🧬 Genomic Text Curation

This repository provides an end-to-end pipeline for extracting biomedical entities, curating relationships, and performing topic modeling on genomic text data.

---

## ⚙️ Setup & Run

### ✅ Step 1. Install Dependencies

```bash
pip install pandas scikit-learn matplotlib seaborn
pip install sentence-transformers bertopic
🧾 Step 2. Input Format
Create a file at data/text.csv with one column named text.

Example:

csv
Copy code
text
"The APOE ε4 allele increases the risk of Alzheimer’s disease."
"Variants rs429358 and rs7412 define APOE isoforms associated with AD."
🚀 Step 3. Run Notebook
Open genomic_text_curation.ipynb in Jupyter or Google Colab,
then execute all cells sequentially.

📤 Outputs Generated
After running successfully, the following files will be created:

Output File	Description
extracted_entities_full.csv	Extracted biomedical entities and their metadata
curated_results.json	Curated relationships and entity summaries
topic_model_tfidf.csv	Topic modeling results using TF-IDF
topic_model_bertopic.csv	Topic modeling results using BERTopic

Plots are automatically saved under images/, e.g.:

kmeans_topics.png

bertopic_topics.png

🧩 Notes
Ensure the data/ and images/ directories exist before running.

The script uses pre-trained SentenceTransformers embeddings.

BERTopic visualization may take several minutes depending on data size.

📚 Citation
If you use this pipeline in your research, please cite the repository or acknowledge the method in your paper.

🧑‍💻 Author
Maintained by Qixuan Zhu
M.S.E. Data Science, University of Pennsylvania

yaml
Copy code

---
