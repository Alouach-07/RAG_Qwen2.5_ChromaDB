# RAG System for Domain-Specific Knowledge Retrieval (Qwen2.5 & ChromaDB)

## 👤 Author
**ALOUACH Abdennour**

## 💡 Project Overview

This repository hosts a robust **Retrieval Augmented Generation (RAG)** system designed to leverage specialized knowledge from domain-specific documentation. The solution is built using the LangChain framework, integrating a local vector store (ChromaDB) for context retrieval, and the **Qwen2.5-7B-Instruct** Large Language Model (LLM) for high-quality, grounded responses.

The primary objective is to demonstrate how to minimize LLM hallucinations and significantly improve the factual accuracy of generated answers by confining the knowledge source to our custom documents.

## 📚 Data Source

The RAG system operates exclusively on the following core documents, which form the entire knowledge base for the vector store:

* `Chapitre1.pdf`
* `Chapitre2.pdf`

These documents are loaded, chunked, and embedded to allow the Qwen2.5 model to retrieve relevant passages before formulating an answer to a user query.

## 🛠️ Technical Stack

| Component | Library/Model | Purpose |
| :--- | :--- | :--- |
| **Framework** | LangChain (Core/Community) | Orchestration of the RAG pipeline. |
| **LLM** | Qwen2.5-7B-Instruct | Generative model for final answers. |
| **Vector Database** | ChromaDB | Local storage and retrieval of vector embeddings. |
| **Embeddings** | HuggingFace Embeddings | Converts text chunks into vector representations. |
| **Document Processing**| `pypdf`, `RecursiveCharacterTextSplitter` | Loading and splitting the source PDFs. |
| **Optimization** | `accelerate`, `bitsandbytes` | Efficient GPU model loading and quantization. |

## 🚀 Setup and Installation

This project is intended for execution in a Jupyter Notebook environment (Kaggle, Colab, or local machine with GPU). Due to specific dependency conflicts often encountered in these environments, the following installation order is crucial for successful execution.

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/YourUsername/RAG_Qwen2.5_ChromaDB.git](https://github.com/YourUsername/RAG_Qwen2.5_ChromaDB.git)
    cd RAG_Qwen2.5_ChromaDB
    ```

2.  **Execute the Dependency Installation Cell:**
    Run the following command *once* at the beginning of your notebook session. This ensures critical libraries are installed in a compatible order, specifically pinning `chromadb` and `protobuf` to known working versions.

    ```bash
    # 1. Install/Update major libraries
    !pip install -U langchain langchain-community langchain-core \
    langchain-text-splitters sentence-transformers transformers pypdf accelerate bitsandbytes

    # 2. Downgrade ChromaDB to a compatible stable version (0.4.24)
    !pip install chromadb==0.4.24

    # 3. Force reinstall a stable Protobuf version (3.20.3)
    !pip install --force-reinstall protobuf==3.20.3
    ```

3.  **Restart the Kernel/Runtime:**
    After the installation is complete, a **kernel restart is mandatory** to ensure the environment loads the newly pinned versions of `chromadb` and `protobuf`.

## ⚙️ Usage

Once the dependencies are installed and the kernel is restarted:

1.  **Run the Imports Cell:** Load all necessary modules.
2.  **Document Ingestion:** The notebook automatically loads `Chapitre1.pdf` and `Chapitre2.pdf`, splits the content, and generates embeddings.
3.  **Build Vector Store:** The `ChromaDB` vector store is initialized and populated with the document chunks.
4.  **LLM Setup:** The `Qwen2.5-7B-Instruct` model is loaded via the HuggingFace pipeline.
5.  **Querying:** Proceed to the querying cell and interact with the RAG system by asking questions based on the content of the two source PDFs.

## 🤝 Contribution

Feel free to open issues or submit pull requests for any improvements, bug fixes, or suggestions regarding the RAG implementation or model configuration.
