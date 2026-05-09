# Project-Flow

Project-Flow is a lightweight, static protocol for AI coding agents. It defines a strict and universal workflow that any agent can follow to turn ideas into structured software without ambiguity or chaos.

---

## 🧠 What this is

This is **NOT** an application.  
This is **NOT** a framework.  
This is a **behavioral execution protocol** for AI agents. It standardizes how agents think, plan, and build software.

---

## ⚙️ Core Workflow

All agents using Project-Flow **MUST** follow this immutable flow:

```
CONTEXT → CLARIFY → PLAN → TASKS → EXECUTION LOOP → DONE
```

No step can be skipped.

---

## 🚀 Activation

To start a project inside any compatible AI coding agent:

```bash
/project "<idea>" --mode <safe|autopilot>
```

**Example:**

```bash
/project "offline notes app" --mode autopilot
```

---

## 🟢 Modes

### SAFE MODE
- Asks clarifying questions when needed
- Requests confirmation before key decisions
- Prioritizes correctness and user control

### AUTOPILOT MODE
- Minimizes questions
- Uses reasonable defaults when needed
- Executes continuously through all phases
- Only stops on real technical blockers

---

## 📦 Core Principle

- Tasks must always be defined before any code is written
- Execution must be step-by-step (no parallel task execution)
- Every task must be verified before completion
- If inconsistency is found, the system returns to PLAN

---

## 📁 Repository Structure

| File | Description |
|------|-------------|
| `FLOW.md` | Core immutable execution flow |
| `commands.md` | Activation + mode definitions |
| `state.json` | Runtime state template |
| `memory.json` | Context memory template |
| `decisions.md` | Architectural decisions log |
| `log.md` | Execution tracking log |
| `examples/` | Example flows |

---

## 🧠 Philosophy

Project-Flow does not replace AI agents. It constrains them into a deterministic engineering process so that outputs become predictable, structured, and reproducible across any environment.

---

## 🔒 License

MIT
