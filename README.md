# Local Web Scraping AI Agent

A small Streamlit app that scrapes a web page and pulls out the data you ask for in plain English. It runs fully on your own machine using **Llama 3.2 via Ollama**, so there are no API costs and nothing leaves your laptop. An OpenAI-powered version is included as an alternative.

Built and tested on a MacBook Air (Apple M2) with Python 3.11.

---

## Features

- Describe what you want in natural language, for example "List the titles of the top 10 stories".
- Runs locally with Llama 3.2 through Ollama, with no API key required.
- Optional OpenAI mode if you prefer a hosted model.
- Simple Streamlit interface: enter a URL, enter a prompt, click Scrape.

## Project Structure

```
web-scraping-ai-agent/
├── local_ai_scrapper.py   # Local version (Ollama + Llama 3.2)
├── ai_scrapper.py         # Hosted version (needs an OpenAI API key)
├── requirements.txt       # Pinned dependencies
└── README.md
```

## Requirements

- macOS (should also work on Linux)
- Python 3.11
- [Ollama](https://ollama.com) (for the local version)
- Git

## Setup

**1. Clone the repo**

```bash
git clone https://github.com/harshitmis1508/web-scraping-ai-agent.git
cd web-scraping-ai-agent
```

**2. Create a virtual environment and install dependencies**

```bash
python3.11 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
playwright install
```

**3. Install Ollama and download the models**

```bash
brew install ollama
ollama serve
```

Leave that terminal running, open a new tab, and run:

```bash
ollama pull llama3.2
ollama pull nomic-embed-text
```

## Run

**Local mode (free, no API key):**

```bash
streamlit run local_ai_scrapper.py
```

**OpenAI mode (needs an API key):**

```bash
streamlit run ai_scrapper.py
```

Then open http://localhost:8501, paste a URL, describe what you want, press Enter, and click **Scrape**.

## Example Prompts

| Website type | Example prompt |
|---|---|
| News / forums | `Extract the title and link of the top 10 stories` |
| Online stores | `Extract product names, prices, and availability` |
| Blogs | `Extract the article title, author, and date` |
| Company pages | `Find company names, emails, and phone numbers` |

Tip: start with small, simple pages and ask for a limited number of items. A local model on a laptop can take a few minutes on large pages.

## Troubleshooting

**`ImportError: cannot import name 'ChatOllama' from 'langchain_community.chat_models'`**
Newer LangChain releases removed this import. This repo pins compatible versions in `requirements.txt` (`scrapegraphai==1.50.0` with `langchain<0.4`), so install from that file instead of upgrading packages.

**Browser or Playwright errors**
Run `playwright install` inside the virtual environment.

**Scrape hangs or fails in local mode**
Make sure `ollama serve` is still running in its own terminal tab, and check with `ollama list` that `llama3.2` and `nomic-embed-text` are downloaded.

**`scrapegraphai` 2.x will not install**
Version 2.x needs Python 3.12 or newer. This project uses Python 3.11 with the 1.x series.

## Responsible Use

Only scrape websites you are allowed to scrape. Check each site's terms of service and `robots.txt` before use.


