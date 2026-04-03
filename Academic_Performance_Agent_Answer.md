# AIML Assignment Answer

## Problem

- Design an AI agent for a college website that answers questions related to admissions, courses, and departments.
- The agent must also handle queries about fees, scholarships, academic policies, administrative policies, timings, and important dates.
- The agent must use only official college documents and structured institutional data sources.
- The agent must classify each query into categories such as admission, academics, finance, policy, or general.
- The agent must decide whether the answer needs structured data, document-based knowledge, or both.
- The architecture must show interpretation, source selection, retrieval, validation, and answer generation clearly.

## Architecture / Flow Diagram

```text
+----------------------------+
| User on College Website    |
| Chatbot / Search Interface |
+-------------+--------------+
              |
              v
+----------------------------+
| API Layer / FastAPI        |
| Request Parsing            |
+-------------+--------------+
              |
              v
+----------------------------+
| Query Preprocessor         |
| clean text, detect entity, |
| identify missing details   |
+-------------+--------------+
              |
              v
+-----------------------------------+
| College AI Agent Orchestrator     |
| (LLM + LangGraph Workflow)        |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Intent and Category Detection     |
| Admission / Academics / Finance / |
| Policy / General                  |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Clarification Decision            |
| Is the query specific enough?     |
+-----------+-----------------------+
            |Yes
            |                     No
            v                      v
+---------------------------+   +----------------------+
| Source Selection Engine   |   | Clarification Module |
| Structured / Documents /  |   | ask user for missing |
| Hybrid retrieval          |   | details              |
+-----------+---------------+   +----------+-----------+
            |                              |
            +--------------+---------------+
                           |
                           v
+-----------------------------------+
| Retrieval Layer                   |
+-----------+------------+----------+
            |            | 
            |            |
            v            v
+----------------+  +----------------------+
| Structured DBs |  | Official Document KB |
| fee tables,    |  | prospectus, policy,  |
| dates, dept    |  | handbook, notices    |
| listings       |  |                      |
+--------+-------+  +----------+-----------+
         |                     |
         +----------+----------+
                    |
                    v
+-----------------------------------+
| Evidence Validation Layer         |
| official source check, freshness, |
| completeness, consistency          |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Decision: Is Evidence Sufficient? |
+-----------+-----------------------+
            |Yes
            |                     No
            v                      v
+---------------------------+   +----------------------+
| Answer Planning Layer     |   | Fallback Handler     |
| choose answer structure   |   | ask follow-up or say |
| and key points            |   | insufficient data    |
+-------------+-------------+   +----------+-----------+
              |                            |
              v                            |
+-----------------------------------+      |
| Response Generator                |<-----+
| combine retrieved facts and       |
| document evidence into answer     |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Final Response                    |
| concise answer + source-backed    |
| details + next guidance           |
+-----------------------------------+

Shared supporting components:
- Source registry for official college systems only
- Vector database for document retrieval
- Logging and monitoring
- Cache/session memory
```

## Component Explanation

1. The system starts when a user asks a question on the college website. The request first goes to the API layer, where it is cleaned and prepared for processing. The AI agent then reads the query and identifies the main category, such as admission, academics, finance, policy, or general information.

2. After understanding the category, the agent checks whether the query is clear enough. If important information is missing, such as course name, department, or admission year, the **Clarification Module** asks the user for more details before moving ahead. This helps the system avoid giving incomplete or wrong answers.

3. Once the query is clear, the **Source Selection Engine** decides where the answer should come from. If the question is about fee amount, deadlines, or department lists, it uses structured data sources. If the question is about rules, scholarships, or academic policies, it uses official document-based knowledge. If needed, it can use both sources together.

4. The **Retrieval Layer** collects data only from official college-maintained sources. This is important because the question clearly says the agent must not depend on unofficial content. The **Evidence Validation Layer** then checks whether the collected information is complete, up-to-date, and consistent across sources.

5. After validation, the agent decides whether enough evidence is available to answer correctly. If the evidence is weak or incomplete, the system either asks a follow-up question or tells the user that sufficient information is not available. If the evidence is strong, the **Answer Planning Layer** organizes the response and decides what information should be shown first.

6. Finally, the **Response Generator** combines the retrieved data and document-based evidence into a final user-friendly response. The answer can include fees, admission deadlines, department details, policy information, timings, or other official guidance in a clear and reliable way.

## Internal Capabilities of the Agent

- **Query Understanding and Classification**: The agent can understand the user question and classify it into admission, academics, finance, policy, or general category.
- **Source Selection**: The agent can decide whether the answer needs structured records, document-based retrieval, or both.
- **Clarification Handling**: The agent can detect incomplete queries and ask the user for missing information before retrieval.
- **Evidence Validation**: The agent can verify whether the retrieved information is official, complete, and sufficient for generating a correct answer.
- **Reliable Response Generation**: The agent can combine data from multiple official sources and generate a final clear answer.

## Libraries and Frameworks with Justification

- **LangGraph**: It is useful for managing the full agent workflow because this problem includes classification, clarification, routing, retrieval, validation, and answer generation.
- **OpenAI API or any enterprise LLM**: It helps the agent understand natural language queries, reason about source selection, and generate clear responses.
- **FastAPI**: It can be used to connect the AI agent with the college website chatbot or query interface.
- **Pydantic**: It helps keep outputs structured, such as query category, source type, missing information, and validation result.
- **SQLAlchemy**: It is useful for connecting with structured institutional sources like fee tables, deadlines, and department listings.
- **FAISS or Chroma**: These are suitable for retrieving information from official documents such as prospectus files, policy documents, and notices.
- **Redis**: It can store short-term session data and improve response speed by caching repeated queries.
- **Prometheus/Grafana or ELK**: These tools are helpful for monitoring, logging, and checking the performance of the AI agent.

## Short Submission Summary

This architecture satisfies the assignment because it is based on an AI agent that can understand user queries, choose the correct official data source, validate the retrieved evidence, and generate accurate responses. It includes multiple internal components, decision points, clarification handling, source selection, retrieval, validation, and final answer generation, so it represents a complete AI agent based system rather than a simple chatbot.
