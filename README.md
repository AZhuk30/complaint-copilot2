# Complaint Copilot 🔍

AI-powered intelligence over the [CFPB Consumer Complaint Database](https://www.consumerfinance.gov/data-research/consumer-complaints/).

**Live demo:** https://complaint-copilot2.streamlit.app

---

## What it does

- Ingests 10,000 real consumer complaints daily from the CFPB public API
- Embeds narratives using `sentence-transformers` for semantic search
- Answers natural-language questions over the complaint corpus via RAG (Claude API)
- Surfaces top products, issues, and companies in an interactive dashboard

---

## Architecture

```
CFPB API (official v1 endpoint)
    ↓  ingest.py
data/complaints.parquet
    ↓  02_copilot_rag.py
Embeddings (all-MiniLM-L6-v2)
    ↓
RAG query engine (Anthropic Claude)
    ↓
Streamlit dashboard
```

---

## Run locally

```bash
git clone https://github.com/YOUR_USERNAME/complaint-copilot
cd complaint-copilot

python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# Pull 10,000 complaints from the CFPB API
python ingest.py --rows 10000

# Generate embeddings + test RAG
python 02_copilot_rag.py

# Launch dashboard (optional: set API key for LLM answers)
export ANTHROPIC_API_KEY=sk-ant-...
streamlit run app.py
```

---

## Data source

CFPB Consumer Complaint Database — official v1 API:
```
https://www.consumerfinance.gov/data-research/consumer-complaints/search/api/v1/
```
Updated daily. 4M+ complaints. No API key required.

---

## Tech stack

| Layer | Tool |
|---|---|
| Data source | CFPB public API |
| Storage | Parquet |
| Embeddings | sentence-transformers (all-MiniLM-L6-v2) |
| RAG | Anthropic Claude API |
| Dashboard | Streamlit |
| Language | Python 3.10+ |
