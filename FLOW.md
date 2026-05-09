[🇬🇧 English](FLOW.md) | [🇪🇸 Español](FLOW.es.md)

---

# FLOW - Core Execution Protocol

## 🔁 Core Flow (IMMUTABLE)

```
CONTEXT → CLARIFY → PLAN → TASKS → EXECUTION LOOP → DONE
```

> **FLOW LOCK:** Skipping phases is **INVALID**. The order is **STRICT** and **IMMUTABLE**.

---

## 📍 Detailed Phases

### 1. CONTEXT

Initial project context collection:
- Main user idea
- Explicit requirements
- Known constraints
- Technology stack (if applicable)

**State:** `stage: "context"`

---

### 2. CLARIFY

Clarification process by mode:

**SAFE MODE:**
- Asks questions when there is ambiguity
- Proposes options instead of assuming
- Requests confirmation before critical decisions
- Prioritizes correctness over speed

**AUTOPILOT MODE:**
- Minimizes questions
- Uses reasonable defaults when necessary
- Continues execution without stopping between phases
- Only stops on technical blockers or contradictions

**State:** `stage: "clarify"`

---

### 3. PLAN

Structured plan design:
- Proposed architecture
- Component breakdown
- Identified dependencies
- Implementation strategy

**Rule:** Any structural modification requires returning to this phase.

**State:** `stage: "plan"`

---

### 4. TASKS

Creation of executable task list:

```json
{
  "tasks": [
    {
      "id": 1,
      "title": "setup project",
      "status": "pending",
      "verified": false
    }
  ]
}
```

**TASK LOCK:** Once created, TASKS are **IMMUTABLE**. Any modification requires returning to **PLAN phase**.

**State:** `stage: "tasks"`

---

### 5. EXECUTION LOOP

**Core Engine:**

For each task:
1. Select next task with status `"pending"`
2. Mark as `"doing"`
3. Execute completely
4. Verify result
5. If success: mark `"done"`, update memory/state
6. If failure: attempt immediate fix
7. If structural problem: return to **PLAN/CLARIFY**

**Execution Rules:**
- Only ONE task in `"doing"` at a time
- Parallel execution not allowed
- Mandatory verification before `"done"`

**State:** `stage: "execution"`

---

### 6. DONE

Completed when:
- All tasks are `"done"`
- No missing dependencies
- Result matches original intent

**State:** `stage: "done"`
**Progress:** `progress: 100`

---

## 🔄 Auto-Recovery

**AUTO-RECOVERY RULE:**

If inconsistency or structural conflict is detected:
1. Stop execution immediately
2. Return to **PLAN phase**
3. Re-evaluate structure
4. Update TASKS if necessary
5. Continue from TASKS phase

---

## 📊 Valid States

| Stage | Description |
|-------|-------------|
| `context` | Initial collection |
| `clarify` | Questions and clarification |
| `plan` | Architecture design |
| `tasks` | Task creation |
| `execution` | Loop execution |
| `done` | Completed |

---

## 🚫 Hard Constraints

1. **HARD GATE BEFORE CODE** - No code until TASKS exists and is valid
2. **TASK STRUCTURE REQUIREMENT** - Specific JSON format required
3. **TASK LOCK** - TASKS immutability after creation
4. **SINGLE TASK EXECUTION** - One task at a time
5. **TASK VERIFICATION RULE** - Mandatory verification for "done"
6. **EXECUTION LOOP** - Follow loop strictly
7. **FLOW LOCK** - Do not skip phases
8. **AUTO-RECOVERY** - Return to PLAN on inconsistencies
