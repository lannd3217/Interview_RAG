# Job Hunting AI Mentor 

## I. What is Job Hunting AI Mentor?

**Job Hunting AI Mentor** is a RAG-powered (Retrieval-Augmented Generation) system that provides on-demand interview preparation and career guidance for early-career Data Science and AI professionals. Unlike generic chatbots, this AI mentor grounds its responses in curated knowledge sources—combining technical fundamentals from authoritative books with real-world experiences from online communities.

### Core Capabilities

- **Technical Interview Prep:** Answer questions about ML algorithms, statistics, A/B testing, and programming concepts
- **Industry Insights:** Provide context from real job seekers' experiences and advice from DS communities
- **Source Transparency:** Show which books or forum posts informed each answer

### Current Knowledge Base

The AI mentor currently draws from **9 carefully curated sources**:

**PDF Books:**
- Machine Learning Interviews (Susan Shu Chang)
- Cracking the Data Science Interview
- Statistical Methods for Data Science
- A/B Testing: A Systematic Literature Review
- Meta ML Interview Prep (Initial + Onsite)
- Essential Machine Learning Interview Questions
- Data Science Analytics Prep Guide
- Data Science Intern Screening Interview Prep

**Online Forum Compilation:**
- Reddit_DS_NewGrad.txt: Real candidate experiences, job search stories, and peer advice from the Data Science new grad community

This combination ensures responses are both technically rigorous and grounded in real-world job search realities.

## II. How It Works

### System Architecture

The system follows a 7-stage pipeline:

1. **Document Ingestion** → PyMuPDF + TextLoader with custom cleaning
2. **Chunking** → RecursiveCharacterTextSplitter (chunk=600, overlap=100)
3. **Embedding** → all-MiniLM-L6-v2 (384-dimensional vectors)
4. **Vector Store** → ChromaDB with persistent storage
5. **Retrieval** → Semantic search
6. **Generation** → TinyLlama-1.1B-Chat with prompt engineering
7. **Evaluation** → RAGAS (Faithfulness + ContextPrecision metrics)



## III. Getting Started

### Prerequisites

Python 3.8+
CUDA-capable GPU (recommended for generation)
8GB+ RAM
### Setup
#### 1. Add PDF books and TXT forum files to ./docs folder
#### 2. Set environment variables
export OPENAI_API_KEY="your-openai-api-key"  # For RAGAS evaluation only
#### 3. Run ingestion pipeline and builde vector store
jupyter notebook InterviewRAG.ipynb
#### 4. Retrieval and answer generation
jupyter notebook Retrieval_RAG_v2.ipynb
#### 5. Demo
jupyter notebook RAG_Demo.ipynb

| Notebook               | Purpose                                      | Key Components                                              |
| ---------------------- | -------------------------------------------- | ----------------------------------------------------------- |
| InterviewRAG.ipynb     | Document ingestion and vector store creation | load_docs_from_folder(), clean_text(), ingestion_pipeline() |
| Retrieval_RAG_v2.ipynb | Retrieval implementation                     | Semantic Retrieval                                          |
| RAG_Evaluation.ipynb   | RAGAS evaluation with GPT-4o-mini            | Faithfulness and ContextPrecision metrics                   |
| RAG_Demo.ipynb         | Interactive demo interface                   | ipywidgets dropdown with live questions and answers         |


### Evaluation Framework
The system uses RAGAS (Retrieval-Augmented Generation Assessment) with two key metrics:
| Metric           | Description                                     | What It Measures        |
| ---------------- | ----------------------------------------------- | ----------------------- |
| Faithfulness     | How grounded the answer is in retrieved context | Prevents hallucinations |
| ContextPrecision | Relevance of retrieved chunks to the question   | Retrieval quality       |

Judge LLM: GPT-4o-mini evaluates each metric automatically, outputting scores to ragas_results.csv.

## IV. Project Structure
InterviewRAG/

├── docs/                          # Source documents (PDFs, TXT)

├── .interview_vector_db/          # Persistent ChromaDB storage

├── InterviewRAG.ipynb             # Main ingestion pipeline

├── Retrieval_RAG_v2.ipynb         # Retrieval implementation

├── RAG_Evaluation.ipynb           # RAGAS evaluation

├── RAG_Demo.ipynb                 # Interactive demo

├── ragas_results.csv              # Evaluation metrics output

├── ragas_eval_dataset.json        # Pre-computed Q&A pairs

├── RAG_Architecture.pdf           # System architecture diagram

└── README.md                      # This file


## V. Technical Stack
LangChain - RAG orchestration framework

ChromaDB - Vector database for semantic search

HuggingFace - TinyLlama-1.1B-Chat, all-MiniLM-L6-v2 embeddings

RAGAS - Evaluation framework for RAG systems

PyMuPDF - PDF document parsing

Jupyter - Interactive development and demo

## VI. Future Improvements
### The Vision: Scaling Mentorship Beyond Availability Constraint
#### The Problem This Solves
Navigating the job market as an early-career professional is challenging. After joining mentorship programs, I realized that personalized guidance has nuances that generic advice can't capture. The core bottleneck: Non-profit mentorship programs are limited by mentor availability. Fewer people with common concerns get access to the personalized guidance they need when they need it.

#### Long-Term Vision
While the current system leverages publicly available books and forums, the ultimate vision is to scale human mentorship by:

1. Capturing Meeting Transcripts: Ingest anonymized transcriptions from real mentorship sessions to preserve nuanced advice

2. Collecting Professional Anecdotes: Partner with experienced professionals to contribute their career stories and lessons learned

3. Personalized Recommendations: Tailor advice based on user background, career stage, and specific goals

4. Continuous Updates: Keep the knowledge base current as the DS/AI field rapidly evolves

#### Impact Statement
This project aims to democratize access to quality career mentorship by:

1. Scaling beyond human constraints - 24/7 availability vs. limited mentor hours

2. Preserving diverse perspectives - Synthesizing insights from multiple mentors and sources

3. Removing barriers - Free and accessible to anyone with internet access

4. Empowering self-directed learning - On-demand answers without waiting for scheduled meetings

##### The ultimate goal: No early-career professional should be held back from their dream job due to lack of mentorship access. This AI system doesn't replace human mentors—it amplifies their reach and preserves their wisdom for future generations of job seekers.



Author: Lan Dinh
