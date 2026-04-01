# AIML Assignment Answer

## Problem

- Design an AI agent that helps students and faculty understand academic performance.
- The agent must retrieve academic records and attendance data from institutional systems.
- The agent must analyse historical academic data to detect trends and weak performance areas.
- The agent must combine structured academic data with academic policy or guidance material when giving recommendations.
- The agent must generate separate summaries for students and faculty members.
- The architecture must show data collection, validation, analysis, insight generation, and recommendation generation.

## Architecture / Flow Diagram

```text
+---------------------------+
| Student / Faculty Portal  |
| Web App / Chat Interface  |
+-------------+-------------+
              |
              v
+---------------------------+
| API Gateway / FastAPI     |
| Request Parsing           |
+-------------+-------------+
              |
              v
+---------------------------+
| Auth + Role Validation    |
| SSO / RBAC Service        |
+-------------+-------------+
              |
              v
+-----------------------------------+
| Academic AI Agent Orchestrator    |
| (LLM + LangGraph Workflow)        |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Intent + Persona Detection        |
| Student View / Faculty View       |
| Query Type / Time Range / Scope   |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Planner / Router                  |
| Select required data sources      |
| and analysis path                 |
+---------+------------+------------+
          |            |
          |            |
          v            v
+----------------+  +----------------------+
| Academic       |  | Attendance / LMS     |
| Records DB     |  | Records System       |
+--------+-------+  +----------+-----------+
         |                     |
         +----------+----------+
                    |
                    v
+-----------------------------------+
| Data Validation Layer             |
| Missing values, consistency,      |
| date range, student/faculty scope |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Decision: Sufficient Historical   |
| Data Available?                   |
+-----------+-----------------------+
            |Yes
            |                     No
            v                      v
+---------------------------+   +----------------------+
| Trend Analysis Engine     |   | Limited-Data Handler |
| grades, attendance, risk, |   | explain constraints, |
| weak-topic detection      |   | request more scope   |
+-------------+-------------+   +----------+-----------+
              |                            |
              v                            |
+-----------------------------------+      |
| Policy / Guidance Retriever       |<-----+
| Vector DB / Knowledge Base        |
| academic rules, support advice    |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Insight Fusion Layer              |
| Combine structured analytics      |
| with policy/guidance context      |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Recommendation Prioritizer        |
| Rank actions by severity, impact, |
| and policy relevance              |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Persona-Specific Summary Builder  |
| Student Summary / Faculty Summary |
+----------------+------------------+
                 |
                 v
+-----------------------------------+
| Response Composer                 |
| final explanation, trends, risks, |
| recommendations, next steps       |
+----------------+------------------+
                 |
                 v
+---------------------------+
| Final User Response       |
+---------------------------+

Shared supporting components:
- Redis session memory and caching
- Audit logging and monitoring
- Encryption and access control
- Prompt/response guardrails
```

## Component Explanation

1. The system starts when a student or faculty member enters a query through the portal or chat interface. The request first goes to the API layer, where the system performs authentication and role checking. This step is important because academic records are sensitive and should only be seen by authorized users.

2. After this, the **Academic AI Agent Orchestrator** understands the request and identifies whether the user is a student or a faculty member. It also detects what kind of analysis is needed, such as subject-wise performance, attendance analysis, semester trend, or class-level summary.

3. The **Planner / Router** then decides which internal systems should be used. For example, it may collect marks from the academic records database, attendance from the LMS or attendance system, and relevant rules or improvement guidelines from the academic policy knowledge base.

4. Once the data is collected, the **Data Validation Layer** checks whether the records are complete, correct, and relevant. It verifies things like missing marks, incomplete attendance records, wrong date range, or insufficient history. If enough historical data is not available, the system gives a limited response instead of making weak or misleading recommendations.

5. If sufficient data is available, the **Trend Analysis Engine** studies the student’s or class’s past performance. It identifies weak subjects, falling attendance, repeated low scores, and patterns that show where improvement is needed most.

6. The system then uses the **Policy / Guidance Retriever** to fetch academic rules, support material, and improvement guidelines. This is useful because recommendations should not be based only on marks and attendance, but also on academic policies and institutional guidance.

7. In the **Insight Fusion Layer**, the agent combines numerical data and policy information. After that, the **Recommendation Prioritizer** arranges the suggestions in order of importance, so the user gets the most useful actions first.

8. Finally, the **Persona-Specific Summary Builder** prepares different outputs for students and faculty members. Students receive personal improvement advice, while faculty receive class-level observations and intervention suggestions. The **Response Composer** then generates the final clear and meaningful answer.

## Libraries and Frameworks with Justification

- **LangGraph**: It is useful for managing the full agent workflow because this problem has many steps, decision points, and multiple system interactions.
- **OpenAI API or any enterprise LLM**: It helps the agent understand user queries, reason about the next step, and generate clear summaries and recommendations.
- **FastAPI**: It can be used to build the backend interface through which the portal or chatbot sends requests to the AI agent.
- **Pydantic**: It helps keep outputs structured and consistent, such as user type, weak subjects, trends, and recommendation priority.
- **SQLAlchemy**: It is useful for connecting with academic databases that store marks, grades, and attendance records.
- **Redis**: It can store short-term session data and cache frequently requested academic information for faster response.
- **FAISS or Chroma**: These are suitable for retrieving academic policies, guidance documents, and support material from unstructured text.
- **Pandas**: It is helpful for analysing academic history, finding trends, and identifying weak performance areas from structured data.
- **Prometheus/Grafana or ELK**: These tools are useful for logging, monitoring, and auditing system usage and performance.
- **RBAC / SSO Integration**: This is necessary to ensure that only authorized users can access confidential academic information.

## Short Submission Summary

This architecture satisfies the assignment because it is based on an AI agent that can choose the correct internal systems, validate academic data, analyse trends, combine data with policy guidance, and generate meaningful recommendations. It also includes multiple components, clear decision stages, and separate summaries for students and faculty, so it matches the requirement of a complete AI agent based system.
