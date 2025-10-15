
# AAI-520-02-FINAL-PROJECT-GROUP-4

# 🧠 Multi-Agent Financial Analysis System – AAI-520 Final Project

  

### University of San Diego — Applied Artificial Intelligence (AAI-520)

**Team Members:**

-  **Alexander J. Padin**

-  **Thomas Geraci**

-  **Ali Mohtat**

## 📘 Project Overview

This project implements an **agentic AI financial research system** using **CrewAI**, **OpenAI GPT-4o**, and **Anthropic Claude 3.5 Sonnet**.

It demonstrates how autonomous AI agents can plan, research, critique, and iteratively improve investment analyses — mirroring real-world financial research workflows.

  

Each agent performs a distinct function in a self-improving multi-agent loop:

1.  **Planner** – designs a structured 5–7 step research plan for a given stock.

2.  **Researcher** – gathers and synthesizes data using Yahoo Finance tools.

3.  **Reviewer** – evaluates the draft, assigns a grade, and provides feedback.

4.  **Optimizer** – refines the report based on Reviewer feedback.

5.  **Archivist (Memory System)** – stores “lessons learned” for future runs.

  

These roles demonstrate all required **workflow patterns**:

-  **Prompt Chaining:** sequential pipeline from planning to refinement.

-  **Routing:** specialized agents handle distinct subtasks.

-  **Evaluator–Optimizer Loop:** Reviewer feedback drives the Optimizer’s improvements.

  

## 🧩 Key Features

- ✅ **Agentic AI Framework** – built with [CrewAI](https://github.com/joaomdmoura/crewAI)

- 🧠 **Multi-Model Reasoning** – integrates *GPT-4o* (OpenAI) and *Claude 3.5 Sonnet* (Anthropic)

- 💾 **Persistent Knowledge Memory** – JSONL-based memory across runs

- 📊 **Financial Data Retrieval** – via [yfinance](https://pypi.org/project/yfinance/) for OHLCV, fundamentals, dividends, and events

- 🔁 **Autonomous Feedback Cycle** – Reviewer → Optimizer → Memory

- 🧰 **Extensible Tools** – modular `@tool()` decorators for future APIs

  

## ⚙️ Installation and Setup

  

### Step 1 – Clone Repository

```bash

git  clone  https://github.com/apadin-repo/AAI-520-02-FINAL-PROJECT-GROUP-4.git

cd AAI-520-02-FINAL-PROJECT-GROUP-4

```

  

### Step 2 – Create Virtual Environment

```bash

python3  -m  venv  venv

source  venv/bin/activate  # macOS/Linux

venv\Scripts\activate  # Windows

```

  

### Step 3 – Install Dependencies

```bash

pip  install  -r  requirements.txt

```

If no `requirements.txt` exists:

```bash

pip  install  crewai  openai  anthropic  yfinance  pandas  python-dotenv  ipython

```

  

### Step 4 – Configure API Keys

Create a `.env` file in the project root:
``` 
touch notebook/.env
```
Add your keys:
```

OPENAI_API_KEY=your_openai_api_key_here

ANTHROPIC_API_KEY=your_anthropic_api_key_here

```

> ⚠️ Do **not** commit `.env` to GitHub.

  

### Step 5 – Run the Notebook

```bash

jupyter  notebook

```

Open and run `AAI520_Final_MultiAgentSystem.ipynb` 


## 📈 Example Run

```python

result = crew.kickoff(inputs={"ticker": "AAPL"})

```

Example output:

```
**SYNTHESIS**                                                                                                  │
│  Recent analysis of Apple Inc. (AAPL) reveals a stable stock trend over the past 90 days, with the latest       │
│  closing price at $256.48. Apple's current market capitalization is approximately $3.8 trillion, reflecting     │
│  strong investor confidence. The stock is nearing its 52-week high of $260.10, indicating a resilient upward    │
│  trajectory recently. A review of recent price movements highlights a support level around $254 and resistance  │
│  near $260, suggesting limited short-term volatility. Apple's consistent dividend payouts, with the most        │
│  recent being $0.26, indicate its commitment to returning value to shareholders. Despite no immediate earnings  │
│  announcements, analysts recommend a detailed examination of its revenue streams and product pipeline for more  │
│  strategic insights. Limited data on specific financial ratios currently emphasizes the need for peer           │
│  comparison and technical analysis.                                                                             │
│                                                                                                                 │
│  **RECOMMENDATION**                                                                                             │
│  HOLD - Considering the market position close to the 52-week high and stable dividend payouts, maintaining      │
│  current holdings is advised unless strategic opportunities or significant under/over-price movements occur.    │
│  Detailed assessments of AAPL’s product launches and service revenue growth are advisable for potential future  │
│  adjustments.                                                                                                   │
│                                                                                                                 │
│  **DATA SNAPSHOT**                                                                                              │
│  ```json                                                                                                        │
│  {                                                                                                              │
│    "ticker": "AAPL",                                                                                            │
│    "recommendation": "HOLD",                                                                                    │
│    "signals": {                                                                                                 │
│      "last_price": 256.48,                                                                                      │
│      "market_cap": 3809379872186.41,                                                                            │
│      "currency": "USD",                                                                                         │
│      "year_high": 260.10,                                                                                       │
│      "year_low": 169.21,                                                                                        │
│      "recent_dividends": [0.26, 0.26, 0.25, 0.25, 0.25],                                                        │
│      "support_level": 254,                                                                                      │
│      "resistance_level": 260                                                                                    │
│    },                                                                                                           │
│    "events": {                                                                                                  │
│      "upcoming_earnings": null                                                                                  │
│    },                                                                                                           │
│    "lessons_used": [                                                                                            │
│      "Always include key financial ratios, technical indicators, and competitive analysis to provide a          │
│  comprehensive and well-supported investment recommendation.",                                                  │
│      "Always provide a comprehensive analysis including financial ratios, competitive positioning, technical    │
│  indicators, and specific price targets, even when faced with data constraints."                                │
│    ]                                                                                                            │
│  }                                                                                                              │
│  ```
```


## 🧠 Agent Summary

| Agent | Purpose | Tools | LLM |
|-------|----------|--------|-----|
| **Planner** | Designs research plan | None | GPT-4o |
| **Researcher** | Collects & synthesizes data | `yf_prices`, `yf_fundamentals`, `yf_dividends`, `yf_calendar` | GPT-4o |
| **Reviewer** | Grades & critiques | Same tools + `save_kb_lesson_tool` | Claude 3.5 |
| **Optimizer** | Refines output | Same tools | GPT-4o |
| **Archivist** | Saves lessons | `load_kb_lessons_tool`, `save_kb_lesson_tool` | Claude 3.5 |


## 🧮 Workflow Patterns Demonstrated

| Pattern | Implementation |
|---------|----------------|
| **Prompt Chaining** | Sequential flow: Planner → Researcher → Reviewer → Optimizer → Archivist |
| **Routing** | Each agent uses specialized toolsets and distinct LLMs |
| **Evaluator–Optimizer Loop** | Reviewer critiques → Optimizer refines → Reviewer archives lesson |


  

## License & Attribution
This project is for educational purposes only as part of the MSAAI program at the University of San Diego.
