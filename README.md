
# 🧠✨ RAGArch ✨🧠

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg?logo=python)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-3.x-lightgrey.svg?logo=flask)](https://flask.palletsprojects.com/)
[![CUDA](https://img.shields.io/badge/CUDA-Required-green.svg?logo=nvidia)](https://developer.nvidia.com/cuda-zone)
[![RAGatouille](https://img.shields.io/badge/RAGatouille-ColBERTv2-orange.svg)](https://github.com/bclavie/RAGatouille)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> **⚡ High-Performance Retrieval-Augmented Generation (RAG) Architecture powered by ColBERTv2 & Flask ⚡**

---

## 📖 About

**RAGArch** is a lightweight, high-performance Flask-based API designed for advanced text retrieval using the **RAGatouille** library (backed by the state-of-the-art **ColBERTv2** model). It intelligently chunks input documents, indexes them on-the-fly, and retrieves the most contextually relevant snippets for any given query. 

Built for speed and accuracy, this architecture leverages GPU acceleration (CUDA) and FAISS to deliver lightning-fast semantic search capabilities. 🔥

---

## ✨ Features

- 🧠 **State-of-the-Art Retrieval**: Utilizes `colbert-ir/colbertv2.0` for late-interaction semantic search.
- ✂️ **Smart Chunking**: Integrates `langchain-text-splitters` for precise `RecursiveCharacterTextSplitter` document segmentation.
- ⚡ **GPU Accelerated**: Enforces CUDA availability for maximum indexing and search performance.
- 🗄️ **FAISS Integration**: Optimized vector storage and retrieval using FAISS.
- 📝 **Robust Logging**: Built-in exception and process logging to `demolog.txt` for easy debugging and monitoring.
- 🌐 **RESTful API**: Simple and intuitive Flask endpoint for seamless integration into any backend system.

---

## 🚀 Getting Started

### 📋 Prerequisites

- 🐍 **Python 3.8+**
- 🎮 **NVIDIA GPU** with CUDA support *(Required: The app asserts `torch.cuda.is_available()`)*
- 📦 **Git**

### 🛠️ Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/postboxat18/RAGArch.git
   cd RAGArch
   

2. **Create a virtual environment (recommended):**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r req.txt
   ```
   *(💡 Note: The `req.txt` includes `torch==2.3.0+cu121`. Ensure your system has CUDA 12.1 toolkits installed, or adjust the PyTorch version to match your local CUDA setup.)*

---

## 📡 API Usage

The application exposes a single endpoint at `http://localhost:9001/`.

### 🔹 Endpoint: `/` (POST)

**Request Payload (JSON):**
```json
{
  "query": "What is the main topic of the document?",
  "all_text": ["This is the first page of the document...", "This is the second page..."],
  "top_k": 3
}
```

**Parameters:**
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `query` | `string` | The search query string. |
| `all_text` | `list[string]` | A list of text chunks or pages to be indexed and searched. |
| `top_k` | `int` *(optional)* | Number of top results to return. Defaults to 20% of the total text chunks if not provided. |

**Example cURL Request:**
```bash
curl -X POST http://localhost:9001/ \
-H "Content-Type: application/json" \
-d '{
  "query": "machine learning",
  "all_text": ["Machine learning is a subset of AI.", "Flask is a web framework in Python."],
  "top_k": 1
}'
```

---

## 📂 Project Structure

```text
RAGArch/
├── 📁 .idea/                  # IDE configuration files
├── 📁 .ragatouille/           # ColBERT index storage directory
│   └── 📁 colbert/
│       └── 📁 indexes/
│           └── 📄 version/    # Generated FAISS/ColBERT index data
├── 📄 FlaskRAG.py             # Main Flask application & RAG logic
├── 📄 req.txt                 # Python dependencies list
└── 📄 demolog.txt             # Auto-generated error/process log file (created at runtime)
```

---

## ⚠️ Important Notes

- 🚨 **CUDA Requirement**: The application will explicitly fail to start if a CUDA-enabled GPU is not detected (`assert torch.cuda.is_available()`). Ensure your NVIDIA drivers and CUDA toolkit are properly configured.
- 🔄 **Index Overwrite**: The current implementation uses `overwrite_index=True`, meaning the index is rebuilt on every POST request. For heavy production workloads, consider implementing persistent indexing or caching strategies.

---

## 👤 Medium article

**Aravinth Chinna Samy**  
🔗 Medium: [🚀 Running RAGatouille with ColBERT v2.0 on Windows: Problems I Faced and How I Fixed Them](https://medium.com/@aravinthc18/running-ragatouille-with-colbert-v2-0-on-windows-problems-i-faced-and-how-i-fixed-them-0a7eda82d05d)

---

## 📜 License

This project is open-source and available under the [MIT License](LICENSE).

---
<p align="center">
  <sub>⚜️ Crafted with precision and passion ⚜️</sub>
</p>
```

### 💡 Tips for using this README:
1. **Special Characters**: I used a mix of Unicode box-drawing characters (`├──`, `└──`) for the file tree, and thematic emojis (🧠, ⚡, 🚀) to make sections pop and improve readability.
2. **Badges**: The shields.io badges at the top instantly communicate the tech stack to visitors.
3. **Next Steps**: If you have a specific license file, make sure to add a `LICENSE` file to your repo so the badge links correctly. If you want to change the license type, just update the text and badge URL.
