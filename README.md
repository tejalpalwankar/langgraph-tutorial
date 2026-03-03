# 🚀 LangGraph Agentic AI Learning Project

This repository contains hands-on implementations from an **Agentic AI with LangGraph** tutorial.  
It explores how to build multi-step AI agents using **LangGraph**, **LangChain**, and **Google Gemini**.

---

## 📚 What This Project Covers

This project demonstrates:

- ✅ Simple stateful graphs  
- ✅ Conditional routing with graph edges  
- ✅ Tool calling with LLMs  
- ✅ Multi-step agent loops  
- ✅ Conversation memory with thread IDs  
- ✅ LangSmith tracing  
- ✅ Human-in-the-loop (HITL) workflows  

---

## 🧠 Core Concept: Why LangGraph?

Traditional LLM chains are linear.

LangGraph allows:

- Stateful orchestration  
- Conditional edges  
- Tool routing  
- Memory checkpoints  
- Human approval gates  

It enables building **real agent systems**, not just prompt-response bots.

---

## 🏗 Project Structure


langgraph-learning/
│
├── 1_simple_graph.ipynb
├── 2_graph_with_conditions.ipynb
├── 3_chatbot.ipynb
├── 4_tool_call.ipynb
├── 5_tool_call_agent.ipynb
├── 6_memory.ipynb
├── 7_langsmith_tracing.ipynb
├── 8_HITL.py
│
├── .env
├── pyproject.toml
├── uv.lock
└── README.md


---

## ⚙️ Setup Instructions

### 1️⃣ Clone Repository

```bash
git clone <your-repo-url>
cd langgraph-learning
```

2️⃣ Create Virtual Environment (Using UV)
uv init
uv add langgraph langchain langchain-google-genai python-dotenv notebook
3️⃣ Configure Python Interpreter

On Mac/Linux:

.venv/bin/python

On Windows:

.venv\Scripts\python.exe
4️⃣ Create .env File

Create a .env file in the project root:

GOOGLE_API_KEY=your_api_key_here

Get your API key from:
https://aistudio.google.com/app/apikey

🧩 Key Implementations
🟢 Simple Graph

Define State using TypedDict

Add nodes

Add edges

Compile and invoke

🔀 Conditional Routing

Uses:

builder.add_conditional_edges(...)

Routes dynamically based on state.

🛠 Tool Calling Agent

Implements:

@tool

ToolNode

tools_condition

Agent loop:

chatbot → tools → chatbot

The LLM decides when to call tools.

🧠 Memory with Thread IDs

Enables persistent conversations:

config = {"configurable": {"thread_id": "1"}}
graph.invoke(input_state, config=config)

Supports:

Conversation persistence

Multiple threads

Checkpoint recovery

🔍 LangSmith Tracing

Provides:

Token tracking

Latency monitoring

Tool call visibility

Cost tracking

👤 Human-in-the-Loop (HITL)

Implements:

interrupt()
Command(resume="yes")

Use case example:

Approve stock trade before execution.

⚠️ Gemini Free Tier Limits

Gemini Free Tier includes:

20 requests per day (RPD)

5 requests per minute (RPM)

Agent loops may consume multiple model calls per query.

If you see:

429 RESOURCE_EXHAUSTED

You have exceeded your daily quota.

Solutions:

Wait for daily reset

Enable billing

Reduce tool loops

Switch to a lighter model

🧪 Example Usage
state = graph.invoke({
    "messages": [("user", "What is the price of AAPL stock?")]
})

print(state["messages"][-1].content)
🛠 Common Errors & Fixes
❌ NameError: TypedDict not defined
from typing_extensions import TypedDict
❌ Structured/Gibberish Output from Gemini

Extract plain text:

def as_text(msg):
    if isinstance(msg.content, str):
        return msg.content
    if isinstance(msg.content, list):
        return "".join(
            block.get("text", "")
            for block in msg.content
            if isinstance(block, dict)
        )
❌ RESOURCE_EXHAUSTED

Free-tier daily request limit reached.

📈 Learning Outcomes

After completing this project, you will understand:

Graph-based AI orchestration

Stateful agent systems

Tool-augmented reasoning

Memory management

Human approval workflows

Production-level observability

🛠 Technologies Used

LangGraph

LangChain

Google Gemini API

LangSmith

UV (Python package manager)

PyCharm

🎯 Future Improvements

Add retry policies

Add error recovery nodes

Add streaming responses

Add evaluation harness

Deploy via LangServe

🙌 Credits

Based on:
Agentic AI Tutorial for Beginners | LangGraph Tutorial
