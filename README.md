# 🤖 Multi-Agent AI Research & Report Generator

A **Generative AI / Agentic AI** project built with **CrewAI, Ollama, and Llama 3.2 1B** that demonstrates how multiple specialized AI agents can collaborate to research a topic and generate a concise report.

The current system uses two AI agents:

- 🔎 **Researcher Agent** — identifies major trends related to a given topic.
- ✍️ **Writer Agent** — converts the research findings into a concise formatted report.

---

## 📌 About the Project

This project demonstrates a basic **multi-agent AI workflow**, where different agents are assigned different responsibilities instead of asking a single LLM to perform the entire task.

### Core Workflow

```text
                    User Topic
                        │
                        ▼
              ┌──────────────────┐
              │ Researcher Agent │
              │                  │
              │ Identifies major │
              │ trends/findings  │
              └────────┬─────────┘
                       │
                 Research Output
                       │
                       ▼
              ┌──────────────────┐
              │   Writer Agent   │
              │                  │
              │ Summarizes the   │
              │ research findings│
              └────────┬─────────┘
                       │
                       ▼
                  Final Report
```

The notebook demonstrates this workflow using **Agentic AI** as the research topic.

---

## 🎯 Project Objective

The main objective is to explore how multiple AI agents can collaborate to complete a larger task.

Instead of:

```text
User → One LLM → Final Answer
```

the project uses:

```text
User
 ↓
Researcher Agent
 ↓
Research Findings
 ↓
Writer Agent
 ↓
Final Report
```

This demonstrates the fundamental concept of **multi-agent orchestration**.

---

## 🛠️ Tools & Languages Used

| Technology | Purpose |
|---|---|
| **Python 3.11.9** | Core programming language |
| **CrewAI** | AI agent creation and orchestration |
| **Ollama** | Local LLM runtime |
| **Llama 3.2 1B** | Language model |
| **Jupyter Notebook** | Development and experimentation |

### LLM

The project uses:

```text
Llama 3.2 1B
```

through Ollama:

```python
local_llm = LLM(
    model="ollama/llama3.2:1b",
    base_url="http://localhost:11434"
)
```

This allows the project to use a locally running language model rather than a cloud-based LLM API.

---

## 🤖 AI Agents

### 🔎 Researcher Agent

**Role:** Researcher

**Goal:** Identify 3 major trends in the given topic.

The Researcher is responsible for identifying important trends and producing a bulleted list of the top three findings.

### ✍️ Writer Agent

**Role:** Writer

**Goal:** Summarize the research findings into a short report.

The Writer receives the Researcher's output and converts it into a clean, formatted report.

---

## ⚙️ How It Works

### 1. Configure the LLM

Llama 3.2 1B is configured through Ollama and used as the underlying model for both agents.

### 2. Create the Researcher

A specialized Researcher Agent is created to identify major trends related to the selected topic.

### 3. Create the Writer

A second Writer Agent is created to transform the research findings into a concise report.

### 4. Define Tasks

Two tasks are created:

```text
Research Task
      ↓
Identify 3 major trends
      ↓
Writer Task
      ↓
Create a concise report
```

### 5. Create the Crew

CrewAI orchestrates both agents and their tasks.

```python
crew = Crew(
    agents=[researcher, writer],
    tasks=[research_task, write_task],
    memory=False,
    verbose=True
)
```

### 6. Execute

The workflow is started with:

```python
crew.kickoff(inputs={'topic': 'Agentic AI'})
```

The Researcher executes first, followed by the Writer.

---

## 🧪 Demonstration

### Input

```text
Agentic AI
```

### Researcher

The Researcher identifies three major trends related to the topic.

### Writer

The Writer converts those findings into a formatted report.

The demonstrated workflow produces a report titled:

```text
Agentic AI Trends: A Summary Report
```

The notebook output shows the two agents executing sequentially and the final Crew output containing the generated report.

---

## 🔄 System Architecture

```text
                         Topic
                           │
                           ▼
                  ┌────────────────┐
                  │    CrewAI      │
                  │      Crew      │
                  └───────┬────────┘
                          │
                          ▼
                  ┌────────────────┐
                  │   Researcher   │
                  │     Agent      │
                  └───────┬────────┘
                          │
                    Research Output
                          │
                          ▼
                  ┌────────────────┐
                  │     Writer     │
                  │     Agent      │
                  └───────┬────────┘
                          │
                          ▼
                    Final Report
```

---

## 🧠 Key Concepts Demonstrated

- Generative AI
- Agentic AI
- Multi-Agent Systems
- AI Agent Roles
- Task Delegation
- Agent Orchestration
- Large Language Models (LLMs)
- Local LLMs
- CrewAI
- Ollama
- Llama Models
- Prompt Engineering
- Automated Research
- AI-powered Report Generation

