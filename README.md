# RAG QA Chatbot  

A clean and practical Retrieval-Augmented Generation (RAG) chatbot built with **LangChain**, **OpenAI**, and **Pinecone**.  
The goal of this project is to provide a simple, production-friendly reference implementation for document ingestion, embeddings, vector search, and LLM-based question answering.  

---  

## 📍 Why This Exists  
Most RAG examples online are either artificial or overly complicated.  
This repo shows a **minimal but realistic** workflow you can extend in real environments.  

---  

## 🧠 What It Does  
- Takes your documents  
- Cleans + chunks text  
- Generates embeddings  
- Stores them in Pinecone  
- Retrieves relevant chunks  
- Sends context + query to an LLM  
- Returns an accurate answer  

---  

## 🏗 Tech Stack  
- **Python**  
- **LangChain**  
- **OpenAI API**  
- **Pinecone**  
- **FastAPI**  
- **Uvicorn**  
- **Sentence Transformers (optional local embeddings)**  

---  

## 🥥 Architecture  

```
                ┌──────────────────────┐
                │   Raw Documents    │
                └──────────────────────┘
                          │
                          │  Ingestion + Chunking
                          │
                ┌───────────────┐
                │   Embedding Model  │
                └───────────────┘
                          │
                          │  Upsert vectors
                          │
                  ┌──────────────┐
                  │  Vector Store   │
                  │   (Pinecone)    │
                  └──────────────┘
                          │
                          │  Retrieve top-k chunks
                          │
              ┌──────────────────────┐
              │      RAG Engine       │
              │ (LLM + Context Merge) │
              └──────────────────────┘
                          │
                          │  API Response
                          │
                ┌────────────────┐
                │   FastAPI Server   │
                └────────────────┘
```

---  

## 🚀 Getting Started  

### 1. Clone the repo  
```bash
git clone https://github.com/your-username/rag-qa-chatbot
cd rag-qa-chatbot
```

### 2. Install dependencies  
```
pip install -r requirements.txt
```

### 3. Set up environment variables  
Copy the example file:
```
cp .env.example .env
```
Fill in:  
- `OPENAI_API_KEY`  
- `PINECONE_API_KEY`

### 4. Run the API  

```
uvicorn src.app:app --reload
```

Open browser:  
```
http://127.0.0.1:8000/docs
```

---  

## 🦖 Example Query  

```
curl -X POST "http://localhost:8000/ask" \
     -H "Content-Type: application/json" \
     -d '{"question": "What is the refund policy?"}'
```

**Response**

```json
{
  "answer": "Based on the documents, refunds are available within 30 days..."
}
```

---  

## 💂 Project Structure  

```
rag-qa-chatbot/
│
├─ src/
│   ├─ app.py
│   ├─ rag_pipeline.py
│   ├─ embed.py
│   ├─ ingest.py
│
├─ tests/
│   └─ test_basic.py
│
├─ data/
│   └─ README.md
│
├─ docs/
│   └─ architecture.md
│
├─ scripts/
│   └─ ingest_data.py
│
├─ .github/workflows/ci.yml
├─ .env.example
├─ requirements.txt
├─ Dockerfile
├─ Makefile
├─ LICENSE
├─ CHANGELOG.md
├─ CODE_OF_CONDUCT.md
├─ CONTRIBUTING.md
└─ SECURITY.md
```

---  

## 📈 Future Improvements  
- Add reranking layer  
- Add evaluation dashboard  
- Add hybrid search (keyword + semantic)  
- Add streaming chat UI  

---  

## 💜 License  
MIT — use freely for personal or commercial work.
