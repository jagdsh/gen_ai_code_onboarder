# 🤖 CodeBuddy: The Open-Source Onboarder

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![LangChain](https://img.shields.io/badge/LangChain-Integration-green)](https://python.langchain.com/)
[![Ollama](https://img.shields.io/badge/Ollama-Local_LLM-orange)](https://ollama.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**CodeBuddy** is an AI-powered, 100% local open-source onboarding assistant built entirely in a Jupyter Notebook. It helps developers quickly understand new codebases, navigate architecture, and check live repository status without sending proprietary code to cloud APIs.

By combining a **Retrieval-Augmented Generation (RAG)** pipeline with **Agentic Tool Calling**, CodeBuddy reads GitHub repositories dynamically and answers complex developer questions in real-time.

---

## 🏗️ System Architecture



CodeBuddy utilizes a "split-brain" routing architecture:
1. **Dynamic Ingestion:** Clones a target GitHub repository, chunks the source code using a code-aware text splitter, and embeds it into a local Chroma vector database.
2. **Intent Routing:** Analyzes user queries to determine if the developer is asking about static code logic or dynamic repository status.
3. **Local RAG Pipeline:** For codebase questions, it searches the Chroma DB and passes context to a local LLM to generate precise, grounded explanations.
4. **Agentic API Tools:** For questions about open Pull Requests or live Issues, it bypasses the database and triggers a LangChain Agent to fetch real-time data from the GitHub REST API.

---

## ✨ Features

* **🔌 Dynamic GitHub Ingestion:** Just paste a GitHub URL, and the system automatically clones, parses, and indexes the repository.
* **🧠 Code-Aware Chunking:** Uses LangChain's Python language splitter to ensure functions and classes aren't broken during vectorization.
* **🔒 100% Local & Private:** Powered by Ollama. No OpenAI API keys required, and no source code is ever sent to the cloud.
* **⚡ Split-Brain Routing:** Intelligently switches between Vector Search (for code explanations) and Agentic Tool Use (for live GitHub data).
* **💻 Interactive UI:** Features a sleek, inline chat interface built with `ipywidgets` directly inside the Jupyter Notebook.

---

## 🛠️ Prerequisites

Because this project runs entirely locally, you must have the following installed on your machine before running the notebook:

1. **Python 3.10+**
2. **Jupyter Notebook** or an IDE that supports `.ipynb` files (like VS Code or PyCharm).
3. **[Ollama](https://ollama.com/)**: Required for running the local LLMs.

### Downloading the Local Models
Once Ollama is installed, open your terminal and pull the required model (we use `llama3.1` by default, but you can swap this in the code):
```bash
ollama pull llama3.1
```
(Note: Ensure the Ollama background app is running before executing the notebook!)

## 🚀 Installation & Setup
Clone this repository:

```Bash
git clone [https://github.com/yourusername/codebuddy.git](https://github.com/yourusername/codebuddy.git)
cd codebuddy
Create a virtual environment (Recommended):
```
```Bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
Install the required dependencies:
```
```Bash
pip install langchain langchain-ollama langchain-community chromadb GitPython ipywidgets requests
Launch the notebook:
```
```Bash
jupyter notebook CodeBuddy.ipynb
```
## 🎮 Usage
1. **Run all cells** in the CodeBuddy.ipynb notebook sequentially.
2. **Enter a Repository URL:** When prompted by the ingestion cell, paste the URL of the public GitHub repository you want to analyze (e.g., https://github.com/hwchase17/langchain-tiny).
3. **Chat:** Scroll down to the final cell (Phase 3). An interactive chat widget will appear.

**Example Questions to try:**
- "Where is the database connection handled in this repository?" (Triggers RAG Vector Search)
- "Explain how the authentication middleware works." (Triggers RAG Vector Search)
- "Are there any open pull requests right now?" (Triggers GitHub API Agent)
- Type exit or quit to close the chat interface gracefully.

## 🔮 Future Enhancements (Phase 4 Roadmap)
While CodeBuddy is currently a functional MVP, future iterations could include:

- **Multi-Language Support:** Expanding the GitLoader and Text Splitters to handle TypeScript, Rust, and Go files.

- **Cross-Repo Context:** Allowing the vector database to ingest multiple repositories simultaneously to answer questions about microservice interactions.

- **Automated PR Review Tooling:** Extending the Agent's capabilities to not just read PRs, but draft code reviews based on the repository's historical coding standards.

Built with LangChain & Ollama.