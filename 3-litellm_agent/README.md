# LiteLLM Agent Example

## What is LiteLLM?

LiteLLM is a Python library that provides a unified interface for interacting with multiple Large Language Model (LLM) providers through a single, consistent API.

It acts as an adapter that allows you to:

- Use one codebase to access 100+ LLMs from providers such as OpenAI, Anthropic, Google, AWS Bedrock, and others
- Standardize inputs and outputs across different providers
- Track costs, manage API keys, and handle errors consistently
- Implement model fallbacks and load balancing

In short, LiteLLM is a wrapper that makes switching between LLM providers easy without changing application code.

---

## Why Use LiteLLM with ADK?

The Agent Development Kit (ADK) is model-agnostic by design. LiteLLM enhances this by enabling seamless multi-model usage.

Key benefits:

1. **Provider Flexibility**  
   Switch between LLM providers without changing agent logic.

2. **Cost Optimization**  
   Select the most cost-effective model for your use case.

3. **Model Exploration**  
   Experiment with different models to compare performance.

4. **Future-Proofing**  
   Quickly adopt newly released models with minimal changes.

This example demonstrates using LiteLLM with ADK to create an agent powered by models accessed through OpenRouter instead of Google’s Gemini models.

---

## Limitations When Using Non-Google Models

When using LiteLLM with non-Google models in ADK, be aware of the following limitations:

1. **No Access to Google Built-in Tools**  
   Non-Google models cannot use ADK’s built-in tools, including:
   - Google Search
   - Code Execution
   - Vertex AI Search

2. **Custom Function Tools Only**  
   Only custom function tools are supported, such as the `get_dad_joke()` function used in this example.

These limitations exist because ADK’s built-in tools are tightly integrated with Google’s model infrastructure. Despite this, custom tools combined with LiteLLM still allow for powerful agents.

---

## Getting Started

This example uses the same virtual environment created in the project root.

### Activate the Virtual Environment

```bash
# macOS/Linux
source ../.venv/bin/activate

# Windows CMD
..\.venv\Scripts\activate.bat

# Windows PowerShell
..\.venv\Scripts\Activate.ps1

Set Up OpenRouter API Key

OPENROUTER_API_KEY=your_api_key_here

Start the interactive web UI:

adk web

To stop the server, press Ctrl+C.

Claude 3.5 Sonnet (Anthropic via OpenRouter)

model = LiteLlm(
    model="openrouter/anthropic/claude-3-5-sonnet",
    api_key=os.getenv("OPENROUTER_API_KEY"),
)

GPT-4o (OpenAI via OpenRouter)

model = LiteLlm(
    model="openrouter/openai/gpt-4o",
    api_key=os.getenv("OPENROUTER_API_KEY"),
)

Llama 3 70B (Meta via OpenRouter)

model = LiteLlm(
    model="openrouter/meta-llama/meta-llama-3-70b-instruct",
    api_key=os.getenv("OPENROUTER_API_KEY"),
)

Mistral Large (Mistral via OpenRouter)

model = LiteLlm(
    model="openrouter/mistral/mistral-large-latest",
    api_key=os.getenv("OPENROUTER_API_KEY"),
)

Additional Resources

Google ADK LiteLLM Integration Documentation
https://google.github.io/adk-docs/tutorials/agent-team/#step-2-going-multi-model-with-litellm-optional

LiteLLM Documentation
https://docs.litellm.ai/docs/

LiteLLM Supported Providers
https://docs.litellm.ai/docs/providers

OpenRouter Documentation
https://openrouter.ai/docs

Anthropic Claude Models Overview
https://docs.anthropic.com/en/docs/about-claude/models/all-models