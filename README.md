# 📚 Python RAG Document Q&A System

This project is a versatile Question-Answering (Q&A) application that uses the Retrieval-Augmented Generation (RAG) architecture. It allows you to "chat" with your documents by uploading them and asking questions. The system retrieves relevant information from the documents and uses a Large Language Model (LLM) to generate a precise answer.

The application comes in two flavors:
1.  **`app-openai.py`**: Connects to the OpenAI API for embeddings and chat generation (Cloud-based).
2.  **`app-ollama.py`**: Connects to a local Ollama instance, allowing you to run the entire system offline and for free (Local-based).

!Demo Screenshot

## ✨ Features

- **Multiple Backends**: Choose between the powerful OpenAI models or a private, local setup with Ollama.
- **Wide Document Support**: Upload and process various file formats:
  - 📄 PDF (`.pdf`)
  - 📝 Word Documents (`.docx`)
  - 📊 Spreadsheets (`.csv`, `.xlsx`)
  - 🌐 Web pages (`.html`)
  - 📃 Plain Text & Markdown (`.txt`, `.md`)
- **Flexible Input**: Upload multiple files or paste text directly into the application.
- **Efficient Search**: Uses `FAISS` (Facebook AI Similarity Search) for fast and accurate semantic search over document chunks.
- **Intuitive UI**: A simple and clean user interface built with Streamlit.
- **Source Citing**: The assistant shows the source chunks from your documents that were used to generate the answer.

## ⚙️ How It Works (RAG Architecture)

The application follows a standard RAG pipeline:

1.  **Load & Chunk**: Documents are loaded and split into smaller, overlapping text chunks.
2.  **Embed**: Each chunk is converted into a numerical vector (an embedding) using an embedding model (either from OpenAI or Ollama).
3.  **Index**: The embeddings are stored in a FAISS vector index for efficient similarity searching.
4.  **Retrieve**: When you ask a question, it's also embedded, and the index is searched to find the most relevant document chunks (the "context").
5.  **Generate**: The question and the retrieved context are passed to an LLM (GPT or a local model like Llama 3), which generates a human-like answer based on the provided information.

## 🚀 Getting Started

Follow these steps to set up and run the project on your local machine.

### Prerequisites

- **Python 3.10+**
- **Conda/Miniconda**: Recommended for managing dependencies, especially `faiss-cpu`. You can download it here.
- **(For Ollama version)**: Ollama installed and running on your system.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/your-repo-name.git
    cd your-repo-name
    ```

2.  **Create and activate a Conda environment:**
    This is the recommended approach as the `requirements.txt` file is configured to use the `conda-forge` channel for specific packages.
    ```bash
    conda create -n rag-app python=3.11
    conda activate rag-app
    ```

3.  **Install the dependencies:**
    The `requirements.txt` file is set up to work with `pip` inside a Conda environment.
    ```bash
    pip install -r requirements.txt
    ```

## 🛠️ Configuration and Usage

Choose one of the two options below to run the application.

---

### Option 1: Using OpenAI (Cloud)

This version uses the OpenAI API and requires an API key.

1.  **Configure your API Key**:
    Create a file named `secrets.toml` inside a `.streamlit` folder in the project root:
    ```toml
    # .streamlit/secrets.toml
    API_KEY = "sk-your-openai-api-key-here"
    ```
    Alternatively, you can set it as an environment variable.

2.  **Run the Streamlit app:**
    ```bash
    streamlit run app-openai.py
    ```

---

### Option 2: Using Ollama (Local)

This version runs entirely on your machine, ensuring privacy and no API costs.

1.  **Install and Run Ollama**:
    Follow the instructions on the Ollama website to download and start the Ollama service.

2.  **Pull the required models**:
    Open your terminal and run the following commands to download the default embedding and chat models:
    ```bash
    ollama pull nomic-embed-text
    ollama pull llama3
    ```

3.  **Run the Streamlit app:**
    Make sure the Ollama application is running in the background.
    ```bash
    streamlit run app-ollama.py
    ```
    The app will connect to Ollama at the default `http://localhost:11434`.

---

### Using the Application

Once the app is running:
1.  Use the sidebar to upload one or more documents or paste text.
2.  Adjust any advanced settings like chunk size if needed.
3.  Click the **"Process Documents"** button. The app will chunk, embed, and index the content.
4.  Once processing is complete, you can start asking questions in the chat input box at the bottom of the page.

## 📂 File Structure

```
.
├── .streamlit/
│   └── secrets.toml    # (Optional) For OpenAI API key
├── app-openai.py       # Streamlit app using OpenAI
├── app-ollama.py       # Streamlit app using local Ollama
├── requirements.txt    # Python dependencies
└── README.md           # This file
```

## 📄 License

This project is licensed under the MIT License. See the `LICENSE` file for details.


This README provides a solid foundation for your project. You can add more details, such as screenshots or a "Contributing" section, as your project evolves.

## TODO

- Combine `app-openai.py` and `app-ollama.py` into a single app where the user can select the backend (OpenAI or Ollama) from the UI.
- Persist the FAISS index to disk so I don't have to re-process documents every time I start the app.

