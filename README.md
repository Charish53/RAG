
# 📚 Document Insights Generator

Welcome to the Document Insights Generator, a powerful tool crafted by Reddipalli Sai Charish for uploading, processing, and querying documents to extract meaningful insights using advanced natural language processing and vector search capabilities. This project leverages a modern tech stack to provide a seamless experience for users to interact with their documents via a web-based interface.

## 🚀 Project Overview

The Document Insights Generator, developed by Reddipalli Sai Charish, allows users to:

- **Upload Documents**: Supports multiple file formats such as PDF, CSV, and TXT.
- **Process Documents**: Splits documents into manageable chunks and creates embeddings for efficient storage and retrieval.
- **Query Documents**: Uses a conversational AI interface to answer questions based on the content of uploaded documents.
- **Interactive Frontend**: A sleek Streamlit-based web interface with custom styling for a user-friendly experience.

This project is ideal for researchers, students, or professionals who need to extract insights from large sets of documents quickly and efficiently.

## 🛠️ Tech Stack

The project is built using a robust combination of Python libraries, frameworks, and tools to handle document processing, embeddings, vector storage, and a web-based frontend.

### Backend

- **Python 3.x**: Core programming language for all scripts and logic.
- **ChromaDB**: A vector database for storing and querying document embeddings.  
  Used in `Trial.py`, `ingest.py`, and `LLM_tool.py` for persistent storage of document embeddings.

- **LangChain**: Framework for document loading, text splitting, embeddings, and conversational retrieval.
  - **Document Loaders**: `CSVLoader`, `PyMuPDFLoader`, `TextLoader` (and others for additional formats like DOCX, EML, EPUB, HTML, Markdown, ODT, PPTX).
  - **Text Splitter**: `RecursiveCharacterTextSplitter` for chunking documents.
  - **Embeddings**: Supports `CohereEmbeddings` and `OpenAIEmbeddings` for vectorizing text.
  - **Chains**: `ConversationalRetrievalChain` for question-answering with conversation history.

- **Cohere Embeddings**: Used for generating high-quality text embeddings (`ingest.py`, `LLM_tool.py`).
- **OpenAI**: Optional LLM backend for conversational AI (`LLM_tool.py`).
- **Ollama**: Alternative LLM model (e.g., Llama3) for local inference (`LLM_tool.py`).
- **python-dotenv**: Manages environment variables for configuration (`constants.py`, `ingest.py`, `LLM_tool.py`).
- **Multiprocessing**: Leverages `Pool` for parallel document loading (`ingest.py`, `LLM_tool.py`).
- **tqdm**: Displays progress bars for document processing (`ingest.py`, `LLM_tool.py`).
- **glob**: Handles file discovery for document loading (`ingest.py`, `LLM_tool.py`).

### Frontend

- **Streamlit**: A Python framework for building interactive web applications.  
  Used in `LLM_tool.py` to create the user interface for document uploads and querying.

- **HTML/CSS**: Custom CSS for styling the chat interface and sidebar (`LLM_tool.py`).  
  Features a modern chat UI with user and bot avatars, custom backgrounds, and responsive design.

- **Pillow (PIL)**: Processes and resizes logos for the Streamlit app (`LLM_tool.py`).

### Additional Tools

- **tempfile**: Creates temporary files for handling uploaded documents in Streamlit (`LLM_tool.py`).
- **argparse**: Included for potential CLI argument parsing, though not fully utilized in the provided code (`LLM_tool.py`).
- **os**: Handles file system operations like directory creation and file path management.

### File Formats Supported

- **PDF**: Processed using `PyMuPDFLoader`.
- **CSV**: Processed using `CSVLoader`.
- **TXT**: Processed using `TextLoader`.
- **Additional Formats** (from `ingest.py`): DOC, DOCX, EML, EPUB, HTML, Markdown, ODT, PPT, PPTX.

## 📂 Project Structure

```

├── Trial.py              # Basic script to initialize ChromaDB and test collection creation
├── constants.py          # Configuration for ChromaDB settings and environment variables
├── ingest.py             # Script for loading, chunking, and embedding documents into ChromaDB
├── LLM\_tool.py           # Streamlit app for document upload, processing, and conversational querying
├── htmltemplate.py       # Placeholder file (no content provided)
├── source\_documents/     # Directory for source documents (PDF, CSV, TXT, etc.)
├── db/                   # Directory for ChromaDB persistent storage
└── .env                  # Environment variables (not included in repo)

```

## ✨ Features