---

## ⚠️ Current Limitations

The current version is a **proof-of-concept / learning project**.

### 1. No Actual Web Search

The Researcher task is instructed to search and analyze news, but the current implementation does **not** connect the agent to a web-search engine, news API, or external retrieval tool.

Therefore, this version should not be described as a real-time web research system.

### 2. LLM Knowledge Dependency

Without external retrieval, the freshness and accuracy of research depend on the local Llama model.

### 3. Only Two Agents

The current workflow contains:

```text
Researcher → Writer
```

There is no dedicated verification or analysis agent.

### 4. No Source Verification

The generated report does not currently provide reliable source citations or a dedicated fact-checking process.

### 5. No User Interface

The project currently runs through a Jupyter Notebook and does not include a web application.

---

# 🚀 Planned Improvements

## 🔎 1. Add Real Web Search

Integrate a web-search engine or news API with the Researcher Agent.

Future workflow:

```text
User Topic
    ↓
Researcher
    ↓
Web Search
    ↓
Relevant Sources
    ↓
Research Findings
```

This would turn the prototype into a more capable **AI Research Assistant**.

---

## 🧠 2. Add an Analysis Agent

Introduce a third specialized agent:

```text
Researcher
     ↓
Analyst
     ↓
Writer
```

**Researcher:** Collects information.

**Analyst:** Compares findings and identifies the most important insights.

**Writer:** Produces the final report.

---

## ✅ 3. Add a Verification Agent

Add an agent dedicated to checking the research before the final report is generated.

```text
Researcher
     ↓
Verifier
     ↓
Writer
```

The Verifier could check:

- Consistency
- Relevance
- Unsupported claims
- Duplicate information
- Source quality

---

## 🔗 4. Add Source Citations

Future reports should include sources for important findings.

```text
Finding
   ↓
Source
   ↓
Citation
```

This would improve transparency, reliability, and usefulness.

---

## 💬 5. Add Interactive User Input

Allow users to enter any topic dynamically.

Example:

```text
Enter topic:
Generative AI in Healthcare
```

The multi-agent workflow would then research the selected topic and generate a report.

---

## 🌐 6. Build a Streamlit Interface

Create a user-friendly web application where users can:

- Enter a research topic
- Start the AI research workflow
- View research findings
- View the generated report
- View sources
- Download the final report

---

## 📈 Future Architecture

```text
                         User
                           │
                           ▼
                    ┌──────────────┐
                    │ Streamlit UI │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │    CrewAI    │
                    │     Crew     │
                    └──────┬───────┘
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
        Researcher      Analyst       Verifier
             │             │             │
             └─────────────┼─────────────┘
                           ▼
                         Writer
                           │
                           ▼
                     Final Report
                           │
                           ▼
                    Sources / Citations
```

---

## 📂 Repository Structure

```text
multi-agent-ai-research-assistant/
│
├── agenticai.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

---

## ⚙️ Installation

### Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/multi-agent-ai-research-assistant.git
cd multi-agent-ai-research-assistant
```

### Create Virtual Environment

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

Example `requirements.txt`:

```text
crewai
ollama
jupyter
ipykernel
```

### Ollama

Install Ollama and make sure the required model is available:

```text
llama3.2:1b
```

The project expects Ollama to run locally at:

```text
http://localhost:11434
```

### Run

Open:

```text
agenticai.ipynb
```

in Jupyter Notebook or VS Code and execute the cells sequentially.

---

## 📚 Learning Outcomes

This project provides hands-on experience with:

- Building AI agents using CrewAI
- Designing specialized agent roles
- Creating multi-agent workflows
- Connecting local LLMs using Ollama
- Using Llama models in AI applications
- Passing information between agent tasks
- Automating research and report generation
- Understanding the limitations of LLM-only research systems

---

## 🏷️ Keywords

`Generative AI` `GenAI` `Agentic AI` `AI Agents` `Multi-Agent Systems` `CrewAI` `Ollama` `Llama 3.2` `LLM` `Local LLM` `AI Research Assistant` `Report Generation` `Agent Orchestration` `Python` `Prompt Engineering` `Artificial Intelligence`

---

## 📌 Project Status

🟡 **Proof of Concept / Learning Project**

The current version demonstrates a two-agent CrewAI workflow powered by a local Llama 3.2 1B model.

The planned roadmap focuses on adding real web research, source verification, additional specialized agents, citations, and a user-facing interface.

---

## 👨‍💻 Author

**Arjun Vijayan**

Aspiring **AI/ML Engineer | Data Scientist | Data Analyst**

### Areas of Interest

- Artificial Intelligence
- Generative AI
- Agentic AI
- Machine Learning
- Data Science
- Data Analytics
- Large Language Models

