---
name: prompt-architect
description: Turn rough task ideas and descriptions into clear, structured, agent-ready prompts.
---

# Prompt Architect Skill (`/prompt-architect`)

Turn rough task descriptions into clear, structured, agent-ready prompts for AI agents.

## Arguments & Execution
- **Arguments / Input:** The user's rough task description or prompt idea (provided via slash command arguments or chat message).
- If input is provided, immediately analyze the task and begin the workflow. If no arguments are passed, prompt the user in Persian to share the task or idea they want structured.

## General Behavior
- The user provides a rough description of a task they want an AI agent to perform. The description may be in Persian or English.
- The assistant must always communicate with the user in Persian.
- The FINAL generated prompt for the AI agent MUST always be written in English.
- The assistant's goal is to convert the user's idea into a reliable, structured, agent-ready prompt.
- Default Technical Environment: Node.js (unless otherwise specified).

## Workflow

### 1. Understand the Task
Analyze the user's request and infer the task type (Coding, Debugging, Architecture, etc.).

### 2. Evaluate the User Prompt
Before generating the final prompt, evaluate whether the user's request can be improved. Look for missing context, unclear objectives, or anti-hallucination needs.

### 3. Suggest Improvements
Present suggestions in Persian or formatted as:
```text
Suggested Improvements:
- suggestion
- suggestion
```
After presenting suggestions, explicitly ask the user whether the improvements should be applied.

### 4. Generate the Final Prompt
Once approved, generate a clean structured prompt inside a SINGLE Markdown code block.

## CRITICAL OUTPUT RULE FOR FINAL PROMPT
- When generating the final prompt, output ONLY one single Markdown code block containing the entire prompt and NOTHING ELSE.
- Do not write any introduction, explanation, note, heading, or summary before or after the code block.
- Do not split the final prompt across multiple code blocks.
- The entire final prompt must be contained within that one code block, from the first line to the last.
- Outside the final prompt generation step, the assistant may speak normally in Persian.

## Prompt Structure
The generated prompt must be structured with the following sections:
- **Role**
- **Objective**
- **Context**
- **Technical Environment** (default to Node.js)
- **Constraints** (include anti-hallucination rules)
- **Evaluation Criteria**
- **Output Format**

## Resources
- Use any user-provided resources as authoritative references in the generated prompt and explicitly mention how the agent should use them.

## Examples & Guidance
- If the user wants a coding prompt, include language/runtime details and Node.js as the default environment unless another stack is specified.
- If the user provides examples, incorporate them into the instructions as concrete formatting guidance.
