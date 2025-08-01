# Gemini Batch Prediction Framework

> **Google Summer of Code 2025 Project**
> Creating efficient video content analysis through intelligent batching and context caching with the Gemini API

**Organization:** Google DeepMind

---

## 🎯 Project Overview

This project develops a framework for efficiently analyzing educational video content using Google's Gemini API. By implementing intelligent batch processing and context caching strategies, we achieve **4-5x reduction in API calls** with **up to 75% cost savings** while maintaining high-quality responses for educational content analysis.

### Key Features

- **Batch Processing**: Group related questions to minimize redundant API calls
- **Context Caching**: Leverage Gemini's implicit and explicit caching for cost reduction
- **Multimodal Analysis**: Support text, PDFs, videos, images, YouTube URLs, and mixed content
- **Conversation Memory**: Maintain coherent follow-up question handling across multi-source analysis
- **Professional Infrastructure**: Production-ready CI/CD, automated testing, and semantic versioning
- **Performance Monitoring**: Ultra-low overhead telemetry system with extensible reporting

## 🚀 Current Status

**Foundation & Multimodal Processing (Weeks 1-3)**: ✅ **COMPLETED**

- Production-ready API client with comprehensive error handling and rate limiting
- Unified interface for any content type (text, files, URLs, directories, YouTube)
- Files API integration and multi-source analysis capabilities

**Advanced Features (Weeks 4-6)**: ✅ **COMPLETED**

- Intelligent context caching with up to 75% cost reduction
- Multi-turn conversation memory with session persistence and context overflow handling
- Performance monitoring infrastructure and architectural modernization

**Professional Infrastructure (Weeks 7-8)**: ✅ **COMPLETED**

- Comprehensive testing foundation with characterization tests and 95%+ coverage
- Modern CI/CD pipeline with automated releases and changelog generation
- Professional Python tooling (ruff, mypy, pre-commit) and semantic versioning

**Next: Architectural Modernization (Week 9+)**: ⚪ **CURRENT**

- Pipeline architecture refactor for enhanced maintainability and performance
- Advanced video processing features and optimization
- Final delivery preparation and documentation

## 📦 Installation

### Recommended: Stable Release

**[📥 Visit Releases Page](https://github.com/seanbrar/gemini-batch-prediction/releases/latest)** to download the latest stable version.

```bash
# Download either the .whl or .tar.gz file, then:
pip install gemini_batch-*.whl                    # For wheel files
# OR
pip install "gemini_batch-*.tar.gz[viz]"          # For source with visualization support
```

### Development Version

For the latest features and improvements (may be less stable):

```bash
git clone https://github.com/seanbrar/gemini-batch-prediction.git
cd gemini-batch-prediction
pip install -e ".[viz]"
```

<details>
<summary><b>👩‍💻 Developer Setup</b></summary>
<br>
If you want to contribute to the project or run tests, install the full development environment:

```bash
# Install development dependencies (includes testing, linting, etc.)
pip install -r dev-requirements.txt

# Verify setup with tests
make test

# See all available development commands
make help
```

This project uses modern Python tooling including `ruff`, `mypy`, `pre-commit`, and `pytest` for a professional development experience.

</details>

### API Key Setup

Get your API key from [Google AI Studio](https://ai.dev/) and configure:

```bash
# Create .env file
GEMINI_API_KEY=your_api_key_here
GEMINI_MODEL=gemini-2.0-flash
GEMINI_ENABLE_CACHING=true     # Enable context caching
GEMINI_TIER=free              # Options: free, tier_1, tier_2, tier_3
```

See [docs/SETUP.md](docs/SETUP.md) for detailed configuration options.

### ⚡ Rate Limit Configuration

**Important**: Gemini API rate limits vary substantially by billing tier. Configure your tier for optimal performance:

**Check your tier in Google AI Studio → Billing:**

- `free` - No billing enabled (default)
- `tier_1` - Billing enabled (most common paid tier)
- `tier_2`, `tier_3` - Higher volume plans

**Without tier configuration**, all users default to free tier limits.

## 🔥 Quick Start

### Basic Usage with Caching

```python
from gemini_batch import BatchProcessor

# Automatic caching for supported models
processor = BatchProcessor(enable_caching=True)

questions = ["What are the main points?", "What are the key insights?"]

# Works with any content type
results = processor.process_questions("content.pdf", questions)
```

### Conversation Analysis

```python
from gemini_batch import create_conversation

# Create persistent conversation session
session = create_conversation("research_papers/")

# Ask initial questions
answers = session.ask_multiple([
    "What are the main research themes?",
    "Which papers discuss efficiency techniques?"
])

# Natural follow-up with full context
followup = session.ask("How do these techniques compare in practice?")

# Session automatically maintains context and can be saved/loaded
session_id = session.save()
```

### Unified Content Processing

```python
questions = ["What are the main points?", "What are the key insights?"]

# YouTube video
results = processor.process_questions("https://youtube.com/watch?v=example", questions)

# Multiple research sources
sources = [
    "research_papers/",           # Directory of papers
    "https://arxiv.org/pdf/...",  # arXiv paper
    "https://youtube.com/watch?v=...",  # Educational video
]

# Single API call processes all sources with caching
results = processor.process_questions_multi_source(sources, questions)
```

### Configuration Options

```python
# Automatic tier detection from environment
processor = BatchProcessor()  # Reads GEMINI_TIER from .env

# Or specify explicitly
from gemini_batch.config import APITier
processor = BatchProcessor(tier=APITier.TIER_1)
```

## 📚 Documentation

### Core Guides

- **[Setup Guide](docs/SETUP.md)** - Installation and configuration
- **[Context Caching](docs/CACHING.md)** - Cost optimization with caching strategies
- **[Conversation System](docs/CONVERSATION.md)** - Multi-turn analysis and session management
- **[Source Handling](docs/SOURCE_HANDLING.md)** - Working with different content types

### Examples & Demos

- **[Examples Directory](examples/)** - Complete usage demonstrations
- **[Research Notebook](notebooks/literature_review_demo.ipynb)** - Academic workflow with 12 sources

## 🛠️ Development Roadmap

| Week | Focus | Status |
|------|-------|--------|
| 1-3 | Foundation, testing & multimodal processing | ✅ **Completed** |
| 4-5 | Context caching & conversation memory | ✅ **Completed** |
| 6 | Performance infrastructure & architecture modernization | ✅ **Completed** |
| 7-8 | Testing foundation & professional infrastructure | ✅ **Completed** |
| 9-11 | Architectural refactor & advanced optimization | ⚪ **Current** |
| 12-13 | Documentation & final delivery | ⚪ Planned |

## 🤝 Contributing

This is a Google Summer of Code project under active development. Feedback and suggestions are welcome! Please open an issue or reach out directly.

For technical implementation details, see the [development documentation](dev/).

## 📄 License

[MIT License](LICENSE) - This project is developed as part of Google Summer of Code 2025.

---

**Note**: This is an active GSoC project. Features and APIs may change as development progresses. Check back weekly for updates!
