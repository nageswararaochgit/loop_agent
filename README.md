# Loop Agent

A self-correcting multi-agent system that uses LangGraph and Groq to generate high-quality explanations through an iterative review and revision process.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python Version](https://img.shields.io/badge/python-3.11+-green.svg)](https://www.python.org/downloads/)

## 🎯 Overview

Loop Agent demonstrates an intelligent multi-agent workflow where:
- A **Writer Agent** creates detailed, beginner-friendly explanations
- A **Reviewer Agent** evaluates the content against quality criteria
- The system **iteratively refines** answers until they meet quality standards

This project showcases how agentic AI can achieve better results through self-correction and multi-stage reasoning.

## ✨ Features

- **Multi-Agent Workflow**: Coordinated agents with specific roles (writer & reviewer)
- **Iterative Refinement**: Automatic revision loop for quality improvement
- **Fast & Reliable**: Powered by Groq's fast LLM inference
- **Web Interface**: Clean FastAPI-based UI for easy interaction
- **Configurable**: Customizable models, revision limits, and system prompts
- **Production-Ready**: Built with best practices using Pydantic & LangGraph

## 🚀 Quick Start

### Prerequisites

- Python 3.11 or higher
- Groq API Key ([Get one for free](https://console.groq.com))

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/loop-agent.git
   cd loop-agent
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   # On Windows
   venv\Scripts\activate
   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   ```bash
   cp .env.example .env
   # Edit .env and add your Groq API key
   ```

### Running the Application

Start the FastAPI server:

```bash
python app.py
```

Open your browser and navigate to:
```
http://localhost:8000
```

## 🏗️ Architecture

### System Components

```
┌─────────────┐
│  Web UI     │  (Jinja2 Templates + JavaScript)
└──────┬──────┘
       │
┌──────▼──────────────┐
│   FastAPI Server    │  (Request handling & API endpoints)
└──────┬──────────────┘
       │
┌──────▼──────────────────┐
│  LangGraph Workflow     │
│                        │
│  ┌────────────────┐    │
│  │ Writer Agent   │    │  Generates initial explanation
│  └────────┬───────┘    │
│           │            │
│  ┌────────▼────────┐   │
│  │ Reviewer Agent  │   │  Evaluates quality & provides feedback
│  └────────┬────────┘   │
│           │            │
│  ┌────────▼────────┐   │
│  │ Revision Loop   │   │  Repeats until approved or max revisions
│  └─────────────────┘   │
└──────┬──────────────────┘
       │
┌──────▼──────────────┐
│  Groq LLM API       │  (Fast inference)
└─────────────────────┘
```

### Workflow Steps

1. **User Input**: Topic submission via web interface
2. **Writing Phase**: Writer agent creates 120-160 word explanation
3. **Review Phase**: Reviewer agent evaluates against quality criteria
4. **Decision**:
   - ✅ **PASS**: Return the answer
   - ♻️ **REVISE**: Send feedback to writer for improvement
5. **Iteration**: Repeat until approved or max revisions reached

## ⚙️ Configuration

Environment variables in `.env`:

```env
# Groq API Configuration
GROQ_API_KEY=your_api_key_here
GROQ_MODEL=llama-3.3-70b-versatile

# Workflow Configuration
MAX_REVISIONS=2
```

### Available Models

Use any Groq-supported model:
- `llama-3.3-70b-versatile` (default)
- `llama-3.1-70b-versatile`
- `mixtral-8x7b-32768`
- [View all available models](https://console.groq.com/docs/models)

## 📁 Project Structure

```
loop-agent/
├── app.py                 # FastAPI application & routes
├── backend.py            # LangGraph workflow logic
├── requirements.txt      # Python dependencies
├── templates/
│   └── index.html       # Web interface template
├── static/
│   ├── app.js           # Frontend JavaScript
│   └── style.css        # Styling
├── .env.example         # Environment variables template
├── README.md            # This file
└── LICENSE              # MIT License
```

## 🔧 Development

### Project Dependencies

- **FastAPI**: Modern web framework for building APIs
- **LangGraph**: Graph-based workflow orchestration
- **LangChain**: LLM framework and utilities
- **Groq**: Fast LLM inference provider
- **Pydantic**: Data validation and settings management
- **Uvicorn**: ASGI web server

### Local Development

```bash
# Install with dev dependencies
pip install -r requirements.txt

# Run with auto-reload for development
uvicorn app:app --reload
```

### Testing the API

Use cURL or Postman to test the `/api/run` endpoint:

```bash
curl -X POST http://localhost:8000/api/run \
  -H "Content-Type: application/json" \
  -d '{"topic": "What is machine learning?"}'
```

## 📝 How It Works: Example

**User Input**: "Explain quantum computing"

**Writer's Response**:
```
Imagine a regular computer bit like a light switch - it's either ON (1) or OFF (0).
Quantum computing uses quantum bits or "qubits" that can be both ON and OFF at the 
same time through quantum superposition. It's like having a coin spinning in the air 
versus already landed. This allows quantum computers to explore many solutions 
simultaneously rather than one at a time, making them potentially powerful for 
specific problems like drug discovery or cryptography.
```

**Reviewer's Feedback**:
```
PASS - Clear explanation, good analogy, appropriate length, suitable for beginners
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙋 Support

Have questions? Issues? Please open an issue on GitHub or reach out to the maintainers.

---

**Built with ❤️ using LangGraph and Groq**