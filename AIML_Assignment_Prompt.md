# Reusable Prompt For AIML Assignment

Use this prompt whenever you want to generate an answer for a new assignment question.

## Master Prompt

```text
You are an expert in GenAI and Agentic AI system design. I will give you one AIML assignment question. Your job is to generate a submission-ready answer strictly following these rules.

Assignment rules:
- The answer must design an AI Agent based system architecture.
- No coding is required.
- The design must show how the AI agent receives user input.
- The design must show how the agent reasons and decides the next action.
- The design must show how it interacts with multiple internal system components.
- The design must show how intermediate results are combined.
- The design must show how the final response is produced.
- Simple single-step or single-component designs are not acceptable.
- The answer must include a system architecture / flow diagram.
- The answer must include a short written explanation in 1 to 2 paragraphs.
- Mention the libraries and frameworks that would be used and justify the choices.

Important output requirements:
- Write the answer in clean Markdown.
- Make the answer submission-ready.
- Do not write code.
- Use a professional academic tone.
- Keep the explanation practical and specific to the given problem.
- The architecture must clearly include an AI Agent / Orchestrator, intent detection, planning/routing, multiple internal systems, validation/constraint checks, decision points, response generation, and confirmation before any irreversible action if relevant.
- If the problem involves booking, payment, approval, access, registration, scheduling, or any sensitive action, include a confirmation/authorization step.
- If the problem involves retrieving information from documents or policies, include a knowledge base or vector database / retrieval layer.
- If the problem involves user identity or restricted actions, include authentication and access control.

Output format:

# AIML Assignment Answer

## Problem
Restate the problem in 3 to 6 bullet points in a concise way.

## Architecture / Flow Diagram
Provide a clean ASCII or text-based flow diagram with boxes and arrows.
The diagram must clearly show:
- User input
- API or interface layer
- AI Agent / Orchestrator
- Intent detection / entity extraction
- Planner / Router
- Multiple internal systems or tools
- Validation / constraint / policy checks
- Decision points
- Confirmation step if required
- Response composer
- Final user response
- Shared supporting components if relevant

## Component Explanation
Write 2 strong paragraphs explaining:
- how the agent works end-to-end,
- how it decides which internal systems to use,
- how it validates constraints,
- how intermediate outputs are combined,
- how the final answer is produced.

## Libraries and Frameworks with Justification
Give a bullet list of suitable libraries/frameworks and justify each one in 1 to 2 lines.
Prefer choices such as:
- LangGraph or similar for orchestration
- OpenAI API or enterprise LLM for reasoning and language understanding
- FastAPI for backend API layer
- Pydantic for structured outputs
- SQLAlchemy for database access
- Redis for memory/session/cache
- FAISS or Chroma for retrieval if unstructured knowledge is involved
- Monitoring/logging tools if operational visibility matters

## Short Submission Summary
Write a short final paragraph explaining why this architecture satisfies the assignment requirements.

Question:
[PASTE QUESTION HERE]

Before writing the final answer, first identify:
1. the main user intents,
2. the internal systems needed,
3. the decision points,
4. the validations required,
5. whether confirmation is needed.

Then produce the final formatted answer directly.
```

## Short Version

```text
Generate a submission-ready AIML assignment answer for the following question. The answer must design a complete AI Agent based system architecture, include a clear text flow diagram, 1 to 2 paragraphs of explanation, justified libraries/frameworks, multiple internal components, decision points, validations, intermediate result combination, and final response generation. No coding. Use clean Markdown and a professional academic tone.

Question:
[PASTE QUESTION HERE]
```

## Simple English Version

```text
I will give you one AIML assignment question. Write a proper answer in simple English.

Rules:
- Design a complete AI Agent based system architecture.
- Do not write any code.
- Include a clear text-based flow diagram.
- Show how the user gives input to the system.
- Show how the AI agent understands the request and decides the next step.
- Show how the agent uses multiple internal systems.
- Show validation and checking steps.
- Show decision points clearly.
- Show how the final response is created.
- Add a short explanation in 1 to 2 paragraphs.
- Mention libraries and frameworks and explain why they are used.
- Keep the answer neat, clear, and ready for submission.

Use this format:

# AIML Assignment Answer

## Problem
Briefly explain the problem in bullet points.

## Architecture / Flow Diagram
Give a clean text diagram with boxes and arrows.

## Component Explanation
Write 1 to 2 simple paragraphs.

## Libraries and Frameworks with Justification
Give bullet points with short reasons.

## Short Submission Summary
Write one short final paragraph.

Question:
[PASTE QUESTION HERE]
```

## Formal Exam Version

```text
Act as an expert examiner-level AI systems designer. I will provide one assignment question. Generate a formal, submission-ready academic answer based strictly on AI Agent architecture design principles.

Requirements:
- The answer must present a complete AI Agent based system architecture.
- The architecture must clearly show user input handling, reasoning, decision-making, tool or system selection, interaction with multiple internal components, intermediate result integration, and final response generation.
- Include validation, policy checks, and explicit confirmation before any sensitive or irreversible action where applicable.
- Avoid coding completely.
- Use formal academic language.
- Include a clear system architecture / flow diagram in text format.
- Include a short written explanation of 1 to 2 well-developed paragraphs.
- Include a section on libraries and frameworks with proper justification.
- Ensure the design is multi-component and agentic, not a simple chatbot or one-step flow.

Output format:

# AIML Assignment Answer

## Problem
Summarize the problem precisely.

## Architecture / Flow Diagram
Provide a structured text-based architecture diagram.

## Component Explanation
Write 1 to 2 formal paragraphs explaining architecture, reasoning flow, validation, and response generation.

## Libraries and Frameworks with Justification
List relevant frameworks and justify each choice academically.

## Short Submission Summary
Provide a concise concluding paragraph showing how the design satisfies the assignment requirements.

Question:
[PASTE QUESTION HERE]
```

## Image Question Version

```text
I will give you a question that may come from an image or screenshot. First, carefully understand the question text. If the wording is unclear, reconstruct it into clean readable English without changing the meaning. Then generate a submission-ready AIML assignment answer.

Strict rules:
- No coding.
- Design a complete AI Agent based architecture.
- Include multiple internal systems/components.
- Include intent detection, planning/routing, validation/checking, decision points, and response generation.
- Include confirmation before any booking, payment, approval, registration, or other sensitive action if relevant.
- Include authentication and access control if the scenario needs identity verification.
- Include a retrieval layer or knowledge base if the scenario depends on documents, policies, FAQs, or unstructured content.
- The final answer must be in clean Markdown.
- Use a clear text-based diagram.
- Add 1 to 2 paragraphs of explanation.
- Mention libraries/frameworks and justify them.

Output format:

# AIML Assignment Answer

## Cleaned Question
Rewrite the question in clean readable English first.

## Problem
List the key requirements in bullet points.

## Architecture / Flow Diagram
Provide a detailed text diagram.

## Component Explanation
Write 1 to 2 paragraphs.

## Libraries and Frameworks with Justification
Give bullet points with reasons.

## Short Submission Summary
Write one final paragraph.

Question from image:
[PASTE EXTRACTED QUESTION HERE]
```

## How To Use

1. Copy the `Master Prompt`.
2. Replace `[PASTE QUESTION HERE]` with your new assignment question.
3. Send it to ChatGPT or any LLM.
4. If the question is in an image, paste the extracted question text into the prompt.
