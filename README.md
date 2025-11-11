🧬 Genomic Text Curation & Topic Grouping

A lightweight NLP pipeline for 20–100 short biomedical texts (e.g., abstracts).
It extracts variants, genes, diseases, detects simple relations, and groups texts into topics for fast human curation.

Why this project?
Small teams often need a quick, reproducible way to structure small corpora without heavy infrastructure.
This repo provides a practical baseline you can run in minutes.

.
├── data/
│   └── text.csv                         # input: one column named `text` (20–100 rows)
│
├── genomic_text_curation.ipynb          # main notebook (entity extraction + relations + topics + plots)
│
├── extracted_entities_full.csv          # extracted entities (variants, genes, diseases)
├── curated_results.json                 # variant–gene–disease relation triples
├── topic_model_tfidf.csv                # TF-IDF + KMeans topic assignments
├── topic_model_bertopic.csv             # BERTopic topic assignments (optional)
│
├── images/
│   ├── kmeans_topics.png                # PCA projection of TF-IDF + KMeans clusters
│   └── bertopic_topics.png              # PCA projection of BERTopic clusters
│
└── README.md
