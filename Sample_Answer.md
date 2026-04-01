# AIML Assignment Answer

## Problem
Design an AI agent for a college campus that can:
- answer upcoming event queries,
- provide room and lab availability,
- share campus facility details,
- handle registration and booking-related requests.

The agent must detect intent, retrieve data from the right internal systems, validate availability and constraints, ask for confirmation before bookings, and generate a final response.

## Architecture / Flow Diagram

```text
+----------------------+
| User Web / Chat UI   |
+----------+-----------+
           |
           v
+----------------------+
| API Layer / FastAPI  |
| Auth + Request Parse |
+----------+-----------+
           |
           v
+------------------------------+
| Campus AI Agent Orchestrator |
| (LLM + LangGraph workflow)   |
+----------+-------------------+
           |
           v
+------------------------------+
| Intent Detection + Entity    |
| Extraction                   |
| Intent = Event / Facility /  |
| Availability / Booking       |
+----------+-------------------+
           |
           v
+------------------------------+
| Planner / Router             |
| Select tools and checks      |
+----+-----------+-------------+
     |           |              |
     |           |              |
     v           v              v
+-----------+  +------------------+  +----------------------+
| Event     |  | Facility Info    |  | Availability &       |
| Service   |  | Service          |  | Constraint Engine    |
| Connector |  | Connector        |  |                      |
+-----+-----+  +--------+---------+  +----------+-----------+
      |                 |                       |
      |                 |                       |
      v                 v                       v
+-----------+   +------------------+   +----------------------+
| Campus    |   | Facilities DB /  |   | Room Scheduler       |
| Events DB |   | Asset Registry   |   +----------------------+
+-----------+   +------------------+   +----------------------+
                                         | Lab Booking System  |
                                         +----------------------+
                                         +----------------------+
                                         | Policy / Academic    |
                                         | Rules Repository     |
                                         +----------+-----------+
                                                    |
                                                    v
               +---------+---------+
               | Need booking?     |
               +----+----------+---+
                    |          |
                  No|          |Yes
                    |          v
                    |  +----------------------+
                    |  | Confirmation Manager |
                    |  | Ask explicit user    |
                    |  | approval             |
                    |  +----------+-----------+
                    |             |
                    |      +------+------+
                    |      | Confirmed?  |
                    |      +---+-----+---+
                    |          |     |
                    |        No|     |Yes
                    |          |     v
                    |          | +----------------------+
                    |          | | Booking Executor     |
                    |          | | Update registration  |
                    |          | | or room/lab booking  |
                    |          | | system               |
                    |          | +--------+-------------+
                    |          |          |
                    +----------+----------+
                                      |
                                      v
                         +--------------------------+
                         | Response Composer        |
                         | Merge results, explain   |
                         | status, alternatives,    |
                         | next steps               |
                         +------------+-------------+
                                      |
                                      v
                         +--------------------------+
                         | User Response            |
                         +--------------------------+

Shared supporting components:
- Session Memory / Redis
- Vector KB for campus policies, facilities FAQ, event descriptions
- Audit Logging and Monitoring
- Role-based access control
```

## Component Explanation

The proposed system uses a central **Campus AI Agent Orchestrator** as the decision-making layer. A student or staff member sends a query through a web or chat interface, and the API layer first authenticates the user and normalizes the request. The AI agent then performs **intent detection** and **entity extraction** to identify whether the request is about an event, facility, room/lab availability, or an actual booking. Based on this intent, a **planner/router** decides which internal campus systems should be consulted, such as the campus events database, facility registry, room scheduler, lab booking system, and policy repository. This makes the architecture agentic because the AI agent is not giving a direct answer immediately; instead, it chooses tools, sequences internal actions, and combines intermediate outputs.

For all availability and booking-related requests, the agent invokes an **Availability and Constraint Engine** to verify room or lab status, operating hours, maintenance blocks, capacity limits, and user eligibility rules. If the request includes a booking or registration action, the agent does not proceed automatically; it sends the request to a **Confirmation Manager**, which explicitly asks the user for final approval. Only after confirmation does the **Booking Executor** update the relevant institutional system, such as an event registration platform or room/lab reservation system. Finally, the **Response Composer** merges data from multiple sources and generates a complete answer, such as available slots, booking status, event information, facility details, or suggested alternatives when constraints are not satisfied.

## Libraries and Frameworks with Justification

- **LangGraph**: Best suited for multi-step AI agent workflows with branching, tool use, confirmation loops, and state transitions. This assignment explicitly requires decision points and multiple internal actions, which LangGraph handles better than a simple linear chain.
- **OpenAI API or another enterprise LLM**: Used for natural language understanding, intent detection, entity extraction, reasoning, and response generation. The LLM helps the agent interpret free-form campus queries and decide the next action.
- **FastAPI**: A lightweight and efficient backend framework for exposing the agent as a campus web service or chatbot API. It is easy to integrate with authentication, booking endpoints, and monitoring.
- **Pydantic**: Ensures structured outputs from the LLM, such as `intent`, `date`, `time`, `facility_type`, and `booking_action`. This reduces ambiguity and improves reliability.
- **SQLAlchemy**: Useful for integrating with structured institutional databases like event schedules, room allocation tables, and lab reservation records.
- **Redis**: Supports session memory, short-term context, and caching of repeated queries such as frequently asked facility information or recent conversation state.
- **Vector Database (FAISS or Chroma)**: Helps retrieve unstructured campus documents like facility rules, booking policies, and event descriptions through semantic search.
- **Mermaid / Draw.io**: Suitable for representing the architecture and decision flow clearly in the final PDF submission.
- **Logging and Monitoring Tools (Prometheus/Grafana or ELK)**: Important for auditing booking actions, tracing failures, and monitoring system health in a real campus deployment.

## Short Submission Summary

This architecture satisfies the assignment because the AI agent actively decides which internal system to consult, whether validation is required, and whether explicit confirmation must be taken before a booking is executed. The design includes multiple internal components, conditional branches, intermediate result combination, and final response generation, which matches the requirement for a complete AI agent-based system rather than a single-step chatbot.
