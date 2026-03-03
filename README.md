Here is your content formatted into a professional, clean `README.md` file. I’ve optimized the tables and structure to ensure it renders perfectly on GitHub.

```markdown
# 🚀 LangGraph Agentic AI Learning Project

This repository contains hands-on implementations from the **Agentic AI with LangGraph** tutorial. It explores how to build reliable multi-step AI agents using **LangGraph**, **LangChain**, and **Google Gemini**.

## 📚 What This Project Covers

This repo demonstrates the core building blocks of modern agentic workflows:

* ✅ **Simple stateful graphs**: The foundation of LangGraph.
* ✅ **Conditional routing**: Graph-based decision making.
* ✅ **Tool calling**: Enabling LLMs to interact with external functions.
* ✅ **Multi-step agent loops**: Iterative reasoning processes.
* ✅ **Memory & Persistence**: Thread-based state management.
* ✅ **LangSmith tracing**: Observability and debugging.
* ✅ **Human-in-the-loop (HITL)**: Manual approval gates for sensitive tasks.

---

## 🧠 Core Concepts

### Workflow vs. Agent

| Feature | Workflow | Agent |
| :--- | :--- | :--- |
| **Structure** | Linear or predefined chains | Graphs with cycles/loops |
| **Logic** | Fixed, hard-coded paths | LLM decides the next step |
| **Nature** | Reactive | Goal-oriented |

**LangGraph enables:**
* Stateful orchestration
* Conditional edges
* Tool routing
* Memory checkpoints
* Human approval gates



---

## 🏗 Project Structure

```text
langgraph-learning/
│
├── 1_simple_graph.ipynb         # Basic nodes and edges
├── 2_graph_with_conditions.ipynb # Routing logic
├── 3_chatbot.ipynb              # Conversational interface
├── 4_tool_call.ipynb            # External function integration
├── 5_tool_call_agent.ipynb      # Autonomous agent loop
├── 6_memory.ipynb               # Thread-based persistence
├── 7_langsmith_tracing.ipynb    # Observability setup
├── 8_HITL.py                    # Human-in-the-loop implementation
│
├── .env                         # API Keys (not tracked)
├── pyproject.toml               # Project dependencies
├── uv.lock                      # Lockfile
└── README.md

```

---

## ⚙️ Setup Instructions

### 1️⃣ Clone Repository

```bash
git clone <your-repo-url>
cd langgraph-learning

```

### 2️⃣ Create Virtual Environment (Using UV)

```bash
uv init
uv add langgraph langchain langchain-google-genai python-dotenv notebook

```

### 3️⃣ Set Python Interpreter

* **Mac/Linux:** `.venv/bin/python`
* **Windows:** `.venv/Scripts/python.exe`

### 4️⃣ Create .env File

Inside the project root, add your [Google AI Studio API Key](https://aistudio.google.com/app/apikey):

```env
GOOGLE_API_KEY=your_api_key_here

```

---

## 🧩 Key Implementations

### 🟢 Simple Graph

Uses `TypedDict` for state definition, defining nodes and edges, then compiling the graph for invocation.

### 🔀 Conditional Routing

Uses `builder.add_conditional_edges(...)` to route the workflow dynamically based on the current state data.

### 🛠 Tool Calling Agent

Implements the standard agent loop: `chatbot` → `tools` → `chatbot`.

* Uses `@tool` decorator.
* Utilizes `ToolNode` and `tools_condition`.

### 🧠 Memory with Thread IDs

Enables conversation persistence and parallel threads using `MemorySaver`.

```python
from langgraph.checkpoint.memory import MemorySaver
config = {"configurable": {"thread_id": "1"}}
graph.invoke(input_state, config=config)

```

### 👤 Human-in-the-Loop (HITL)

Implements `interrupt()` and `Command(resume="yes")`. This is ideal for use cases like approving a stock trade before execution.

---

## ⚠️ Free Tier Gemini Quota Limits

If you encounter a `429 RESOURCE_EXHAUSTED` error, you have exceeded the daily quota:

* **Limits:** 20 Requests Per Day (RPD) / 5 Requests Per Minute (RPM).
* **Fixes:** Wait for daily reset, use `gemini-1.5-flash` for lower overhead, or enable billing.

---

## 🛠 Common Errors & Fixes

* **`NameError: TypedDict not defined`**: Ensure you import from `typing_extensions` or `typing`.
* **`RESOURCE_EXHAUSTED`**: You've hit the Gemini free-tier daily cap.
* **Structured Content Errors**: If Gemini returns a list instead of a string, use a helper function to extract `block.get("text")`.

---

## 📈 Learning Outcomes

* Mastering graph-based agent orchestration.
* Implementing stateful AI systems with memory.
* Integrating tool-augmented reasoning.
* Setting up production-grade observability with LangSmith.

---

## 📌 Technologies Used

* **LangGraph** (Orchestration)
* **LangChain** (Framework)
* **Google Gemini** (LLM)
* **LangSmith** (Tracing)
* **UV** (Package Management)

---

## 🙌 Credits

Based on the tutorial: *Agentic AI Tutorial for Beginners | LangGraph Tutorial*

