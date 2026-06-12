## RAG Pipeline 

A hands-on playground for exploring Retrieval-Augmented Generation (RAG) techniques from classic pipelines to agentic, tool-calling workflows. Built around Solo Leveling content, but the patterns are fully transferable to any domain.

### Project 1 -> Solo Leveling RAG Pipeline 
This project is built on **Traditional-RAG-Pipeline**

```
TRADATIONAL-RAG-PIPELINE/
├── notebook/
│   ├── agentic_rag_pipeline.ipynb   # Full agentic RAG with LangGraph
│   ├── agentic_rag.ipynb            # Agentic RAG experiments
│   └── note.ipynb                   # Scratch / notes
├── data/                            # PDFs and source documents
├── .env                             # API keys (not committed)
├── Dockerfile
├── pyproject.toml
├── requirements.txt
└── uv.lock
```


### Workflows Implementation

1. **Traditional RAG**
The classic, battle-tested pipeline. Clean and straightforward.
> PDF Directory → Chunking → Embedding → Vector DB → Retriever → LLM → Answer

How it works:
- Load - Ingests a directory of PDFs using DirectoryLoader + PyMuPDF

- Chunk - Splits text with RecursiveCharacterTextSplitter

- Embed & Store - Embeds chunks and loads them into ChromaDB

- Retrieve - Uses Chroma as a retriever to fetch relevant context

- Generate - Passes context + query to an LLM to produce the final answer

Notebook: notebook/traditional-pipeline.ipynb

2. **Agentic RAG**
A smarter pipeline powered by LangGraph. Instead of blindly retrieving, the agent decides how to answer.
> Start → Rewrite Query → Retriever → (fallback) Web Search → Generate → End

How it works:
- Rewrite - The agent rewrites the user query for better retrieval

- Retriever - Tries ChromaDB first

- Web Search - Falls back to web search if the retriever doesn't find enough relevant context (dashed path)

- Generate - Synthesizes a final answer from whichever source(s) were used

This is a StateGraph built with langgraph.prebuilt nodes are Python functions, edges are conditional routing logic.

Notebook: notebook/agentic_rag_pipeline.ipynb

### Getting Started

Prerequisites

Python 3.10+
uv (recommended) or pip

Install dependencies

`git clone https://github.com/IkkIsuhas/solo-leveling-RAG-pipeline.git`

`cd solo-leveling-RAG-pipeline`

`uv sync`

`uv venv --python 3.10`

`.venv/Scripts/activate`

`uv add -r requirements.txt`

**Set up environment variables**

- OPENROUTER_API_KEY=

- COHERE_API_KEY=          # optional, for reranking

- TAVILY_API_KEY= 

### 🗺️ Roadmap

- [ ] Traditional RAG — Index once, retrieve always, no questions asked
- [ ] Agentic RAG — Agent decides whether to retrieve, rewrite, search the web, or combine sources before answering
- [ ] BM25 Retriever — Ranking algorithm for keyword-based search 
- [ ] Graph RAG — Builds a knowledge graph from your documents where entities are nodes and their relationships are edges
- [ ] HyDE — Hypothetical Document Embeddings
- [ ] Reranking — Cohere / cross-encoder based reranking 
- [ ] Self-RAG — Model decides when to retrieve and how to use it

## 🛠️ Tech Stack

| Component | Tool |
|---|---|
| LLM Framework | LangChain, LangGraph |
| Vector DB | ChromaDB |
| PDF Loader | PyMuPDF (`pymupdf`) |
| Embeddings | HuggingFace (sentence-transformers/all-MiniLM-L6-v2) |
| Web Search | Tavily |
| Package Manager | `uv` |
| Environment | Jupyter Notebooks |

---

### Workflow Diagrams

![Traditional-RAG] (images/traditional-rag)

![Agentic-RAG] (images/agentic-rag)

## 📬 Connect

Built by [Suhas](https://github.com/IkkIsuhas) - AI/ML Engineer exploring RAG pipelines and AI agents.
---

> ⭐ Star the repo if you find it useful more techniques coming soon.