[🇬🇧 English](example-flow.md) | [🇪🇸 Español](example-flow.es.md)

---

# Example Flow

Complete example of Project-Flow execution.

---

## Activation

```bash
project: "offline notes app" --mode autopilot
```

---

## 1. CONTEXT

**User input:**
> "offline notes app"

**Initial interpretation:**
- Notes application
- Offline-first
- Local persistence

**State:**
```json
{
  "stage": "context",
  "mode": "autopilot",
  "progress": 10,
  "current_task": null
}
```

---

## 2. CLARIFY

**AUTOPILOT Mode - Defaults applied:**
- Stack: Node.js + TypeScript
- Persistence: SQLite local
- UI: Terminal (TUI)

**No questions to user** (autopilot mode)

**State:**
```json
{
  "stage": "clarify",
  "mode": "autopilot",
  "progress": 20,
  "current_task": null
}
```

---

## 3. PLAN

**Proposed architecture:**
```
notes-app/
├── src/
│   ├── index.ts
│   ├── notes.ts
│   └── storage.ts
├── package.json
└── tsconfig.json
```

**Components:**
1. CLI interface (commands: add, list, delete)
2. Storage layer (SQLite)
3. Note entity (title, content, timestamp)

**State:**
```json
{
  "stage": "plan",
  "mode": "autopilot",
  "progress": 30,
  "current_task": null
}
```

---

## 4. TASKS

**Task list created:**

```json
{
  "tasks": [
    {
      "id": 1,
      "title": "setup project",
      "status": "pending",
      "verified": false
    },
    {
      "id": 2,
      "title": "create storage layer",
      "status": "pending",
      "verified": false
    },
    {
      "id": 3,
      "title": "implement CLI commands",
      "status": "pending",
      "verified": false
    },
    {
      "id": 4,
      "title": "test all commands",
      "status": "pending",
      "verified": false
    }
  ]
}
```

**State:**
```json
{
  "stage": "tasks",
  "mode": "autopilot",
  "progress": 40,
  "current_task": null
}
```

---

## 5. EXECUTION LOOP

### Task 1: setup project

**Transition:** `pending` → `doing`

**Actions:**
```bash
mkdir notes-app
npm init -y
npm install typescript sqlite3 @types/node --save-dev
npx tsc --init
```

**Verification:**
- ✅ package.json exists
- ✅ tsconfig.json exists
- ✅ node_modules installed

**Result:** `done`

---

### Task 2: create storage layer

**Transition:** `pending` → `doing`

**Actions:**
- Create `src/storage.ts`
- Implement functions: init, save, findAll, delete
- Configure SQLite

**Verification:**
- ✅ storage.ts exists
- ✅ Functions exported
- ✅ Connection tests OK

**Result:** `done`

---

### Task 3: implement CLI commands

**Transition:** `pending` → `doing`

**Actions:**
- Create `src/index.ts`
- Implement commands: add, list, delete
- Parse CLI arguments

**Verification:**
- ✅ CLI functional
- ✅ All commands respond
- ✅ Help message available

**Result:** `done`

---

### Task 4: test all commands

**Transition:** `pending` → `doing`

**Actions:**
- Test: `notes add "title" "content"`
- Test: `notes list`
- Test: `notes delete <id>`

**Verification:**
- ✅ Add creates note correctly
- ✅ List shows all notes
- ✅ Delete removes note

**Result:** `done`

---

## 6. DONE

**Final state:**
```json
{
  "stage": "done",
  "mode": "autopilot",
  "progress": 100,
  "current_task": null
}
```

**Summary:**
- ✅ 4 tasks completed
- ✅ 0 errors
- ✅ 0 pending questions
- ✅ Functional application

---

## memory.json Final

```json
{
  "stack": "Node.js + TypeScript + SQLite",
  "decisions": [
    "Use SQLite for local persistence",
    "CLI TUI instead of graphical interface",
    "TypeScript for type safety"
  ],
  "open_questions": [],
  "constraints": ["offline-first", "local persistence"]
}
```