- **Multi-Format Document Support**: Upload and process various document types (PDF, CSV, TXT, and more).
- **Efficient Document Processing**: Splits documents into chunks (default: 500 tokens, 50-token overlap) for optimal embedding and retrieval.
- **Vector Storage**: Uses ChromaDB to store document embeddings for fast similarity searches.
- **Conversational AI**: Query documents using a conversational interface powered by Cohere, OpenAI, or Ollama (Llama3).
- **Interactive UI**: Streamlit-based frontend with custom styling, avatars, and a sidebar for document uploads.
- **Progress Tracking**: Displays progress bars during document processing for a better user experience.
- **Persistent Storage**: Stores embeddings in a local ChromaDB instance for reuse across sessions.
- **Customizable Configuration**: Environment variables for paths, model selection, and chunking parameters.

## 🖥️ Frontend Details

The frontend, designed by Reddipalli Sai Charish, is built using Streamlit and features:

- **Chat Interface**: A clean, modern chat UI with distinct styling for user and bot messages.
  - User messages: Dark background (#2b313e) with a user avatar.
  - Bot messages: Lighter background (#475063) with a bot avatar.

- **Custom CSS**: Defined in `LLM_tool.py` for styling the chat UI and sidebar.
- **Logos**: Two logos (`CampusX.jfif` and `Q&A logo.jfif`) displayed in the header for branding.
- **Sidebar**: Allows users to upload multiple documents and trigger processing.
- **Responsive Design**: Sidebar width is fixed at 300px for consistency.

## ⚙️ Setup Instructions

### Prerequisites

- **Python 3.8+**
- **Dependencies**: Install required packages using the provided `requirements.txt` (see below).
- **Environment Variables**: Create a `.env` file with the following:
```

PERSIST\_DIRECTORY=db
SOURCE\_DIRECTORY=source\_documents
EMBEDDINGS\_MODEL\_NAME=Cohereembeddings
MODEL\_TYPE=Llama3
TARGET\_SOURCE\_CHUNKS=5

````

### Installation

1. **Clone the Repository**:
 ```bash
 git clone https://github.com/reddipallisaicharish/document-insights-generator.git
 cd document-insights-generator
````

2. **Create a Virtual Environment**:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   Create a `requirements.txt` file with the following content:

   ```txt
   chromadb
   langchain
   langchain-cohere
   langchain-community
   streamlit
   python-dotenv
   tqdm
   pypdf
   pillow
   ```

   Then run:

   ```bash
   pip install -r requirements.txt
   ```

4. **Set Up Environment Variables**:
   Create a `.env` file in the project root with the variables listed above.

5. **Run the Application**:

   ```bash
   streamlit run LLM_tool.py
   ```

## 📖 Usage

1. **Run the Streamlit App**:

   ```bash
   streamlit run LLM_tool.py
   ```

2. **Upload Documents**:

   * Use the sidebar to upload PDF, CSV, or TXT files.
   * Click the "Process" button to load, chunk, and embed the documents.

3. **Query Documents**:

   * Enter a question in the text input field.
   * The app will respond with answers based on the document content, maintaining conversation history.

## 🐛 Troubleshooting

* **.env File Not Found**: Ensure the `.env` file exists in the project root and contains the required variables.
* **Unsupported File Extension**: Only PDF, CSV, and TXT are supported in `LLM_tool.py`. For additional formats, use `ingest.py`.
* **Embedding Errors**: Verify that `EMBEDDINGS_MODEL_NAME` is set correctly (`Cohereembeddings` or `openai`) and that API keys are configured for Cohere or OpenAI.
* **ChromaDB Issues**: Ensure the `PERSIST_DIRECTORY` path exists and is writable.

## 📝 Future Improvements

* Add support for more file formats in the Streamlit app (e.g., DOCX, HTML).
* Implement batch processing for large document sets in `LLM_tool.py`.
* Enhance the frontend with additional styling options or themes.
* Add support for more LLM models (e.g., other Hugging Face models).
* Improve error handling for invalid file uploads or network issues.

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Create a Pull Request.

## 📜 License

This project is licensed under the MIT License. See the LICENSE file for details.

## 📬 Contact

For questions or feedback, reach out to Reddipalli Sai Charish at [your.email@example.com](mailto:your.email@example.com) or open an issue on GitHub.

---

## ✅ Additional Enhancements Made

* **Streamlit Cloud Deployment Ready**: Successfully deployed the project on [Streamlit Cloud](https://dsznc3oklyxyxdxfmykzwm.streamlit.app/).
* **Folder Structure Refactor**: Cleaned and pushed only necessary files to the GitHub repo for streamlined deployment.
* **Force Push & Repo Syncing**: Handled Git conflicts and force-synced local changes to [Charish53/RAG](https://github.com/Charish53/RAG).
* **Streamlit Bug Fixes**: Resolved `NoneType` call error in `st.session_state.conversation`.
* **Environment Setup Assistance**: Ensured `.env`, `requirements.txt`, and runtime configurations are clearly documented and functional.

---

Built with ❤️ by Reddipalli Sai Charish — Empower your documents with intelligent insights!


