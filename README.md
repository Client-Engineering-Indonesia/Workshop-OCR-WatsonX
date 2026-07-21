# Workshop OCR WatsonX

## About This Project

This project is a workshop that demonstrates how to build an **OCR-powered AI Chatbot** using **IBM watsonx Orchestrate**. The solution leverages watsonx Orchestrate's Agent Builder and Document Extractor capability to create an intelligent agent capable of reading, extracting, and validating structured data from image-based documents (OCR).

The primary use case is **QRIS (QR Code Indonesian Standard) merchant data extraction** — a BI Assistance Agent that accepts uploaded QRIS documents, extracts merchant fields automatically using a trained schema, and provides conversational responses grounded in a knowledge base.

### Key Components

| Component | Description |
|-----------|-------------|
| **IBM watsonx Orchestrate** | Core AI platform for agent orchestration |
| **Agent Builder** | No-code interface to configure the AI agent's persona, tools, and knowledge |
| **Document Extractor (Agentic Workflow)** | OCR pipeline that extracts structured fields from uploaded documents |
| **Embedded HTML Chatbot** | Standalone HTML page to host the chatbot on any web page |

### Repository Contents

```
Workshop-OCR-WatsonX/
├── Assets/          # Supporting images and assets
├── Sample/          # Sample QRIS documents for testing
└── Lab1_IBM_OCR.md  # Step-by-step lab guide
```

---

## 📖 Step-by-Step Lab Guide

For the full hands-on lab instructions, refer to the official lab document:

👉 **[Lab 1 — Building a QRIS Extractor AI Agent on IBM watsonx Orchestrate](https://github.com/Client-Engineering-Indonesia/Workshop-OCR-WatsonX/blob/main/Lab1-IBM_WXO_OCR/Lab1_IBM_OCR.md)**
