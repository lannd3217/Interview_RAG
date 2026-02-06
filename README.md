# Interview Intelligence Assistant
## 1. Project Overview
Aspiring Data Scientists and AI Engineers often struggle with "hidden" technical requirements and cultural nuances of top-tier tech companies. This information is typically scattered across engineering blogs, research papers, and fragmented interview guides.

The Interview Intelligence Assistant is a Retrieval-Augmented Generation (RAG) system that centralizes these disparate resources. It allows users to query a curated knowledge base of company-specific technical documentation, providing grounded, cited answers to high-stakes interview questions.

## 2. Target Audience
Job Seekers: Early-to-mid-career candidates targeting Data Science, ML Engineering (MLE), or AI Research roles.


## 3. The Hypothesis
By grounding an LLM in a company-specific technical knowledge base via RAG, we can reduce hallucinations and provide 100% verifiable citations, solving the 'information gap' inherent in general-purpose AI models.

## 4. Key Features
Accelerated Research: Instant summaries of engineering blogs and whitepapers.

No-Hallucination Guardrails: The system is programmed to say "I don't know" if the information isn't present in the provided documents.

Source Attribution: Every response includes the specific PDF and page number where the information was found.

Recursive Chunking: Advanced text splitting ensures semantic continuity even for complex mathematical formulas and code snippets.

## 5. Technical Stack
Language: Python 3.10+

Orchestration: LangChain

Document Loading: PyMuPDFLoader (Optimized for speed and accuracy)

Text Splitting: RecursiveCharacterTextSplitter

Embeddings: sentence-transformers/all-MiniLM-L6-v2 (Local and Free)

Vector Store: FAISS (Fast Approximate Nearest Neighbor Search)


## 7. Getting Started
Installation
Bash
pip install -U langchain-huggingface langchain-community pymupdf faiss-cpu sentence-transformers
Ingestion & Querying
Load: Place your PDFs in the docs/ folder.

Index: Run the ingestion script to create your vector store.

Ask:
# Example Query
query = "What does Meta look for in a System Design interview for MLE?"
# The assistant retrieves relevant snippets and generates an answer grounded in your PDFs.


## 8. Future Roadmap
Multimodal RAG: Support for technical diagrams and architecture charts within PDFs.

Auto-Scraper: Integration with official Engineering Blog APIs (Meta, Netflix, Uber).

Citations UI: A frontend interface highlighting the exact paragraph in the source PDF.

Author: Lan Dinh
