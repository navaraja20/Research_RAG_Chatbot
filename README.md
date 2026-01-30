# Research RAG Bot 🤖📚

A powerful Retrieval-Augmented Generation (RAG) chatbot that enables intelligent conversations about research papers using local LLMs via Ollama and LangChain.

## 🌟 Overview

This project implements a conversational AI system that can read, understand, and answer questions about research papers. It uses the RAG architecture to combine the power of large language models with document retrieval, ensuring accurate and contextual responses based on the actual content of your research papers.

## ✨ Features

- **📄 PDF Processing**: Automatically loads and processes research papers in PDF format
- **🔍 Intelligent Chunking**: Splits documents into manageable chunks with overlap for better context preservation
- **💾 Vector Storage**: Uses FAISS for efficient similarity search and retrieval
- **🧠 Local LLM Integration**: Powered by Llama 3.1 (8B) via Ollama - runs completely offline
- **💬 Conversational Memory**: Maintains chat history for contextual follow-up questions
- **⚡ Fast Retrieval**: Quick document search using embedding-based semantic similarity
- **🔒 Privacy-Focused**: All processing happens locally - no data sent to external APIs

## 🛠️ Technologies Used

- **LangChain**: Framework for building LLM applications
- **Ollama**: Local LLM runtime (Llama 3.1:8b)
- **FAISS**: Facebook AI Similarity Search for vector storage
- **PyPDF**: PDF document processing
- **Python**: Core programming language

## 📋 Prerequisites

Before running this project, ensure you have:

1. **Python 3.8+** installed
2. **Ollama** installed and running ([Download Ollama](https://ollama.ai))
3. **Llama 3.1:8b model** pulled in Ollama:
   ```bash
   ollama pull llama3.1:8b
   ```

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd "Research RAG BOT"
   ```

2. **Install required dependencies**
   ```bash
   pip install langchain langchain-ollama faiss-cpu pypdf requests
   ```

3. **Verify Ollama is running**
   ```bash
   ollama list
   ```
   Ensure `llama3.1:8b` is in the list.

## 📖 Usage

### Basic Setup

1. **Place your PDF research paper** in the project directory (e.g., `RAGPaper.pdf`)

2. **Open the Jupyter Notebook**
   ```bash
   jupyter notebook "Research RAG bot.ipynb"
   ```

3. **Run the cells sequentially** to:
   - Initialize the LLM
   - Load and process your PDF
   - Create vector embeddings
   - Set up the conversational chain

### Example Queries

```python
# Ask questions about your research paper
query = "What is this research paper all about, explain it in 2-3 lines"
result = qa({"question": query, "chat_history": chat_history})
print(result['answer'])

# Follow-up questions maintain context
chat_history.append((query, result['answer']))
query = "What are the main findings?"
result = qa({"question": query, "chat_history": chat_history})
print(result['answer'])
```

## 🏗️ Architecture

```
┌─────────────────┐
│   PDF Document  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  PyPDFLoader    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Text Splitter   │ (1000 char chunks, 200 overlap)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Embeddings    │ (Llama 3.1:8b via Ollama)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  FAISS Vector   │
│     Store       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Conversational  │
│ Retrieval Chain │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   LLM Response  │ (Llama 3.1:8b)
└─────────────────┘
```

## ⚙️ Configuration

You can customize the following parameters:

- **Chunk Size**: Adjust `chunk_size=1000` for larger/smaller text segments
- **Chunk Overlap**: Modify `chunk_overlap=200` to control context preservation
- **LLM Model**: Change `model='llama3.1:8b'` to use different Ollama models
- **Retriever Settings**: Customize retrieval parameters in `db.as_retriever()`

## 📝 Code Structure

- **Cell 1**: Import dependencies
- **Cell 2**: Initialize the LLM (Llama 3.1:8b)
- **Cell 3-4**: Test basic LLM functionality
- **Cell 5**: Load PDF and split into chunks
- **Cell 6**: Create embeddings and FAISS vector store
- **Cell 7**: Set up conversational retrieval chain with custom prompt
- **Cell 8**: Query the system and get responses

## 🔧 Troubleshooting

### Common Issues

1. **Ollama connection error**
   - Ensure Ollama is running: `ollama serve`
   - Check if the model is available: `ollama list`

2. **Memory issues**
   - Reduce `chunk_size` to process smaller segments
   - Consider using a smaller model

3. **PDF loading errors**
   - Ensure the PDF path is correct
   - Check PDF file is not corrupted
   - Verify file permissions

## 🎯 Use Cases

- **Research Paper Analysis**: Quickly understand complex academic papers
- **Literature Review**: Extract key information from multiple papers
- **Study Assistant**: Get explanations of difficult concepts
- **Citation Finding**: Locate specific information within papers
- **Paper Summarization**: Generate concise summaries of lengthy documents

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest new features
- Submit pull requests
- Improve documentation

## 📄 License

This project is open-source and available under the MIT License.

## 🙏 Acknowledgments

- LangChain team for the excellent framework
- Ollama for making local LLM inference accessible
- Meta for the Llama model
- Facebook AI Research for FAISS

## 📧 Contact

For questions or feedback, please open an issue in the repository.

---

**Happy Researching! 🎓✨**
