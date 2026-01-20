# LinkedIn Post Generator Loop Agent

This example demonstrates how to combine Sequential and Loop Agent patterns in the Agent Development Kit (ADK) to generate and iteratively refine a LinkedIn post until quality requirements are met.

---

## Overview

The LinkedIn Post Generator uses a structured pipeline with an embedded refinement loop to:

1. Generate an initial LinkedIn post  
2. Iteratively review and improve the post until it meets defined quality criteria  

This example showcases several important ADK patterns:

1. **Sequential Pipeline**  
   A multi-step workflow with clearly defined stages.

2. **Iterative Refinement**  
   A loop-based process that repeatedly improves content.

3. **Automatic Quality Checking**  
   Validation against explicit content and formatting requirements.

4. **Feedback-Driven Refinement**  
   Improvements guided by reviewer-generated feedback.

5. **Loop Exit Tool**  
   A tool-based mechanism to terminate the loop when requirements are satisfied.

---

## Architecture

The system is composed of the following components.

---

### Root Sequential Agent

**LinkedInPostGenerationPipeline**

A `SequentialAgent` that orchestrates the entire workflow:

1. Generates the initial LinkedIn post  
2. Executes the refinement loop until completion  

---

### Initial Post Generator

**InitialPostGenerator**

An `LlmAgent` responsible for creating the first draft of the LinkedIn post with no prior context.

---

### Refinement Loop

**PostRefinementLoop**

A `LoopAgent` that runs a two-stage refinement cycle:

1. Executes the reviewer to evaluate post quality and potentially exit the loop  
2. Executes the refiner to improve the post when further refinement is needed  

---

### Sub-Agents Inside the Refinement Loop

1. **Post Reviewer (`PostReviewer`)**  
   - Evaluates post quality  
   - Provides specific feedback  
   - Terminates the loop when all requirements are met  

2. **Post Refiner (`PostRefiner`)**  
   - Improves the post based on reviewer feedback  
   - Refines tone, clarity, structure, and compliance  

---

### Tools

1. **Character Counter**  
   - Validates post length against LinkedIn requirements  
   - Used by the reviewer  

2. **Exit Loop Tool**  
   - Signals the loop to terminate when quality criteria are satisfied  
   - Used by the reviewer  

---

## Loop Control with Exit Tool

A core design pattern in this example is explicit loop control using an `exit_loop` tool.

The **Post Reviewer** has two responsibilities:

1. **Quality Evaluation**  
   Determines whether the post meets all defined requirements.

2. **Loop Control**  
   Calls the `exit_loop` tool when the post passes all checks.

When the `exit_loop` tool is invoked:

1. `tool_context.actions.escalate` is set to `True`  
2. The `LoopAgent` detects this signal and stops iterating  

This approach follows ADK best practices by:

- Separating generation from refinement  
- Giving the reviewer authority over loop termination  
- Using a dedicated refinement agent  
- Managing control flow through explicit tools  

---

## Usage

To run this example:

```bash
cd 11-loop-agent
adk web
In the web interface, enter a prompt such as:

nginx
Copy code
Generate a LinkedIn post about what I've learned from @aiwithbrandon's Agent Development Kit tutorial.
The system will:

Generate an initial LinkedIn post

Review the post for quality and compliance

Exit the loop if requirements are met

Otherwise, provide feedback and refine the post

Repeat until the post meets requirements or the maximum iteration limit is reached

Return the final refined post