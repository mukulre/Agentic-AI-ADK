# Persistent Storage in ADK

This example demonstrates how to implement persistent storage for ADK agents, allowing them to remember information and maintain conversation history across multiple sessions, application restarts, and server deployments.

---

## What Is Persistent Storage in ADK?

Earlier examples use `InMemorySessionService`, which stores session data only in memory. This data is lost when the application stops.

For real-world applications, agents often need long-term memory. ADK provides `DatabaseSessionService`, which stores session data in a SQL database.

This enables:

1. **Long-Term Memory**  
   Session data persists across application restarts.

2. **Consistent User Experiences**  
   Users can resume conversations where they left off.

3. **Multi-User Support**  
   Data remains isolated and secure per user.

4. **Scalability**  
   Compatible with production-grade databases.

This example implements a reminder agent that remembers your name and todos across conversations using an SQLite database.

---

## Project Structure

5-persistent-storage/
│
├── memory_agent/ # Agent package
│ ├── init.py # Required for ADK to discover the agent
│ └── agent.py # Agent definition with reminder tools
│
├── main.py # Application entry point with database session setup
├── utils.py # Utility functions for terminal UI and agent interaction
├── .env # Environment variables
├── my_agent_data.db # SQLite database (created on first run)
└── README.md # Documentation

yaml
Copy code

---

## Key Components

### 1. DatabaseSessionService

Persistent storage is enabled using `DatabaseSessionService`, initialized with a database URL:

```python
from google.adk.sessions import DatabaseSessionService

db_url = "sqlite:///./my_agent_data.db"
session_service = DatabaseSessionService(db_url=db_url)
This service allows ADK to:

Store session data in a SQLite database

Retrieve previous sessions for a user

Automatically manage database schemas

2. Session Management
The example demonstrates how to reuse existing sessions or create new ones:

python
Copy code
existing_sessions = session_service.list_sessions(
    app_name=APP_NAME,
    user_id=USER_ID,
)

if existing_sessions and len(existing_sessions.sessions) > 0:
    SESSION_ID = existing_sessions.sessions[0].id
    print(f"Continuing existing session: {SESSION_ID}")
else:
    session_service.create_session(
        app_name=APP_NAME,
        user_id=USER_ID,
        session_id=SESSION_ID,
        state=initialize_state(),
    )
This ensures users continue from their most recent session when available.

3. State Management with Tools
The agent uses tools to modify persistent state stored in the database:

python
Copy code
def add_reminder(reminder: str, tool_context: ToolContext) -> dict:
    reminders = tool_context.state.get("reminders", [])
    reminders.append(reminder)
    tool_context.state["reminders"] = reminders

    return {
        "action": "add_reminder",
        "reminder": reminder,
        "message": f"Added reminder: {reminder}",
    }
Any update to tool_context.state is automatically persisted to the database.

Getting Started
Prerequisites
Python 3.9+

Google API key for Gemini models

SQLite (included with Python)

Setup
Activate the virtual environment from the root directory:

bash
Copy code
# macOS/Linux
source ../.venv/bin/activate

# Windows CMD
..\.venv\Scripts\activate.bat

# Windows PowerShell
..\.venv\Scripts\Activate.ps1
Ensure your Google API key is set in the .env file:

env
Copy code
GOOGLE_API_KEY=your_api_key_here
Running the Example
Run the application:

bash
Copy code
python main.py
This will:

Connect to the SQLite database or create it if it does not exist

Look for existing sessions for the user

Start a conversation with the memory agent

Persist all state changes to the database

Example Interactions
Try the following to verify persistent memory:

First run:

What's my name?

My name is John

Add a reminder to buy groceries

Add another reminder to finish the report

What are my reminders?

Exit the program with exit

Second run:

What's my name?

What reminders do I have?

Update my second reminder to submit the report by Friday

Delete the first reminder

The agent will remember your name and reminders between runs.

Using Database Storage in Production
Although this example uses SQLite, DatabaseSessionService supports multiple databases via SQLAlchemy:

PostgreSQL
postgresql://user:password@localhost/dbname

MySQL
mysql://user:password@localhost/dbname

MS SQL Server
mssql://user:password@localhost/dbname

For production deployments:

Choose a database suited for your scale

Configure connection pooling

Secure database credentials

Implement regular backups for critical agent data

Additional Resources
ADK Sessions Documentation
https://google.github.io/adk-docs/sessions/session/

Session Service Implementations
https://google.github.io/adk-docs/sessions/session/#sessionservice-implementations

State Management in ADK
https://google.github.io/adk-docs/sessions/state/

SQLAlchemy Documentation
https://docs.sqlalchemy.org/