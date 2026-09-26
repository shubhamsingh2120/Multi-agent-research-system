# 🔬 ResearchMind — Multi-Agent AI Research Assistant

ResearchMind is a **Multi-Agent AI Research Assistant** that automates the process of researching a topic, gathering web information, extracting detailed content, generating a structured research report, and critically reviewing the final output.

The system uses specialized AI agents and chains for different stages of the research workflow:

**Search → Read → Write → Critique**

The application provides an interactive **Streamlit web interface** where users can enter a research topic and run the complete research pipeline.

---

## 🚀 Project Overview

Traditional research often requires manually searching multiple websites, reading articles, organizing information, writing a report, and reviewing the final content.

ResearchMind automates this workflow using a multi-agent architecture.

Given a research topic, the system:

1. Searches the web for recent and reliable information.
2. Selects and scrapes a relevant resource for deeper research.
3. Combines the gathered information.
4. Generates a structured research report.
5. Reviews the generated report using a dedicated critic chain.
6. Displays the results through a Streamlit interface.
7. Allows the final report to be downloaded as a Markdown file.

The Streamlit interface explicitly presents four stages: **Search Agent, Reader Agent, Writer Chain, and Critic Chain**.

---

## ✨ Key Features

* 🤖 Multi-agent AI research workflow
* 🔎 Web search using Tavily
* 🌐 Web-page scraping using BeautifulSoup
* 📚 Deep content extraction
* ✍️ Automated research report generation
* 🧐 AI-powered report criticism
* 📊 Structured research pipeline
* 🖥️ Interactive Streamlit interface
* 📥 Markdown report download
* 🔄 Real-time pipeline status
* 🔐 Environment-variable based API configuration

---

## 🧠 Multi-Agent Architecture

The project separates the research process into specialized components.

### 1. Search Agent 🔍

The Search Agent searches the web for **recent, reliable, and detailed information** about the user's topic.

It uses the `web_search` tool and returns titles, URLs, and snippets from search results.

### 2. Reader Agent 📄

The Reader Agent selects a relevant URL from the search results and uses the scraping tool to retrieve deeper content from that source.

The scraper removes unnecessary elements such as:

* Scripts
* Styles
* Navigation
* Footer content

and extracts readable page text.

### 3. Writer Chain ✍️

The Writer Chain combines the search results and scraped content to generate a detailed research report.

The report is structured into:

* Introduction
* Key Findings
* Conclusion
* Sources

The prompt requires a minimum of three well-explained key findings and a list of URLs found during research.

### 4. Critic Chain 🧐

The Critic Chain reviews the generated report and provides:

* Score
* Strengths
* Areas to Improve
* One-line verdict

This provides an additional quality-review stage after report generation.

---

## 🔄 Research Workflow

```text
                 User
                  │
                  ▼
          Enter Research Topic
                  │
                  ▼
        ┌──────────────────┐
        │   Search Agent   │
        │  Tavily Search   │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │   Reader Agent   │
        │  Web Scraping    │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │   Writer Chain   │
        │ Research Report  │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │   Critic Chain   │
        │ Quality Review   │
        └────────┬─────────┘
                 │
                 ▼
          Final Research
             Report
```

## The same four-stage workflow is implemented in the standalone `pipeline.py` execution flow.

## 🏗️ Project Architecture

```text
ResearchMind
│
├── Streamlit UI
│
├── Search Agent
│      └── Tavily Web Search
│
├── Reader Agent
│      └── URL Scraper
│          ├── Requests
│          └── BeautifulSoup
│
├── Writer Chain
│      └── OpenAI LLM
│
└── Critic Chain
       └── OpenAI LLM
```

The agents are created using LangChain's agent framework, while the LLM is configured through `ChatOpenAI`.

---

## 🖥️ Streamlit Interface

The project includes a custom Streamlit interface called **ResearchMind**.

The UI provides:

* Research topic input
* Run Research Pipeline button
* Pipeline status indicators
* Search results
* Scraped content
* Final research report
* Critic feedback
* Markdown report download

The interface also provides example research topics such as:

```text
LLM agents 2025
CRISPR gene editing
Fusion energy progress
```

---

## 📑 Report Generation

