🧬 Genomic Text Curation & Topic Grouping

A lightweight NLP pipeline for 20–100 short biomedical texts (e.g., abstracts).
It extracts variants, genes, diseases, detects simple relations, and groups texts into topics for fast human curation.

Why this project?
Small teams often need a quick, reproducible way to structure small corpora without heavy infrastructure.
This repo provides a practical baseline you can run in minutes.

⚙️ Setup & Run
1️⃣ Install dependencies
pip install pandas scikit-learn matplotlib seaborn
pip install sentence-transformers bertopic


You may optionally add scispacy for biomedical entity models.

2️⃣ Input format

data/text.csv

text
"The APOE ε4 allele increases the risk of Alzheimer’s disease."
"Variants rs429358 and rs7412 define APOE isoforms associated with AD."
...


Each row is one abstract or text snippet.

3️⃣ Run notebook

Open genomic_text_curation.ipynb and execute all cells.

Outputs will appear as:

extracted_entities_full.csv

curated_results.json

topic_model_tfidf.csv

topic_model_bertopic.csv

plots in images/
