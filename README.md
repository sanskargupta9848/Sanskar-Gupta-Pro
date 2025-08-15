Stock Market AI – Core Data Engineering & RAG Pipeline

An Intelligent Financial Data Pipeline with Medallion Architecture & RAG in Databricks

Overview

This project delivers a fully integrated stock market data pipeline leveraging the Medallion Architecture (Bronze → Silver → Gold) in Databricks, combined with a Retrieval-Augmented Generation (RAG) system for AI-driven financial insights.

It ingests and processes:

Historical stock prices

Real-time and historical market news

Broader market trends

Institutional holders data

Data flows through multiple transformation layers, culminating in a business-ready analytics layer. A Streamlit-based UI chatbot enables natural language queries to perform advanced financial analysis.

UI Overview

The Streamlit interface offers an intuitive, chat-like experience for querying market data.

Initial View (No Prompt) – Clean application layout before any input.


Prompt Submission – Chat overlay appears after a user query.


Prompt Only (Pending Response) – User query in chatbox awaiting model reply.


Prompt & Response – Model-generated insights displayed alongside user query.


Getting Started

Install Requirements

pip install streamlit


Run the App

streamlit run app.py


This launches the Streamlit server locally and opens the UI in your browser.

System Architecture
Stock APIs → Bronze Layer → Silver Layer → Gold Layer → Vector DB → RAG → Streamlit UI Chatbot
    ↓           ↓             ↓            ↓           ↓         ↓            ↓
yfinance    Raw Data    Cleaned Data   Business    FAISS    Gemini AI   Chatbot Output
Finnhub     Storage     Validation     Ready       Vector   LangChain   

Technology Stack
Data Engineering

Platform: Databricks (Apache Spark)

Data Lake: Delta Lake with ACID transactions

Catalog: Unity Catalog with Medallion architecture

Sources:

Yahoo Finance (yfinance API)

Finnhub (market news API)

Orchestration: Databricks Workflows

Processing: PySpark, Python

Scheduling: Automated workflows

RAG (Retrieval-Augmented Generation)

Embeddings: Google Generative AI (models/embedding-001)

Vector Database: FAISS (Facebook AI Similarity Search)

LLM: Google Gemini 2.0 Flash

Framework: LangChain

Text Chunking: RecursiveCharacterTextSplitter (optimized token size)

Custom Analysis: Proprietary financial metrics & indicators

Repository Structure
├── notebooks/
│   ├── bronze_layer/                  # Raw data ingestion
│   ├── silver_layer/                  # Data cleaning & standardization
│   ├── gold_layer/                    # Business-ready analytics
│   ├── rag_implementation/            # AI-powered querying
│   └── analytics/                     # Interactive dashboards
├── data_catalog/                      # Unity Catalog tables
├── src/                               # Utility functions & processing scripts
├── config/                            # Config files
├── tests/                             # Unit tests
└── docs/                              # Documentation

Data Pipeline
1. Bronze Layer – Raw Data Ingestion

Historical Stock Data (Stocks_ai_historical_bronze)

Source: Yahoo Finance (yfinance)

Features: Incremental loading, multi-ticker processing, date-based logic, schema flattening

News Data (stocks_news_bronze_layer)

Source: Finnhub API

Features: News summaries, API rate limiting, incremental updates, basic filtering

2. Silver Layer – Cleansing & Standardization

Combined Processing (combined_silver_layer_historical+news)

Standardized date formats (MM-dd-yyyy)

Rounded price precision (3 decimals)

Consistent column naming

Null handling & type casting

3. Gold Layer – Business-Ready Analytics

Merges historical data, aggregated news, company metadata

Adds institutional holder information

Produces RAG-ready datasets

Output Tables:

Stocks_news_historical_RAG → Main AI-ready dataset

Stocks_holders_RAG → Institutional holders analytics

4. RAG Layer – AI Financial Analysis

Combines historical data, news sentiment, and holder info into contextual text

Chunks text for embeddings

Stores in FAISS for fast similarity search

Supports natural language financial queries like:

"Summarize Apple’s past performance"

"List Tesla’s major institutional holders"

"Correlation between news sentiment & price movement"

"Highest volatility stocks last quarter"

Data Schema

Bronze Layer

Column	Type	Description
date	Date	Trading date
open	Float	Opening price
high	Float	High price
low	Float	Low price
close	Float	Closing price
adj_close	Float	Adjusted close
volume	Integer	Trading volume
ticker	String	Stock symbol

Gold Layer

Table	Description
Stocks_news_historical_RAG	OHLCV + aggregated news + company info
Stocks_holders_RAG	Institutional holders data
Planned Enhancements

Short Term

Production-grade RAG system with better error handling

Real-time streaming market data

Advanced risk & technical indicators

Predictive ML models (price & volatility)

Long Term

Multi-modal RAG (charts/graphs in responses)

Conversation memory for multi-turn queries

Portfolio optimization tools

Sentiment analysis for market news

Options market volatility surface analytics

Example Use Cases

Financial Research – "Analyze correlation between oil prices & energy sector stocks"

Risk Management – "Identify risks in my tech portfolio"

Investment Decision Support – "Should I buy Tesla given recent news?"

Market Impact Analysis – "Effect of Fed rate changes on bank stocks"

Portfolio Strategy – "Create a balanced portfolio for current conditions"

User Interface Details

Built with Streamlit for simplicity and speed

Works standalone for demo purposes

Future versions will connect directly to Databricks for live, dynamic querying