The Writer Chain generates a professional report using the collected research.

The generated report follows this structure:

```text
Introduction

Key Findings
    ├── Finding 1
    ├── Finding 2
    └── Finding 3+

Conclusion

Sources
```

The final report is rendered directly in the Streamlit application and can be downloaded as a `.md` file.

---

## 🧐 AI Critic

After the report is generated, the Critic Chain evaluates its quality.

Example output format:

```text
Score: X/10

Strengths:
- ...
- ...

Areas to Improve:
- ...
- ...

One line verdict:
...
```

The critic output is displayed separately from the final research report.

---

## 🛠️ Technologies Used

### AI / LLM

* OpenAI
* LangChain
* LangChain Agents

### Web Research

* Tavily
* Requests
* BeautifulSoup
* lxml

### Application

* Streamlit
* Python

### Supporting Libraries

* Pydantic
* Pandas
* aiohttp
* tiktoken
* Rich
* Tenacity
* orjson

The project's requirements file includes the LangChain ecosystem, OpenAI, Tavily, BeautifulSoup, Requests, dotenv, and supporting libraries.

---

## 📁 Project Structure

```text
ResearchMind/
│
├── app.py
├── agents.py
├── pipeline.py
├── tools.py
├── requirements.txt
├── .gitignore
└── README.md
```

### `app.py`

Contains the Streamlit user interface and executes the complete research workflow.

### `agents.py`

Contains:

* Search Agent
* Reader Agent
* Writer Chain
* Critic Chain

### `pipeline.py`

Provides a standalone Python implementation for running the complete research pipeline from the terminal.

### `tools.py`

Contains the web search and URL scraping tools.

---

## ⚙️ Environment Variables

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
```

Do not commit your `.env` file or API keys to GitHub.

---

## ▶️ Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/researchmind.git
cd researchmind
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

### 3. Activate the Environment

**Windows:**

```bash
venv\Scripts\activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Configure API Keys

Create a `.env` file:

```env
OPENAI_API_KEY=your_api_key
TAVILY_API_KEY=your_api_key
```

### 6. Run the Application

```bash
streamlit run app.py
```

---

## 💻 Run Without Streamlit

The research pipeline can also be executed directly from the terminal:

```bash
python pipeline.py
```

You will then be prompted to enter a research topic.

The standalone pipeline executes Search → Reader → Writer → Critic and returns the complete state containing the search results, scraped content, generated report, and critic feedback.

---

## 🔍 Example

### Input

```text
Quantum Computing Breakthroughs
```

### Pipeline

```text
🔍 Search Agent
       ↓
📄 Reader Agent
       ↓
✍️ Writer Chain
       ↓
🧐 Critic Chain
       ↓
📝 Final Research Report
```

### Output

The application produces:

* Search results
* Scraped research content
* Structured research report
* Critic feedback

---

## 🎯 Use Cases

ResearchMind can be used for:

* Technology research
* Market research
* Academic research assistance
* AI/ML topic exploration
* Industry research
* Competitive research
* News and trend analysis
* Research report generation
* Information gathering and summarization

---

## 🔮 Future Improvements

Potential improvements include:

* Multi-source scraping instead of selecting a single URL
* Parallel research agents
* Source credibility scoring
* Citation verification
* Fact-checking agent
* PDF report generation
* Persistent research history
* Vector database integration
* RAG-based knowledge retrieval
* User authentication
* Research comparison across multiple topics
* Better error handling and retry mechanisms
* Deployment with Docker

---

## ⚠️ Limitations

The current implementation depends on external web search and scraping services.

The Reader Agent currently selects a relevant URL from the search output and scrapes that source for deeper content.

Therefore, results may depend on:

* Search engine results
* Website availability
* Website structure
* Scraping restrictions
* API availability
* LLM-generated content

ResearchMind should be treated as a research-assistance tool, and important information should be independently verified.

---

## 👨‍💻 Author

**Shubham Singh**

B.Tech – Information Technology

Interested in:

**Artificial Intelligence • Machine Learning • Data Science • Python • NLP • Generative AI**

---

## ⭐ If You Find This Project Useful

Consider giving the repository a ⭐ on GitHub.
