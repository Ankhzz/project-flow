# Example Flow

Ejemplo completo de ejecución de Project-Flow.

---

## Activación

```bash
/project "offline notes app" --mode autopilot
```

---

## 1. CONTEXT

**Input del usuario:**
> "offline notes app"

**Interpretación inicial:**
- Aplicación de notas
- Sin conexión (offline-first)
- Persistencia local

**Estado:**
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

**Modo AUTOPILOT - Defaults aplicados:**
- Stack: Node.js + TypeScript
- Persistencia: SQLite local
- UI: Terminal (TUI)

**Sin preguntas al usuario** (modo autopilot)

**Estado:**
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

**Arquitectura propuesta:**
```
notes-app/
├── src/
│   ├── index.ts
│   ├── notes.ts
│   └── storage.ts
├── package.json
└── tsconfig.json
```

**Componentes:**
1. CLI interface (comandos: add, list, delete)
2. Storage layer (SQLite)
3. Note entity (title, content, timestamp)

**Estado:**
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

**Lista de tareas creada:**

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

**Estado:**
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

**Transición:** `pending` → `doing`

**Acciones:**
```bash
mkdir notes-app
npm init -y
npm install typescript sqlite3 @types/node --save-dev
npx tsc --init
```

**Verificación:**
- ✅ package.json existe
- ✅ tsconfig.json existe
- ✅ node_modules instalado

**Resultado:** `done`

---

### Task 2: create storage layer

**Transición:** `pending` → `doing`

**Acciones:**
- Crear `src/storage.ts`
- Implementar funciones: init, save, findAll, delete
- Configurar SQLite

**Verificación:**
- ✅ storage.ts existe
- ✅ Funciones exportadas
- ✅ Tests de conexión OK

**Resultado:** `done`

---

### Task 3: implement CLI commands

**Transición:** `pending` → `doing`

**Acciones:**
- Crear `src/index.ts`
- Implementar comandos: add, list, delete
- Parsear argumentos CLI

**Verificación:**
- ✅ CLI funcional
- ✅ Todos los comandos responden
- ✅ Help message disponible

**Resultado:** `done`

---

### Task 4: test all commands

**Transición:** `pending` → `doing`

**Acciones:**
- Probar: `notes add "titulo" "contenido"`
- Probar: `notes list`
- Probar: `notes delete <id>`

**Verificación:**
- ✅ Add crea nota correctamente
- ✅ List muestra todas las notas
- ✅ Delete elimina nota

**Resultado:** `done`

---

## 6. DONE

**Estado final:**
```json
{
  "stage": "done",
  "mode": "autopilot",
  "progress": 100,
  "current_task": null
}
```

**Resumen:**
- ✅ 4 tasks completados
- ✅ 0 errors
- ✅ 0 pending questions
- ✅ Aplicación funcional

---

## memory.json Final

```json
{
  "stack": "Node.js + TypeScript + SQLite",
  "decisions": [
    "Usar SQLite para persistencia local",
    "CLI TUI en lugar de interfaz gráfica",
    "TypeScript para type safety"
  ],
  "open_questions": [],
  "constraints": ["offline-first", "persistencia local"]
}
```
