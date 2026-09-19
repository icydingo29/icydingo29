<div align="center">

# icydingo29

**AI Engineer** · retrieval systems, LLM pipelines, applied ML

MSc *Information Retrieval & Knowledge Discovery* — Sofia University "St. Kliment Ohridski", FMI

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/gabriel-tuparov-0830b5317/)
[![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/icydingo29)

</div>

---

I put language models on top of structured data — and then measure whether they actually work. Most of what I build ships with a benchmark, an ablation, and a written account of where it fails.

- 🏦 &nbsp;**AI Engineer intern** 
- 🔍 &nbsp;**Focus:** RAG & knowledge graphs, information retrieval, evaluation of LLM systems
- 🛠 &nbsp;**Also ship:** FastAPI services, Dockerised deployments, PyTorch training pipelines
- 📍 &nbsp;Sofia, Bulgaria — open to AI/ML engineering roles

---

## Tech

**Languages** &nbsp;
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![SPARQL](https://img.shields.io/badge/SPARQL-0C479D?style=flat-square)

**ML & AI** &nbsp;
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat-square&logo=ollama&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-F55036?style=flat-square&logo=groq&logoColor=white)

**Backend & Data** &nbsp;
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![GraphDB / RDF](https://img.shields.io/badge/GraphDB%20%2F%20RDF-1A1A1A?style=flat-square)

---

## Selected Work

### 🧾 [Smart Receipt Analyzer](https://github.com/icydingo29/smart-receipt-analyzer)
*An LLM document-processing service that actually runs as a service.*

PDF invoices in, structured expense reports out. Vision-model OCR with a `pdfplumber` fallback, an LLM enrichment stage that categorises line items and corrects OCR noise, Pydantic-validated persistence to PostgreSQL, and a generated PDF report. Exposed both as a REST API and a web UI; the whole stack comes up with one `docker compose` command.

`FastAPI` · `PostgreSQL` · `SQLAlchemy` · `Pydantic v2` · `Groq` · `Docker Compose` · `Streamlit`

---

### 🌍 [Natural Language → SPARQL over a Knowledge Graph](https://github.com/icydingo29/nlq-sparql-graphdb-benchmark)
*Can a small local LLM query an ontology reliably? Measured, not guessed.*

<img src="https://github.com/icydingo29/nlq-sparql-graphdb-benchmark/raw/main/docs/demo.gif" width="700" alt="Natural language question translated to SPARQL and executed against GraphDB">

A local Qwen2.5-Coder model translates plain-language questions into SPARQL against an OWL2-RL geographic ontology in GraphDB. The interesting part is the evaluation harness: **22 questions across 7 reasoning categories, 10 runs each**, scored against hand-written reference queries executed live against the triplestore — no hardcoded expected values.

**Result:** 82% exact-match at 3B, **93% at 7B**, with every failure mode traced to a root cause (dropped `FILTER`s, abandoned `MINUS`, entity-name abbreviation, reasoner limitations under the open-world assumption).

📄 [Full methodology & benchmark report](https://github.com/icydingo29/nlq-sparql-graphdb-benchmark/blob/main/docs/report.md)

`Ollama` · `GraphDB` · `OWL2-RL` · `SPARQL` · `owlready2` · `Python`

---

### 🎹 [LSTM vs Transformer for Symbolic Music](https://github.com/icydingo29/lstm-transformer-midi-comparison)
*A controlled architecture comparison, written up as a paper.*

Four models — 2 architectures × 2 tokenisation schemes — trained on ~38K MIDI files with **parameter counts matched within ±10%** and an artist-stratified split so no artist appears in both train and test. Includes a custom 532-token event tokeniser alongside a REMI+ wrapper.

**Finding:** raw perplexity isn't comparable across tokenisers, so evaluation uses bits per second of musical time. Measuring loss per position bucket shows the Transformer's advantage over the LSTM **grows ~8.5× across the 512-token context window** — long-range dependency access, quantified.

📄 [Paper (PDF)](https://github.com/icydingo29/lstm-transformer-midi-comparison/blob/main/3MI3400841_9MI3400791_LSTM_versus_Transformer_for_Symbolic_Music_anonymous.pdf) · 🤗 [Trained checkpoints](https://huggingface.co/icydingo29/lstm-vs-transformer-symbolic-music)

`PyTorch` · `MidiTok` · `flash attention` · `Kaggle / Lightning AI`

---

### 🎵 [Phonetic Song Search Engine](https://github.com/icydingo29/phonetic-song-search-engine)
*Find the song from lyrics you misheard.*

Lyrics are converted to IPA phonemes and indexed as bigrams, then queries pass through a four-stage retrieval pipeline — inverted-index lookup → Jaccard filtering → TF-IDF reranking → weighted Levenshtein distance using a phoneme substitution-cost matrix — with query-length-adaptive thresholds and optional one-hop query expansion. Benchmarked against SoundEx and Metaphone baselines on Accuracy@1, Recall@K and MRR.

*Built with [@Bifrost19](https://github.com/Bifrost19) as MSc coursework in Information Retrieval.*

`Python` · `eng_to_ipa` · custom TF-IDF · `pandas`

---

### 📰 [Linguistic Priors in Bulgarian Summarization](https://github.com/icydingo29/prior-weights-impact-lsa-textrank-bg)
*Do POS and NER priors help graph ranking or matrix decomposition more?*

TextRank (PageRank power iteration) and LSA (TF-IDF + SVD), both implemented from scratch in NumPy and both extended with sentence priors derived from POS and NER tags, blended by a tunable α. Evaluated with ROUGE-1/2/L across a grid over α and summary length, on a morphologically rich language with Bulgarian-specific stemming and stopword handling.

`NumPy` · `CoNLL-U Plus` · `BulStem` · `ROUGE`

---

### 🍺 [Beer Archetype Discovery](https://github.com/icydingo29/beer-archetype-discovery)
*Unsupervised clustering turned into rules a human can read.*

Fuzzy C-Means with random restarts discovers latent archetypes in sensory beer profiles; adaptive Gaussian membership functions then convert cluster centroids into linguistic IF–THEN rules. Product t-norm activation is computed in log-space to avoid underflow in high dimensions, and the rule-based approximation is validated against the original FCM model (**Pearson r > 0.90**) rather than assumed faithful.

`Fuzzy C-Means` · `PCA` · `NumPy` · `Matplotlib`

---

### ⚡ [AI Algorithms from Scratch (C++)](https://github.com/icydingo29/artificial-intelligence-from-scratch)
*Fundamentals, implemented for speed rather than for the textbook.*

IDA\* with Manhattan distance for the N-Puzzle, MinConflicts for N-Queens, a genetic algorithm with order crossover for TSP, minimax with alpha-beta pruning, plus K-Means, Naive Bayes and decision trees — no libraries. Optimised with O(1) conflict frequency arrays, delta-distance mutation updates and cache-friendly memory layout.

**Benchmark:** 10,000-queens MinConflicts solved in **0.34s**; 15-Puzzle solved by IDA\* effectively instantly.

`C++17` · `-O3` · `std::mt19937`

---

## Education

**MSc — Information Retrieval & Knowledge Discovery** · Sofia University "St. Kliment Ohridski", FMI
Deep learning with PyTorch, recommender systems, knowledge bases & ontologies, NLP, knowledge discovery from data.

**BSc — Computer Science** · Sofia University "St. Kliment Ohridski", FMI
Algorithms & data structures, object-oriented programming, databases, operating systems, computer networks, software engineering, discrete mathematics & probability.

---

<div align="center">

*Most repos ship with a written report or paper — the methodology is usually more interesting than the code.*

</div>