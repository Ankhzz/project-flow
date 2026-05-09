[🇬🇧 English](README.md) | [🇪🇸 Español](README.es.md)

---

# Project-Flow v1.0

**Structured workflow for AI coding agents.**

> **Important:** Project-Flow does **NOT** replace your AI agent. It only provides the workflow and execution rules. You still need an AI agent (OpenCode, Claude Code, Cursor, etc.) to use this protocol.

---

## 🚀 Quick Start

### 1. Get the files

```bash
git clone https://github.com/Ankhzz/project-flow.git
```

### 2. Where to put them

Inside your project folder:

```
my-project/
└── project-flow/ ← cloned here
```

### 3. (Optional) Add skills for your tech stack

Skills are **optional** markdown files for specific technologies (Web3, wallets, etc.).

**They are NOT part of Project-Flow** - you create or download them separately.

```
my-project/
├── skills/
│   ├── solidity-base.md ← for smart contracts
│   └── wallet-auth.md ← for wallet connections
└── project-flow/
```

> 💡 **Tip:** If you're working with Web3, contracts, wallets, etc., install your skills **BEFORE** starting the project. The agent will detect them automatically during execution.

### 4. Start your AI agent

Open your preferred agent:

- OpenCode
- Claude Code
- Cursor (with custom commands)
- Any AI coding agent with custom command support

### 5. Activate Project-Flow

```bash
/project "create a web3 dashboard with wallet login" --mode safe
```

**That's it.** Project-Flow will guide the agent to:

1. Ask about your idea
2. Create a plan
3. Build step by step
4. Verify everything works

---

## 🎯 Simple Flow

```
1. Download Project-Flow
2. (Optional) Add your skills
3. Open your AI agent
4. Run: /project "your idea" --mode safe
5. Agent builds your project
```

No chaos. No random code. Just structured building.

---

## 🟢 SAFE vs 🔴 AUTOPILOT

### SAFE MODE - "Ask me before important decisions"

**Best for:**

- Complex projects you want to control
- When you're not sure what you want
- Learning the protocol
- Security-sensitive projects

**What it does:**

- ✅ Asks clarifying questions
- ✅ Shows options before deciding
- ✅ Waits for your confirmation

**Example:**

```
User: /project "e-commerce site" --mode safe
Agent: Got it. To clarify:
1. What stack? (React/Vue/Next.js)
2. Payment integration? (Stripe/PayPal)
3. Database requirements?
```

### AUTOPILOT MODE - "Just build it"

**Best for:**

- Standard projects with known patterns
- When you trust reasonable defaults
- Speed is priority

**What it does:**

- ✅ Uses smart defaults (Node.js, SQLite, etc.)
- ✅ Makes assumptions based on context
- ✅ Continues without stopping

**Important:** AUTOPILOT still uses PLAN → TASKS → EXECUTION. The difference is it takes reasonable decisions automatically without asking you each step.

**Example:**

```
User: /project "cli todo app" --mode autopilot
Agent: Understood. Using defaults:
- Stack: Node.js + TypeScript
- Storage: SQLite local
- UI: Terminal (TUI)
Building...
```

### Quick Comparison

| You want... | SAFE | AUTOPILOT |
|-------------|------|-----------|
| To be asked first | ✅ Yes | ❌ No |
| Speed over control | ❌ No | ✅ Yes |
| Standard project | ⚠️ Overkill | ✅ Perfect |
| Complex/custom project | ✅ Perfect | ⚠️ Risky |

---

## 🧠 About Skills

### What are skills?

Skills are **optional** markdown files that guide the AI on specific technologies.

**They are NOT part of Project-Flow** - they're separate files you create or download.

### Where do they go?

```
my-project/
├── skills/
│   ├── solidity-base.md
│   └── wallet-auth.md
└── project-flow/
```

### How to use them?

1. **Let agent discover:** Agent finds relevant skills automatically
2. **Specify manually:**
   ```bash
   /project "web3 dashboard" --mode safe
   # Uses: skills/solidity-base.md, skills/wallet-auth.md
   ```

### Are skills required?

**No.** But they help:

- Keep technical decisions consistent
- Speed up planning
- Ensure agent knows your stack
- Maintain team consistency

---

## 📁 Project Structure

After setup:

```
my-project/
├── project-flow/ ← This protocol
│   ├── README.md
│   ├── FLOW.md
│   └── ...
├── skills/ ← Your optional skills
│   └── solidity-base.md
└── src/ ← Your actual code
```

**Important:** `project-flow/` folder must exist for the protocol to work.

---

## 🧠 How It Works (Technical)

Project-Flow enforces a strict execution loop:

```
CONTEXT → CLARIFY → PLAN → TASKS → EXECUTION LOOP → DONE
```

**Key rules:**

- No code until tasks defined
- One task at a time
- Verify before marking done
- Auto-recover on errors

See [FLOW.md](./FLOW.md) for full technical details.

---

## 🔒 System Rules

These cannot be skipped:

1. **No code before TASKS** - Define tasks first
2. **TASK structure required** - Specific JSON format
3. **TASK LOCK** - Tasks don't change once created
4. **Single task execution** - One at a time
5. **Mandatory verification** - Verify before done
6. **Auto-recovery** - Return to plan on errors

---

## 📚 Documentation

| File | What it's for |
|------|---------------|
| **README.md** | This guide |
| **FLOW.md** | Core protocol rules |
| **EXECUTION.md** | Output limits, servers |
| **commands.md** | Command syntax |
| **state.json** | State template |
| **memory.json** | Memory structure |
| **decisions.md** | Decision log |
| **log.md** | Execution log |

---

## 🛠️ Compatible Agents

Works with agents supporting custom commands:

- ✅ OpenCode
- ✅ Claude Code
- ✅ Cursor (configured)
- ✅ Custom AI coding agents

**Requirement:** Must support slash-command style activation.

---

## 🔒 License

MIT - See LICENSE file
