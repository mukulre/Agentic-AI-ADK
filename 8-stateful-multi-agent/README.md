# Stateful Multi-Agent Systems in ADK

This example demonstrates how to build a stateful multi-agent system in the Agent Development Kit (ADK), combining persistent state management with specialized agent delegation. The result is an intelligent agent system that remembers user information across interactions while leveraging domain-specific expertise.

---

## What Is a Stateful Multi-Agent System?

A stateful multi-agent system merges two powerful ADK patterns:

1. **State Management**  
   Persisting user information and conversation context across interactions.

2. **Multi-Agent Architecture**  
   Delegating tasks to specialized agents based on domain expertise.

Together, these patterns enable systems that:

- Remember user information and interaction history
- Route queries to the most appropriate specialist
- Personalize responses using past interactions
- Maintain context across multiple agent handoffs

This example implements a customer service system for an online course platform, where multiple specialized agents collaborate while sharing a common session state.

---

## Project Structure

7-stateful-multi-agent/
│
├── customer_service_agent/ # Main agent package
│ ├── init.py # Required for ADK discovery
│ ├── agent.py # Root agent definition
│ └── sub_agents/ # Specialized agents
│ ├── course_support_agent/ # Handles course content questions
│ ├── order_agent/ # Manages order history and refunds
│ ├── policy_agent/ # Answers policy questions
│ └── sales_agent/ # Handles course purchases
│
├── main.py # Application entry point with session setup
├── utils.py # Helper functions for state management
├── .env # Environment variables
└── README.md # Documentation


How It Works

Initial Session Creation

A new session is created with default user data

Interaction history starts empty

Conversation Tracking

Each user message is appended to interaction_history

Agents can reference prior interactions for context

Query Routing

The root agent analyzes the user query

The query is delegated to the correct specialized agent

Full session state is passed during delegation

State Updates

Sales actions update purchased_courses

Updates persist across future interactions

Personalized Responses

Agents tailor responses based on purchase history

Different logic paths are taken depending on user state

Getting Started
Setup

Activate the virtual environment from the root directory:

# macOS/Linux
source ../.venv/bin/activate

# Windows CMD
..\.venv\Scripts\activate.bat

# Windows PowerShell
..\.venv\Scripts\Activate.ps1


Ensure your Google API key is set in the .env file:

GOOGLE_API_KEY=your_api_key_here

Running the Example

Run the application:

python main.py

Additional Resources

ADK Sessions Documentation
https://google.github.io/adk-docs/sessions/session/

ADK Multi-Agent Systems Documentation
https://google.github.io/adk-docs/agents/multi-agent-systems/

State Management in ADK
https://google.github.io/adk-docs/sessions/state/