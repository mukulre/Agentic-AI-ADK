# Agent Development Kit (ADK) 

This repository contains hands-on examples for learning Google’s Agent Development Kit (ADK), a powerful framework for building production-grade, LLM-powered agents.

The course progresses from simple agents to advanced, stateful, multi-agent systems, giving you a practical and structured path to mastering ADK.

---

## Getting Started

### Environment Setup

You only need **one virtual environment** for all examples in this repository.

Follow these steps from the root directory:

```bash
# Create a virtual environment
python -m venv .venv

# Activate the environment (each new terminal)
# macOS/Linux
source .venv/bin/activate

# Windows CMD
.venv\Scripts\activate.bat

# Windows PowerShell
.venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt
Once created, this single environment will work for every example in the course.

Setting Up API Keys
Create a Google Cloud account
https://cloud.google.com/?hl=en

Create a new Google Cloud project

Generate an API key
https://aistudio.google.com/apikey

Assign the API key to your project

Connect the project to a billing account

Each example folder includes a .env.example file.

For any example you want to run:

Navigate to the example folder

Rename .env.example to .env

Open .env and add your API key:

env
Copy code
GOOGLE_API_KEY=your_api_key_here