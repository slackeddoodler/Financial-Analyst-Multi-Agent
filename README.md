# **Financial Analyst Multi-Agent MCP System**

A multi-agent financial analysis system powered by **CrewAI**, served through **Groq**, and exposed as an **MCP server** for use with **Cursor** or **GitHub Copilot**.

This project lets you: \
✔ Parse natural-language financial queries \
✔ Auto-generate Python code for stock visualizations \
✔ Execute the code securely \
✔ Save/Run code directly via custom MCP tools

---

## 🚀 **Tech Stack**

* **CrewAI** — Multi-agent orchestration
* **Groq** — Serves the LLM backend
* **Cursor or GitHub Copilot (VSCode)** — MCP host
* **MCP Tools** — For code saving and plot execution

---

## 🧠 **Agents Overview**

### **1. Query Parser Agent**

* Takes a natural-language user query.
* Uses **Pydantic models** to parse and convert it into structured data.
* Ensures clean and valid inputs for the rest of the pipeline.

### **2. Code Writer Agent**

* Generates Python code to visualize stock data.
* Uses:

  * `pandas`
  * `matplotlib`
  * `yfinance`
* Entire visualization logic is auto-created based on the parsed query.

### **3. Code Executor Agent**

* Reviews the generated code.
* Executes it inside a **CrewAI Code Interpreter sandbox**.
* Produces plots and results safely.

---

## ⚙️ **LLM Setup (Groq)**

1. Create a Groq account
2. Get your Groq API key
3. Set it in your `.env`:

```bash
GROQ_API_KEY="your_key"
```

4. The agents will now use Groq to handle all LLM calls.

---

## 🧩 **Crew Setup & Kickoff**

After defining your 3 agents and tasks:

```python

result = crew.kickoff(
    inputs={"query": "Plot YTD stock gain of Google"}
)
```

This triggers:

1. Query → structured output
2. Code generation
3. Code validation + execution
4. Plot returned to user

---

# 🛠️ **MCP Server Setup**

Your system includes 3 MCP tools:

### **Provided Tools**

| Tool                     | Description                                       |
| ------------------------ | ------------------------------------------------- |
| `financial-analyst`      | Primary agent interface                           |
| `save_code`              | Saves generated Python files to project directory |
| `run_code_and_show_plot` | Executes the saved code & outputs plot            |


### Install Dependencies

```
pip install 'crewai[tools]' yfinance matplotlib fastmcp
```

### Clone/Download the Repository

```
git clone https://github.com/slackeddoodler/Financial-Analyst-Multi-Agent.git
cd Financial-Analyst-Multi-Agent
```

### **Run the MCP server**

```
python server.py
```

---

# 💻 **Integrating MCP With Editors**

You can use either **Cursor** or **GitHub Copilot in VSCode**.

---

# 🎯 **1. Use With Cursor**

### **Steps**:

1. Open Cursor
2. Go to:
   **File → Preferences → Cursor Settings → MCP**
3. Add new global MCP server using:

```jsonc
{
  "mcpServers": {
    "financial-analyst": {
      "command": "python exec directory",
      "args": ["server.py"],
      "cwd": "project-directory"
    }
  }
}
```

---

# 🎯 **2. Use With GitHub Copilot (VSCode)**


### **Steps**:

1. Open **VSCode**
2. Go to:
   **Settings → Extensions → GitHub Copilot → MCP Servers**
3. Click **Add MCP Server**
4. Insert:

```jsonc
{
  "financial-analyst": {
    "command": "python exec directory",
    "args": ["server.py"],
    "cwd": "project-directory"
  }
}
```

5. Restart VSCode
6. Copilot will now show MCP tool entries inside its UI.

---

## 📁 **Project Structure (Suggested)**

```
├── server.py        # MCP server
├── crew.py          # Crew orchestration
└── README.md
```

---

# ✅ **You're Ready to Run**

Once the MCP server is live, Cursor or Copilot can now do:

```
Ask the financial analyst to plot Apple's last 6 month trend.
```

And your multi-agent system will:

1. Parse
2. Generate code
3. Execute
4. Return the final plot

## Example
<img width="1466" height="742" alt="fin_analysis_example" src="https://github.com/user-attachments/assets/bedf1a05-e709-4fd2-932f-8e8b2709ca7f" />

