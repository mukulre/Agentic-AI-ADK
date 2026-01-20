# Sessions and State Management in ADK

This example demonstrates how to create and manage stateful sessions in the Agent Development Kit (ADK), allowing agents to maintain context and remember user information across multiple interactions.

---

## What Are Sessions in ADK?

Sessions in ADK enable agents to persist information beyond a single request.

They allow you to:

1. **Maintain State**  
   Store and retrieve user data, preferences, and other contextual information between interactions.

2. **Track Conversation History**  
   Automatically record and access prior messages in a conversation.

3. **Personalize Responses**  
   Use stored session data to generate more relevant and personalized responses.

Unlike stateless agents, session-based agents can build continuity over time by remembering important user details.

---

## Example Overview

This directory contains a basic stateful session example demonstrating:

- Creating a session with predefined user preferences
- Using template variables to reference session state in agent instructions
- Running an agent with a session to preserve context

The example uses a simple question-answering agent that responds based on user information stored in session state.

---


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

GOOGLE_API_KEY=your_api_key_here

Run the example script to see session state in action:

python basic_stateful_session.py


This process will:

Create a new session containing user information

Initialize the agent with access to that session

Process a user query that references stored preferences

Output the agent’s response using session data

Key Components
Session Service

The example uses an in-memory session service to store session data:

session_service = InMemorySessionService()

Initial State

Sessions are initialized with predefined user information:

initial_state = {
    "user_name": "Brandon Hancock",
    "user_preferences": """
        I like to play Pickleball, Disc Golf, and Tennis.
        My favorite food is Mexican.
        My favorite TV show is Game of Thrones.
        Loves it when people like and subscribe to his YouTube channel.
    """,
}

Creating a Session

A session is created using a unique application name, user ID, and session ID:

stateful_session = session_service.create_session(
    app_name=APP_NAME,
    user_id=USER_ID,
    session_id=SESSION_ID,
    state=initial_state,
)

Accessing State in Agent Instructions

The agent references session state using template variables in its instruction prompt:

instruction="""
You are a helpful assistant that answers questions about the user's preferences.

Here is some information about the user:
Name:
{user_name}
Preferences:
{user_preferences}
"""

Running with Sessions

The session service is passed to the Runner to ensure state is maintained during execution:

runner = Runner(
    agent=question_answering_agent,
    app_name=APP_NAME,
    session_service=session_service,
)

Additional Resources

Google ADK Sessions Documentation
https://google.github.io/adk-docs/sessions/session/

State Management in ADK
https://google.github.io/adk-docs/sessions/state/