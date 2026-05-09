[🇬🇧 English](README.md) | [🇪🇸 Español](README.es.md)

---

# Project-Flow v1.0

Universal execution protocol for AI coding agents.

---

## 🚀 Activation

```bash
/project "<idea>" --mode <safe|autopilot>
```

### Example

```bash
/project "offline notes app" --mode autopilot
```

---

## ⚙️ Execution Modes

| Mode | Description |
|------|-------------|
| **SAFE** | Asks clarifying questions, requests confirmation before critical decisions |
| **AUTOPILOT** | Continuous execution with minimal questions, uses reasonable defaults |

---

## 📋 Core Flow

```
CONTEXT → CLARIFY → PLAN → TASKS → EXECUTION LOOP → DONE
```

> **IMPORTANT:** This order is **STRICT** and **CANNOT** be skipped.

---

## ⚙️ Execution Loop & Safety Rules

Each task must follow this strict execution loop:

1. Select next "pending" task
2. Mark task as "doing"
3. Execute task fully
4. Verify output against intent
5. If valid → mark as "done"
6. If invalid → fix immediately or return to PLAN phase

**Rules:**
- Only one task can be "doing" at any time
- No task can be marked "done" without verification
- Failed tasks cannot be skipped

---

## ✅ Task Completion Criteria

**Terminate immediately when:**
- Server responds correctly (HTTP 200/OK)
- Core functionality works
- Minimum validations pass

**Do NOT continue** unnecessary verifications after successful build.

---

## 📏 Output Limits

**Never:**
- List complete directories recursively
- Show node_modules content
- Print more than 200 consecutive lines
- Use `Get-ChildItem -Recurse` without exclusions

**When listing files:**
- Show only relevant project files
- Exclude: `node_modules/`, `.git/`, `dist/`, `build/`

---

## 🖥️ Background Processes

**All dev servers MUST run detached/background:**
1. Start server in background
2. Save PID or port
3. Continue with other tasks
4. Never wait indefinitely for live logs
5. Cleanup on task completion

---

## ⏱️ Timeout & Auto-Completion

**If no real changes for 5 minutes:**
1. Perform final validation
2. Summarize state
3. Terminate task cleanly

---

## 🔇 Concise Mode (Default)

**Default behavior prioritizes:**
- Short outputs
- Actionable summaries
- Minimal terminal spam

---

## 🧠 Inconsistency Handling

If any of the following occurs:
- Missing dependencies
- Unclear requirements during execution
- Conflicting results between tasks
- Unexpected errors

**The agent MUST:**
→ Return to PLAN phase  
→ Adjust or regenerate TASKS if needed  
→ Continue only after correction

---

## 🔒 System Constraints (Hard Rules)

1. **No code before TASKS exist** - Tasks must exist and be valid before coding
2. **TASK structure required** - Specific JSON format with id, title, status, verified
3. **TASK LOCK** - Once created, TASKS are immutable
4. **Single task execution** - Only one task in "doing" status at a time
5. **Mandatory verification** - A task is only marked "done" if verified
6. **Auto-recovery** - If inconsistency, return to PLAN phase

---

## 📁 System Files

| File | Description |
|------|-------------|
| `README.md` | Main documentation |
| `FLOW.md` | Complete immutable flow |
| `EXECUTION.md` | Execution guidelines & limits |
| `commands.md` | Command and mode definitions |
| `state.json` | Base project state |
| `memory.json` | Agent memory |
| `decisions.md` | Decisions log |
| `log.md` | Execution log |

---

## 🧠 System Behavior

- Converts idea → structured plan → executable tasks
- Forces step-by-step execution
- Prevents coding without planning
- Ensures verification before completion
- Maintains persistent project state
- Prioritizes speed and stability over excessive logging

---

## 🔒 Final State

Project-Flow v1.0 is a closed and consistent execution protocol. It is not designed to evolve during use.
