# =========================
# README.md
# =========================

# Basic ADK Agent Example

This repository shows how to build and run a **minimal ADK LLM Agent** using the Agent Development Kit (ADK).

It focuses on:
- Correct project structure
- Agent discovery rules
- A working, minimal `LlmAgent`
- Running the agent via Web UI, CLI, or API

If ADK is the nervous system, this example is a reflex arc: simple, fast, and alive.

---

## What Is an ADK Agent?

An ADK agent is powered by `LlmAgent` (often imported as `Agent`).  
This is the reasoning core of your application.

An `LlmAgent` can:
- Understand natural language
- Reason about user intent
- Generate responses
- Decide whether to use tools
- Transfer control to other agents

Its behavior is **non-deterministic**.  
It interprets instructions dynamically using an LLM instead of following fixed workflows.

---

## Required Project Structure

ADK uses convention-based discovery.  
If the structure is wrong, the agent is invisible.


---

## File Responsibilities

### `__init__.py`
Makes the folder a Python package and exposes the agent.

### `agent.py`
Defines the agent and exposes `root_agent`.

### `.env`
Stores environment variables such as API keys.

---

## Environment Setup

Activate the virtual environment created at the project root.

### macOS / Linux
```bash
source ../.venv/bin/activate

### Windows (CMD)
..\.venv\Scripts\activate.bat

### Windows (PowerShell)
..\.venv\Scripts\Activate.ps1

### Running the Agent

Always run ADK commands from the parent folder, not inside the agent directory.

### Start Web UI

adk web

### Run in Terminal
adk run greeting_agent

### Run as API Server
adk api_server