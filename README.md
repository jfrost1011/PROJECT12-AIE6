# 📑 OpenAI Agents SDK – "Research Bot" Walk-Through  
*Course: AI Engineering Bootcamp – Project 14*  

## ⚡️ Quick Glance
| Stage | What We Built | Key Take-aways |
|-------|---------------|----------------|
| **Task 1 – Planner Agent** | GPT-4-powered agent that turns a user query into 5-20 web-search terms. | Showcased **structured outputs** with `WebSearchPlan`, making downstream steps trivial. |
| **Task 2 – Search Agent** | Agent equipped with the hosted **`WebSearchTool`** (Responses API). For every term it returns a <300-word summary. | Demonstrated tool-calling (`tool_choice="required"`). |
| **Task 3 – Writer Agent** | "Senior-researcher" agent that (1) outlines, (2) writes a multi-page markdown report, (3) suggests 5 follow-ups. We specialized the prompt for **FinTech in residential remodels**. | Used a **reasoning model** (`o3-mini`) and custom `ReportData` schema. |
| **Task 4 – Utilities** | `Printer` (Rich live console) + `ResearchManager` that orchestrates the full loop: plan → search → write, with progress spinners & trace links. | Illustrated concurrency (`asyncio` + max 5 searches at once) and built-in OpenAI **trace IDs** for observability. |
| **Task 5 – Run** | Async CLI asks *"What would you like to research?"* and streams the finished report + follow-up Qs. | End-to-end demo; prompt used: **"Lessons U.S. remodel-focused fintechs can learn from Japan's long-term housing renovation loan."** |

---

## ❓ Notebook Q&A  

| # | Question | Answer (concise) |
|---|----------|------------------|
| 1 | *Why use a structured response template?* | It lets every later step parse data deterministically (no messy regex) – like giving LEGO blocks instead of a glued-together model. |
| 2 | *What other tools does the Responses API support?* | `web_search`, `file_search`, `code_interpreter`, and any **custom** tool you register (e.g., DB queries, cloud actions). |
| 3 | *Why pick a reasoning model for writing?* | Long-form synthesis needs chain-of-thought, source weaving, and consistency – skills smaller chat-only models often lack. |

---

## 🏗️ Activities  

### Activity #1 – Prompt Personalisation  
We rewrote the Writer prompt to target **FinTech solutions for U.S. residential remodels**, ensuring domain-specific tone and examples.

### Activity #2 – Flowchart  
Created an architecture diagram showing message flow:<br>
**User → Planner → Search (×N) → Writer → Console Printer** (with trace hooks).  
*(PNG located in `/12_OpenAI_Agents_SDK/image_agent_flow_activity2.png`)*  

---

## 🚀 How to Re-Run

```bash
git clone https://github.com/<your-org>/openai-agents-remodel-fintech.git
cd openai-agents-remodel-fintech
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
export OPENAI_API_KEY=<your-key>
python notebook_runner.py   # or launch Jupyter and run cells
```
