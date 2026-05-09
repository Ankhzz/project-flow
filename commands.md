[🇬🇧 English](commands.md) | [🇪🇸 Español](commands.es.md)

---

# Commands

## Activation

```bash
project: "<idea>" --mode <safe|autopilot>
```

### Parameters

| Parameter | Description | Values |
|-----------|-------------|--------|
| `<idea>` | Natural description of the idea/project | string |
| `--mode` | Execution mode | `safe` \| `autopilot` |

---

## Execution Modes

### 🟢 SAFE MODE

**Behavior:**
- Asks clarifying questions when there is ambiguity
- Proposes options instead of making assumptions
- Requests confirmation before critical decisions
- Prioritizes correctness over speed

**Use cases:**
- Complex projects with multiple possible interpretations
- Users who want full control over decisions
- When requirements are not completely clear

**Example:**
```bash
project: "online store with payments" --mode safe
```

---

### 🔴 AUTOPILOT MODE

**Behavior:**
- Minimizes questions to the user
- Uses reasonable defaults when necessary
- Continues execution without stopping between phases
- Only stops on technical blockers or contradictions

**Use cases:**
- Standard projects with known patterns
- Experienced users who trust defaults
- When speed is a priority

**Example:**
```bash
project: "notes cli" --mode autopilot
```

---

## Comparison

| Characteristic | SAFE MODE | AUTOPILOT MODE |
|----------------|-----------|----------------|
| Questions | Frequent | Minimal |
| Confirmations | Required | Omitted |
| Speed | Moderate | Maximum |
| Control | High | Low |
| Ideal for | Complex projects | Standard projects |

---

## System Response

When activating the command, the system responds with:

1. **Mode recognition** selected
2. **Entry to CONTEXT phase**
3. **First question/action** according to mode

**Example SAFE MODE:**
```
🟢 SAFE MODE activated
📍 CONTEXT phase started

Understood: "online store with payments"

To clarify the context, I need to know:
1. What technology stack do you prefer?
2. Do you require a specific database?
3. Any security requirements?
```

**Example AUTOPILOT MODE:**
```
🔴 AUTOPILOT MODE activated
📍 CONTEXT phase started

Understood: "notes cli"
Stack: Node.js (default)
Persistence: Local file (default)

Continuing to CLARIFY phase...
```
