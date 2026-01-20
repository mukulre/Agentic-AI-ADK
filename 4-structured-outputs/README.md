# Structured Outputs in ADK

This example demonstrates how to implement structured outputs in the Agent Development Kit (ADK) using Pydantic models. The main agent in this example, `email_generator`, uses the `output_schema` parameter to ensure its responses conform to a specific structured format.

---

## What Are Structured Outputs?

ADK allows you to define structured data formats for agent inputs and outputs using Pydantic models.

Key benefits include:

1. **Controlled Output Format**  
   Using `output_schema` ensures the LLM produces responses in a consistent JSON structure.

2. **Data Validation**  
   Pydantic validates that all required fields are present and correctly formatted.

3. **Improved Downstream Processing**  
   Structured outputs are easier to consume in downstream applications or by other agents.

Use structured outputs when format consistency is critical for system integration or agent-to-agent communication.

---

## Email Generator Example

This example implements an email generator agent that produces structured output containing:

1. **Email Subject**  
   A concise and relevant subject line.

2. **Email Body**  
   Well-formatted email content including greeting, paragraphs, and signature.

The agent uses a Pydantic model called `EmailContent` to define this structure, ensuring every response follows the same format.

---

### Output Schema Definition

The Pydantic model explicitly defines the required fields and their descriptions:

```python
class EmailContent(BaseModel):
    """Schema for email content with subject and body."""
    
    subject: str = Field(
        description="The subject line of the email. Should be concise and descriptive."
    )
    body: str = Field(
        description="The main content of the email. Should be well-formatted with proper greeting, paragraphs, and signature."
    )

Setup

Activate the virtual environment from the root directory:

# macOS/Linux
source ../.venv/bin/activate

# Windows CMD
..\.venv\Scripts\activate.bat

# Windows PowerShell
..\.venv\Scripts\Activate.ps1


Create a .env file and add your Google API key:

GOOGLE_API_KEY=your_api_key_here

Running the Example
cd 4-structured-outputs
adk web

Additional Resources

ADK Structured Data Documentation
https://google.github.io/adk-docs/agents/llm-agents/#structuring-data-input_schema-output_schema-output_key

Pydantic Documentation
https://docs.pydantic.dev/latest/