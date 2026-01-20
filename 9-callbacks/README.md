# Callbacks in ADK

This example demonstrates how to use callbacks in the Agent Development Kit (ADK) to intercept, observe, and modify agent behavior at different stages of execution. Callbacks provide powerful hooks into the agent lifecycle, enabling monitoring, logging, filtering, transformation, and enforcement of custom logic.

---

## What Are Callbacks in ADK?

Callbacks are functions that run at specific points during an agent’s execution flow. They allow you to inject custom logic without modifying the core agent behavior.

With callbacks, you can:

1. **Monitor and Log**  
   Track agent activity, timing, and usage metrics.

2. **Filter Content**  
   Block or intercept inappropriate requests or responses.

3. **Transform Data**  
   Modify inputs before execution or outputs before delivery.

4. **Implement Security Policies**  
   Enforce compliance, moderation, or governance rules.

5. **Add Custom Logic**  
   Apply business-specific rules at precise execution stages.

ADK provides multiple callback types that attach to agents, models, and tools.

---

## Callback Parameters and Context

Each callback type receives specific context objects that expose execution state and metadata.

---

### CallbackContext

`CallbackContext` is provided to all callback types and includes:

- **agent_name**: Name of the executing agent  
- **invocation_id**: Unique identifier for the invocation  
- **state**: Session state (read/write access)  
- **app_name**: Application name  
- **user_id**: Current user ID  
- **session_id**: Current session ID  

Example:

```python
def my_callback(callback_context: CallbackContext, ...):
    user_name = callback_context.state.get("user_name", "Unknown")
    print(
        f"Agent {callback_context.agent_name} executing "
        f"(Invocation ID: {callback_context.invocation_id})"
    )


    Types of Callbacks Demonstrated

This project includes three callback patterns.

1. Agent Callbacks (before_after_agent/)

Before Agent Callback: Runs before agent execution

After Agent Callback: Runs after agent execution

Used for logging, metrics, and request-level state tracking.

2. Model Callbacks (before_after_model/)

Before Model Callback: Intercepts requests before they reach the LLM

After Model Callback: Modifies model responses

Used for moderation, filtering, and response transformation.

3. Tool Callbacks (before_after_tool/)

Before Tool Callback: Modifies or blocks tool execution

After Tool Callback: Enhances tool responses

Used for validation, normalization, and enrichment.

Project Structure
8-callbacks/
│
├── before_after_agent/           # Agent callback example
│   ├── __init__.py
│   ├── agent.py                  # Agent with agent callbacks
│   └── .env
│
├── before_after_model/           # Model callback example
│   ├── __init__.py
│   ├── agent.py                  # Agent with model callbacks
│   └── .env
│
├── before_after_tool/            # Tool callback example
│   ├── __init__.py
│   ├── agent.py                  # Agent with tool callbacks
│   └── .env
│
└── README.md

Setup

Activate the virtual environment from the root directory:

# macOS/Linux
source ../.venv/bin/activate

# Windows CMD
..\.venv\Scripts\activate.bat

# Windows PowerShell
..\.venv\Scripts\Activate.ps1


Create .env files in each agent directory:

GOOGLE_API_KEY=your_api_key_here

Run
cd 8-callbacks
adk web


Select the agent to test from the dropdown:

before_after_agent

before_after_model

before_after_tool

Additional Resources

ADK Callbacks Documentation
https://google.github.io/adk-docs/callbacks/

Types of Callbacks
https://google.github.io/adk-docs/callbacks/types-of-callbacks/

Design Patterns and Best Practices
https://google.github.io/adk-docs/callbacks/design-patterns-and-best-practices/