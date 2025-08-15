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

---

## Getting Started

```bash
# 1️Install dependencies
pip install streamlit

# Run the app
streamlit run app.py
