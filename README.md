🧬 Genomic Text Curation & Topic Grouping

A lightweight NLP pipeline for 20–100 short biomedical texts (e.g., abstracts).
It extracts variants, genes, diseases, detects simple relations, and groups texts into topics for fast human curation.

Why this project?
Small teams often need a quick, reproducible way to structure small corpora without heavy infrastructure.
This repo provides a practical baseline you can run in minutes.

⚙️ Setup & Run
🧩 Step 1. Install dependencies
pip install pandas scikit-learn matplotlib seaborn
pip install sentence-transformers bertopic


Optional: Add scispacy for biomedical entity models (e.g., pip install scispacy).

🧩 Step 2. Input format

Create data/text.csv with one column named text:

text
"The APOE ε4 allele increases the risk of Alzheimer’s disease."
"Variants rs429358 and rs7412 define APOE isoforms associated with AD."


Each row represents one abstract or text snippet.

🧩 Step 3. Run notebook

Open genomic_text_curation.ipynb in Jupyter or Google Colab and run all cells sequentially.

Outputs generated:

extracted_entities_full.csv

curated_results.json

topic_model_tfidf.csv

topic_model_bertopic.csv

plots saved under images/ (e.g., kmeans_topics.png, bertopic_topics.png)


