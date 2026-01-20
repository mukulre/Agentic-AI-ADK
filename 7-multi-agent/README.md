# Multi-Agent Systems in ADK

This example demonstrates how to build a multi-agent system in the Agent Development Kit (ADK), where multiple specialized agents collaborate to handle complex tasks, each focusing on a specific area of expertise.

---

## What Is a Multi-Agent System?

A Multi-Agent System is an advanced ADK pattern that enables multiple agents to work together. Each agent is responsible for a specific domain or capability, and collaboration happens through delegation or controlled interaction.

This approach allows you to solve problems that are too complex or too broad for a single agent by distributing responsibilities across specialists.

---

## Project Structure Requirements

For multi-agent systems to work correctly in ADK, your project must follow a strict directory structure:

parent_folder/
├── root_agent_folder/ # Main agent package (e.g., "manager")
│ ├── init.py # Must import agent.py
│ ├── agent.py # Must define root_agent
│ ├── .env # Environment variables
│ └── sub_agents/ # Directory for all sub-agents
│ ├── init.py # Empty or imports sub-agents
│ ├── agent_1_folder/ # Sub-agent package
│ │ ├── init.py # Must import agent.py
│ │ └── agent.py # Must define an agent variable
│ ├── agent_2_folder/
│ │ ├── init.py
│ │ └── agent.py
│ └── ...

markdown
Copy code

---

### Essential Structure Components

1. **Root Agent Package**
   - Follows the standard agent structure
   - `agent.py` must define a `root_agent` variable

2. **Sub-Agents Directory**
   - Typically named `sub_agents`
   - Each sub-agent lives in its own folder with a standard agent structure

3. **Importing Sub-Agents**
   - Sub-agents must be imported by the root agent:
   ```python
   from .sub_agents.funny_nerd.agent import funny_nerd
   from .sub_agents.stock_analyst.agent import stock_analyst
Command Location

Always run adk web from the parent directory (for example, 6-multi-agent)

Do not run the command from inside an agent folder

This structure allows ADK to correctly discover and load all agents in the hierarchy.

Getting Started

This example uses the virtual environment created in the project root.

Setup

Activate the virtual environment:

# macOS/Linux
source ../.venv/bin/activate

# Windows CMD
..\.venv\Scripts\activate.bat

# Windows PowerShell
..\.venv\Scripts\Activate.ps1


Configure your API key:

Rename .env.example to .env inside the manager folder

Add your Google API key:

GOOGLE_API_KEY=your_api_key_here

Running the Example

Navigate to the 6-multi-agent directory.

Start the interactive web UI:

adk web


Open the URL shown in the terminal (usually http://localhost:8000
).

Select the manager agent from the dropdown menu.

Start interacting with the system using the input box.

To stop the server, press Ctrl+C.

Troubleshooting

If the multi-agent system does not appear correctly:

Ensure adk web is run from the parent directory (6-multi-agent)

Verify each agent’s __init__.py imports its agent.py

Confirm the root agent imports all sub-agents