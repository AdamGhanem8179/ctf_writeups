# Write-Up: Assistant or Agent?

**Tags:** `AI`, `LLM Security`, `AI Ethics`, `Autonomous Agents`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> **Assistant or Agent?** is an interactive narrative challenge set in Westbrook High that explores the operational and security boundaries between an **AI Assistant** (passive, read-only, advisory) and an **AI Agent** (active, autonomous execution with real-world side effects). Through branching narrative choices, the challenge illustrates why autonomous systems require strict human review checkpoints, principle-of-least-privilege permissions, and runtime guardrails before executing irreversible actions. Navigating the scenario by enforcing these safety boundaries keeps the high school's systems intact and reveals the flag.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Assistant or Agent? |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 2026 |

### Description

> *Return to Westbrook High in this playful AI ethics interactive fiction. Learn when an AI assistant should advise, when an AI agent should act, and how permissions, guardrails, and review checkpoints keep autonomous actions safe.*

---

## Narrative Breakdown & Core Concepts

Instead of a traditional computational exploit or dataset tuning, this scenario uses an interactive story to test your understanding of autonomous AI governance:

### 1. Assistant vs. Agent
* **The Assistant Role:** An LLM functioning purely as an advisory tool. It summarizes text, synthesizes data, brainstorms solutions, and writes drafts, but **cannot take state-changing actions**.
* **The Agent Role:** An LLM equipped with tools, API access, or execution permissions (e.g., sending emails, modifying grades, changing schedule records, executing scripts). The moment an AI has write permissions or external access, its threat model fundamentally changes.

### 2. Guardrails and Review Checkpoints
Throughout the Westbrook High scenario, situations arise where characters are tempted to give the model direct execution privileges to save time:
* **Unchecked Delegation:** Allowing an autonomous agent to take immediate action without confirmation creates catastrophic blind spots when hallucinations or poisoned inputs occur.
* **Human-in-the-Loop (HITL):** Enforcing explicit human approval gates for high-impact actions (modifying database entries, communicating on behalf of staff, deleting logs).
* **Least Privilege:** Limiting the tools exposed to an agent so it cannot access resources outside its strict operational scope.

Navigating the story safely comes down to choosing options that **treat the AI as an assistant by default**, requiring human oversight and authorization whenever the system attempts to act as an agent with external side effects.

---

## Flag

```text
academy{4551574n7_0r_463n7_........}
