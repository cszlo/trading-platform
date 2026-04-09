# Chapter 9 — Agent Architecture & Boundaries

> Status: 🔲 Not started

## Purpose
Design the agents that survived the Chapter 8 filter. Define what each agent owns, what it consumes, what it produces, and how agents communicate. Every agent must be independently testable and have a clear, bounded responsibility.

---

## 9.1 Agent Roster
*Populated after Chapter 8 filter.*

| Agent | Responsibility | Inputs | Outputs |
|---|---|---|---|
| TBD | | | |

---

## 9.2 Agent Communication Design
*How do agents talk to each other?*

Options:
- Direct function calls with typed inputs/outputs
- Message bus / event queue
- Shared state store (DB-backed)
- Async task queue

*Decision: ___*

---

## 9.3 The Coordinator
*Routes signals to the appropriate execution strategy based on agent outputs.*

- What information does the coordinator consume?
- What is the routing logic?
- How does the coordinator handle conflicting agent recommendations?
- What is the coordinator's behavior when an agent is unavailable?

---

## 9.4 Agent Boundaries
*What each agent is explicitly NOT responsible for.*

---

## 9.5 Agent Contracts
*Typed input/output definitions for each agent. These are the interfaces — not implementations.*

---

## 9.6 Failure Modes
*What happens when an agent fails, times out, or returns a low-confidence result?*

- Fallback to deterministic behavior
- Skip signal for current bar
- Alert and halt

---

## 9.7 Testing Strategy
*How is each agent tested in isolation? How is the coordinator tested end-to-end?*

---

## 9.8 Orchestration Framework Decision
*LangGraph, custom, Claude Agent SDK, or something else? Evaluated here after architecture is clear.*

---

## 9.9 Open Questions from This Chapter
