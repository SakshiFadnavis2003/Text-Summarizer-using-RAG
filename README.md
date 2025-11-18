# Local RAG System

## Overview
The **LocalRAGSystem** is a Python-based Retrieval-Augmented Generation (RAG) pipeline designed to process local documents (PDF, Word, PowerPoint), split them into chunks, embed them using sentence-transformer models, store them in a FAISS vector database, and answer user queries using a locally hosted language model.

This project is ideal for offline document question-answering and summarization tasks.

---

## Features
- Upload and process multiple document formats: **PDF**, **DOCX**, **PPTX**
- Split documents into manageable chunks using `RecursiveCharacterTextSplitter`
- Generate embeddings with **HuggingFace sentence-transformers**
- Store embeddings in **FAISS** for efficient similarity search
- Use a local LLM (e.g., `google/flan-t5-base`) for question answering
- Retrieval-based QA with top-k document chunks

---

## Installation
1. Clone the repository:
```bash
git clone <your-repo-url>
cd LocalRAGSystem
```

2. Install dependencies:
```bash
pip install langchain langchain-community transformers sentence-transformers faiss-cpu unstructured google-colab
```

---

## Usage
Run the following steps in a Google Colab or local environment:

### 1. Initialize the RAG System
```python
rag = LocalRAGSystem()
rag.run_setup()
```
This will:
- Upload PDFs interactively
- Load and split documents
- Create embeddings and FAISS vector store
- Initialize the local LLM and QA chain

### 2. Ask Questions
```python
q1 = "What is the main topic of these documents?"
print(f"Q: {q1}
A: {rag.answer_question(q1)}")

q2 = "Summarize the key points from the documents."
print(f"Q: {q2}
A: {rag.answer_question(q2)}")
```

---

## Example Workflow
```python
rag = LocalRAGSystem()
rag.run_setup(chunk_size=1000, chunk_overlap=200, model_id="google/flan-t5-base", k=3)

# Ask questions
print(rag.answer_question("Provide a summary of uploaded documents."))
```

---

## Configuration Options
- **chunk_size**: Size of text chunks for splitting (default: 1000)
- **chunk_overlap**: Overlap between chunks (default: 200)
- **model_id**: HuggingFace model for LLM (default: `google/flan-t5-base`)
- **k**: Number of top documents retrieved for QA (default: 3)

---

## Logging
The system uses Python's `logging` module to provide detailed logs during execution.

---

## License
This project is licensed under the MIT License.
