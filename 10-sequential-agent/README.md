# Sequential Agents in ADK

This example demonstrates how to implement a Sequential Agent in the Agent Development Kit (ADK). The main agent, `lead_qualification_agent`, is a Sequential Agent that executes sub-agents in a predefined order, where each agent’s output feeds directly into the next step of the workflow.

---

## What Are Sequential Agents?

Sequential Agents are workflow-oriented agents in ADK designed for deterministic, step-by-step execution.

They are ideal when you need:

1. **Fixed Execution Order**  
   Sub-agents always run in the exact sequence they are defined.

2. **Data Passing Between Steps**  
   Each sub-agent can read results produced by previous agents through shared state.

3. **Processing Pipelines**  
   Perfect for workflows where later steps depend on earlier outputs.

Use Sequential Agents when execution order matters and the workflow must be predictable.

---

## Lead Qualification Pipeline Example

This example implements a sales lead qualification pipeline using a Sequential Agent. The `lead_qualification_agent` orchestrates three specialized sub-agents.

---

### 1. Lead Validator Agent

Validates whether the lead contains sufficient information for qualification.

- Checks for required details such as contact information and stated interest
- Outputs a simple validation result: **valid** or **invalid**, with reasoning

---

### 2. Lead Scorer Agent

Scores valid leads on a scale of 1–10.

- Evaluates urgency, authority, budget, and timeline
- Outputs a numeric score with a brief explanation

---

### 3. Action Recommender Agent

Suggests next steps based on validation and scoring results.

- **Invalid leads**: Recommends missing information to collect
- **Low score (1–3)**: Suggests nurturing actions
- **Medium score (4–7)**: Suggests qualification actions
- **High score (8–10)**: Suggests direct sales actions

---

## How It Works

The `lead_qualification_agent` coordinates the pipeline as follows:

1. **Validator runs first**  
   Determines whether the lead is complete enough to proceed.

2. **Scorer runs second**  
   Accesses validation results via shared state and assigns a score.

3. **Recommender runs last**  
   Uses both validation and score to determine the next best action.

Each sub-agent stores its result in session state using `output_key`:

- `validation_status`
- `lead_score`
- `action_recommendation`

This makes all intermediate results available throughout the workflow.

---

## Project Structure

9-sequential-agent/
│
├── lead_qualification_agent/ # Main Sequential Agent package
│ ├── init.py # Package initialization
│ ├── agent.py # Sequential Agent definition (root_agent)
│ │
│ └── subagents/ # Sub-agents
│ ├── init.py
│ │
│ ├── validator/ # Lead validation agent
│ │ ├── init.py
│ │ └── agent.py
│ │
│ ├── scorer/ # Lead scoring agent
│ │ ├── init.py
│ │ └── agent.py
│ │
│ └── recommender/ # Action recommendation agent
│ ├── init.py
│ └── agent.py
│
├── .env.example # Environment variables example
└── README.md # Documentation

yaml
Copy code

---

## Getting Started

### Setup

1. Activate the virtual environment from the root directory:

```bash
# macOS/Linux
source ../.venv/bin/activate

# Windows CMD
..\.venv\Scripts\activate.bat

# Windows PowerShell
..\.venv\Scripts\Activate.ps1
Copy .env.example to .env and add your Google API key:

env
Copy code
GOOGLE_API_KEY=your_api_key_here
Running the Example
bash
Copy code
cd 9-sequential-agent
adk web

Additional Resources

ADK Sequential Agents Documentation
https://google.github.io/adk-docs/agents/workflow-agents/sequential-agents/

Full Pipeline Example
https://google.github.io/adk-docs/agents/workflow-agents/sequential-agents/#full-example-code-development-pipeline
