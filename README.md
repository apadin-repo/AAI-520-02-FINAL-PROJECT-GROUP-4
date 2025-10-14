# AAI-520-02-FINAL-PROJECT-GROUP-4
# 🧠 Multi-Agent Financial Analysis System – AAI-520 Final Project

### University of San Diego — Applied Artificial Intelligence (AAI-520)
**Team Members:**  
- **Alexander J. Padin**  
- **Thomas Geraci**
- **Ali Mohtat**
  
---

## 📘 Project Overview
This project implements an **agentic AI financial research system** using **CrewAI**, **OpenAI GPT-4o**, and **Anthropic Claude 3.5 Sonnet**.  
It demonstrates how autonomous AI agents can plan, research, critique, and iteratively improve investment analyses — mirroring real-world financial research workflows.

Each agent performs a distinct function in a self-improving multi-agent loop:
1. **Planner** – designs a structured 5–7 step research plan for a given stock.  
2. **Researcher** – gathers and synthesizes data using Yahoo Finance tools.  
3. **Reviewer** – evaluates the draft, assigns a grade, and provides feedback.  
4. **Optimizer** – refines the report based on Reviewer feedback.  
5. **Archivist (Memory System)** – stores “lessons learned” for future runs.

These roles demonstrate all required **workflow patterns**:  
- **Prompt Chaining:** sequential pipeline from planning to refinement.  
- **Routing:** specialized agents handle distinct subtasks.  
- **Evaluator–Optimizer Loop:** Reviewer feedback drives the Optimizer’s improvements.

---

## 🧩 Key Features
- ✅ **Agentic AI Framework** – built with [CrewAI](https://github.com/joaomdmoura/crewAI)  
- 🧠 **Multi-Model Reasoning** – integrates *GPT-4o* (OpenAI) and *Claude 3.5 Sonnet* (Anthropic)  
- 💾 **Persistent Knowledge Memory** – JSONL-based memory across runs  
- 📊 **Financial Data Retrieval** – via [yfinance](https://pypi.org/project/yfinance/) for OHLCV, fundamentals, dividends, and events  
- 🔁 **Autonomous Feedback Cycle** – Reviewer → Optimizer → Memory  
- 🧰 **Extensible Tools** – modular `@tool()` decorators for future APIs  

---

## ⚙️ Installation and Setup

### Step 1 – Clone Repository
```bash
git clone https://github.com/<your-team>/<your-repo-name>.git
cd <your-repo-name>
```

### Step 2 – Create Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate     # macOS/Linux  
venv\Scripts\activate        # Windows
```

### Step 3 – Install Dependencies
```bash
pip install -r requirements.txt
```
If no `requirements.txt` exists:
```bash
pip install crewai openai anthropic yfinance pandas python-dotenv ipython
```

### Step 4 – Configure API Keys
Create a `.env` file in the project root:
```
OPENAI_API_KEY=your_openai_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here
```
> ⚠️ Do **not** commit `.env` to GitHub.

### Step 5 – Run the Notebook
```bash
jupyter notebook
```
Open and run `AAI520_Final_MultiAgentSystem.ipynb` or, if scripted:
```bash
python main.py
```

---

## 📈 Example Run
```python
result = crew.kickoff(inputs={"ticker": "AAPL"})
```
Example output:
```json
{
 "ticker": "AAPL",
 "recommendation": "HOLD",
 "signals": {
  "last_price": 256.48,
  "market_cap": 3.8e12,
  "year_high": 260.10,
  "year_low": 169.21
 },
 "lessons_used": [
  "Always include key financial ratios and peer context.",
  "Always provide comprehensive analysis even under data constraints."
 ]
}
```

---

## 📚 Repository Structure
```
├── AAI520_Final_MultiAgentSystem.ipynb
├── outputs/
│   ├── reviewer_output.json
│   ├── archivist_output.json
├── memory/
│   ├── kb_AAPL.jsonl
├── .env
├── requirements.txt
├── README.md
```

---

## 🧠 Agent Summary
| Agent | Purpose | Tools | LLM |
|-|-|-|-|
| **Planner** | Designs research plan | None | GPT-4o |
| **Researcher** | Collects & synthesizes data | `yf_prices`, `yf_fundamentals`, `yf_dividends`, `yf_calendar` | GPT-4o |
| **Reviewer** | Grades & critiques | Same tools + `save_kb_lesson_tool` | Claude 3.5 |
| **Optimizer** | Refines output | Same tools | GPT-4o |
| **Archivist** | Saves lessons | `load_kb_lessons_tool`, `save_kb_lesson_tool` | Claude 3.5 |

---

## 🧮 Workflow Patterns Demonstrated
| Pattern | Implementation |
|-|-|
| **Prompt Chaining** | Sequential flow: Planner → Researcher → Reviewer → Optimizer → Archivist |
| **Routing** | Each agent uses specialized toolsets and distinct LLMs |
| **Evaluator–Optimizer Loop** | Reviewer critiques → Optimizer refines → Reviewer archives lesson |

---

## 📊 Visualization Example
```python
import yfinance as yf
import matplotlib.pyplot as plt
data = yf.download("AAPL", period="90d", interval="1d")
data['Close'].plot(title="AAPL Closing Prices (90 Days)")
plt.show()
```


## License & Attribution
Educational project for **University of San Diego – AAI-520 (Natural Language Processing and GenAI)**.  
Please cite **CrewAI**, **OpenAI GPT-4o**, and **Anthropic Claude 3.5 Sonnet** if reusing this work.  

© 2025 USD AAI-520 Team — Ali Mohtat, Alexander J. Padin, Thomas Geraci  
