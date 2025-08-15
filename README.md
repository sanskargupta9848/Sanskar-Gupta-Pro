
# Stock Market AI – Core Data Engineering & RAG Pipeline  
**An Intelligent Financial Data Platform with Medallion Architecture & RAG in Databricks**

---

## Overview

This project implements a **complete stock market intelligence pipeline** using the **Medallion Architecture** (Bronze → Silver → Gold) in **Databricks**, enhanced with **Retrieval-Augmented Generation (RAG)** for AI-driven financial insights.  

It ingests and processes:  
- **Historical stock prices** (OHLCV)  
- **Real-time & historical market news**  
- **Market trends & analytics**  
- **Institutional holders data**  

All data flows through **refined transformation layers**, producing **business-ready datasets**.  
A **Streamlit UI chatbot** enables **natural language** financial queries.

---

## UI Preview

| Stage | Screenshot |
|-------|------------|
| Initial view | ![UI Empty](https://github.com/user-attachments/assets/caed6ed4-d8bc-4c16-8815-f6f079506c0f) |
| Chat overlay after prompt | ![Chat Overlay](https://github.com/user-attachments/assets/f9a52fe8-4588-425c-87c0-ed226f0ef211) |
| Prompt only (awaiting response) | ![Prompt Only](https://github.com/user-attachments/assets/90323d38-c883-4dad-800d-b6a256a8375e) |
| Prompt + model response | ![Prompt Response](https://github.com/user-attachments/assets/39a0ba32-fbb0-43ff-8964-649efc81bec8) |

> ℹ The current Streamlit app includes a **local/demo mode** with sample data and a mock LLM response if no API keys are provided. When keys are present, it uses **Google Generative AI Embeddings** and **Gemini**.

---

## Getting Started

```bash
# 1️ Create & activate a virtual environment (recommended)
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# 2️ Install dependencies
pip install -r requirements.txt

# 3️ (Optional) Configure API keys
cp .env.sample .env   # then edit .env

# 4 Run the Streamlit app
streamlit run app.py
```

Opens locally in your browser with an interactive chat UI.

---

## Architecture

```
Stock APIs → Bronze Layer → Silver Layer → Gold Layer → Vector DB → RAG → Streamlit Chatbot
    ↓           ↓             ↓            ↓           ↓         ↓            ↓
yfinance    Raw Data    Cleaned Data   Business    FAISS    Gemini AI   Chatbot Output
Finnhub     Storage     Validation     Ready       Vector   LangChain   
```

---

## ⚙Tech Stack

### Data Engineering
- **Platform:** Databricks (Apache Spark)
- **Data Lake:** Delta Lake (ACID transactions)
- **Catalog:** Unity Catalog
- **Sources:** Yahoo Finance (yfinance), Finnhub (news)
- **Processing:** PySpark, Python
- **Orchestration/Scheduling:** Databricks Workflows

### RAG Components
- **Embeddings:** Google Generative AI (`models/embedding-001`)
- **Vector DB:** FAISS
- **LLM:** Google Gemini 2.0 Flash
- **Framework:** LangChain
- **Chunking:** RecursiveCharacterTextSplitter (optimized token size)
- **Custom Metrics:** Financial performance & risk indicators

---

## Repository Structure

```
notebooks/
    bronze_layer/        → Raw data ingestion
    silver_layer/        → Data cleaning & standardization
    gold_layer/          → Business-ready datasets
    rag_implementation/  → AI-powered querying
    analytics/           → Dashboards & visualizations
data_catalog/            → Unity Catalog schemas
src/                     → Utilities & helper scripts
config/                  → Config files
tests/                   → Unit tests
docs/                    → Documentation
data/                    → Sample CSVs for demo/local mode
```

---

## Data Pipeline

### Bronze Layer – Raw Ingestion
- **Historical Stocks:** Incremental loading, batch multi-ticker fetch, schema flattening  
- **News Data:** API rate-limited aggregation, incremental updates, summary filtering  

### Silver Layer – Cleansing & Standardization
- Standardized date formats  
- Rounded price precision  
- Consistent column naming  
- Null handling & type casting  

### Gold Layer – Business-Ready Analytics
- Merges OHLCV, aggregated news, company metadata  
- Enriched with institutional holders data  
- Produces **RAG-ready datasets**:  
  - `Stocks_news_historical_RAG`
  - `Stocks_holders_RAG`

### RAG Layer – AI Querying
- Combines historical, sentiment, and holder data into embeddings  
- Uses FAISS for retrieval  
- Example queries:
  - “Summarize Apple’s past performance”
  - “Tesla’s top institutional holders”
  - “Correlation between news sentiment & stock movement”
  - “Most volatile stocks last quarter”

---

## Data Schema

**Bronze Layer**  
| Column      | Type   | Description |
|-------------|--------|-------------|
| date        | Date   | Trading date |
| open, high, low, close | Float | OHLC data |
| adj_close   | Float  | Adjusted close |
| volume      | Int    | Volume traded |
| ticker      | String | Stock symbol |

**Gold Layer**  
| Table | Description |
|-------|-------------|
| `Stocks_news_historical_RAG` | OHLCV + aggregated news + company info |
| `Stocks_holders_RAG` | Institutional holders data |

---

## Planned Enhancements

**Near-Term**
- Production-grade RAG with robust error handling  
- Real-time streaming integration  
- Advanced risk & technical indicators  
- Price & volatility forecasting models  

**Future**
- Multi-modal RAG (charts & visuals)  
- Conversation memory for multi-turn chats  
- Portfolio optimization tools  
- Sentiment scoring for news feeds  
- Options volatility surface analytics  

---

## Example Use Cases
- **Market Research:** “Impact of oil prices on energy sector stocks”  
- **Risk Analysis:** “Key risks in my tech portfolio”  
- **Decision Support:** “Should I buy Tesla given recent news?”  
- **Event Analysis:** “Effect of Fed announcements on banking stocks”  
- **Portfolio Strategy:** “Suggest a balanced portfolio for current market conditions”  

---

## Configuration

Create a `.env` in the repo root (or set env vars) for API access:

```
GOOGLE_API_KEY=your_google_key
FINNHUB_API_KEY=your_finnhub_key
```

If keys are not provided, the app runs in **local/demo mode** using sample data and a mock LLM.

---

## Tests

Run a basic smoke test:

```bash
pytest -q
```

---

## License

This project is released under the **MIT License**.
