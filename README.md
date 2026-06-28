# 🏠 Real Estate RAG API

A Retrieval-Augmented Generation (RAG) API for searching real estate properties using semantic search and Large Language Models (LLMs).

The application uses FAISS vector search to retrieve the most relevant properties and optionally uses the Groq API (Llama 3.1) to generate a natural language summary of the results.

---

# Features

- Semantic property search using sentence embeddings
- FAISS vector database
- FastAPI REST API
- LLM-powered property summaries using Groq
- JSON API ready for frontend integration
- Automatic API documentation with Swagger UI

---

# Tech Stack

- Python 3.13
- FastAPI
- LangChain
- FAISS
- HuggingFace Embeddings
- Sentence Transformers
- Groq API (Llama 3.1)
- Pydantic

---

# Project Structure

```
RAG/
│
├── backend/
│   ├── api.py
│   ├── rag_engine.py
│   └── ...
│
├── data/
│   └── sampled_properties.jsonl
│
├── myenv/
│
├── requirements.txt
├── .env
└── README.md
```

---

# Installation

## 1. Clone the repository

```bash
git clone <repository-url>
cd RAG
```

---

## 2. Create a virtual environment

Windows

```powershell
python -m venv myenv
```

Activate it

```powershell
.\myenv\Scripts\Activate.ps1
```

---

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

# Environment Variables

Create a file named

```
.env
```

inside the project root.

Example:

```env
GROQ_API_KEY=your_groq_api_key_here
```

If no API key is provided, the application will still work but AI-generated summaries will be disabled.

---

# Running the API

Start the FastAPI server:

```bash
uvicorn backend.api:app --reload
```

You should see

```
Uvicorn running on:

http://127.0.0.1:8000
```

---

# API Documentation

Swagger UI

```
http://127.0.0.1:8000/docs
```

ReDoc

```
http://127.0.0.1:8000/redoc
```

---

# API Endpoint

## POST /search

Search for properties using natural language.

### Request

```json
{
    "query": "2 bedroom apartment in Cairo"
}
```

---

### Response

```json
{
    "summary": "AI generated summary...",
    "properties": [
        {
            "id": 821,
            "type": "Apartment",
            "price": 14000000,
            "location": "New Cairo",
            "bedrooms": 2,
            "bathrooms": 2,
            "area": 115,
            "description": "...",
            "photos_url": [
                "..."
            ]
        }
    ]
}
```

---

# How It Works

1. Load property data from JSONL.
2. Convert each property into a LangChain Document.
3. Split documents into chunks.
4. Generate embeddings using:

```
sentence-transformers/all-MiniLM-L6-v2
```

5. Store embeddings in a FAISS vector database.
6. Perform semantic similarity search.
7. Remove duplicate property matches.
8. Return the best matching properties.
9. Optionally generate an AI summary using Groq.

---

# Similarity Search

The API uses FAISS similarity search with a configurable threshold.

Current configuration:

```python
top_k = 3
similarity_threshold = 0.8
```

These values can be adjusted depending on the dataset.

---

# Example Query

Request

```json
{
    "query": "Apartment with 2 bedrooms in Cairo under 10 million"
}
```

Response

- Matching properties
- AI-generated comparison
- Property metadata
- Images
- Prices
- Locations

---

# Future Improvements

- Store FAISS index on disk
- Incremental indexing
- Metadata filtering
- Price filtering
- Location filtering
- Hybrid Search (Keyword + Vector)
- PostgreSQL integration
- Authentication
- Docker support
- Cloud deployment
- Pagination
- Caching

---

# Notes

- The vector database is generated at application startup.
- The application supports semantic search rather than exact keyword matching.
- AI summaries require a valid Groq API key.
- Without the API key, only property search results are returned.

---

# Author

Developed as a Retrieval-Augmented Generation (RAG) backend for a real estate search application using FastAPI, LangChain, FAISS, and Groq.
