# 🧠 Deep Agent Text-to-SQL Evaluation System

A production-style **multi-agent Text-to-SQL system with evaluation, repair loops, and regression testing** built using LLMs and LangGraph-style orchestration.

---

# 🚀 Overview

This project implements an end-to-end **agentic pipeline for converting natural language questions into SQL queries**, executing them, and evaluating results.

It includes:

- Multi-step LLM agent pipeline
- SQL generation + validation
- Execution engine with retry + repair loop
- Trajectory logging for debugging
- Evaluation + scoring framework
- Regression testing suite

---

### 🧰 Agent Roster
1. **Planner Agent:** Creates high-level analytical plans without code generation.
2. **Schema Explorer Agent:** Isolates relevant entities and join paths using the schema catalog.
3. **SQL Generator Agent:** Produces exact SQLite queries following formatting guardrails.
4. **SQL Repair Agent:** An expert debugging agent that inspects traceback exceptions and iteratively fixes broken SQL queries.
5. **LLM Judge / Evaluator:** A decoupled evaluation layer scoring final generation quality from `0-10`.

---

## 🚀 Key Features

* **LangGraph Orchestration:** Replaces traditional fragile sequential chains with a declarative, graph-based execution runtime featuring native state management and conditional routing.
* **Self-Healing SQL Repair Loop:** Automatically intercepts execution runtime crashes, routing state vectors back to the repair agent to re-synthesize code up to 2 times.
* **Unified State Management:** Maintains full transaction visibility through a custom `AgentState` schema tracker that captures granular task transitions, elapsed execution latencies, and step trajectories.
* **Automated Regression & Evaluation Suite:** Evaluates generations across structural, behavioral, semantic, and structural boundaries using a weighted composite formula:
  $$\text{Composite Score} = (0.3 \times \text{SQL Presence}) + (0.2 \times \text{Execution Success}) + \left(0.3 \times \frac{\text{LLM Score}}{10}\right) + (0.2 \times \text{Exact Match})$$
* **Security Interceptor Guardrails:** Sanitizes and strips generated strings using AST-level string interceptors to fully prevent malicious state operations (`DROP`, `DELETE`, `UPDATE`, `ALTER`).

---


