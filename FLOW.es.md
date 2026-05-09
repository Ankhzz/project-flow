[🇬🇧 English](FLOW.md) | [🇪🇸 Español](FLOW.es.md)

---

# FLOW - Protocolo de Ejecución Central

## 🔁 Flujo Central (INMUTABLE)

```
CONTEXT → CLARIFY → PLAN → TASKS → EXECUTION LOOP → DONE
```

> **FLOW LOCK:** Saltar fases es **INVÁLIDO**. El orden es **ESTRICTO** e **INMUTABLE**.

---

## 📍 Fases Detalladas

### 1. CONTEXT

Recopilación inicial del contexto del proyecto:
- Idea principal del usuario
- Requisitos explícitos
- Restricciones conocidas
- Stack tecnológico (si aplica)

**Estado:** `stage: "context"`

---

### 2. CLARIFY

Proceso de clarificación según el modo:

**SAFE MODE:**
- Realiza preguntas cuando hay ambigüedad
- Propone opciones en lugar de asumir
- Solicita confirmación antes de decisiones críticas
- Prioriza corrección sobre velocidad

**AUTOPILOT MODE:**
- Minimiza preguntas
- Usa defaults razonables cuando es necesario
- Continúa ejecución sin detenerse entre fases
- Solo se detiene en bloqueos técnicos o contradicciones

**Estado:** `stage: "clarify"`

---

### 3. PLAN

Diseño del plan estructurado:
- Arquitectura propuesta
- Desglose en componentes
- Dependencias identificadas
- Estrategia de implementación

**Regla:** Cualquier modificación estructural requiere volver a esta fase.

**Estado:** `stage: "plan"`

---

### 4. TASKS

Creación de la lista de tareas ejecutables:

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

**TASK LOCK:** Una vez creados, los TASKS son **INMUTABLES**. Cualquier modificación requiere volver a **PLAN phase**.

**Estado:** `stage: "tasks"`

---

### 5. EXECUTION LOOP

**Motor de Ejecución (CORE ENGINE):**

Para cada task:
1. Seleccionar el próximo task con status `"pending"`
2. Marcar como `"doing"`
3. Ejecutar completamente
4. Verificar resultado
5. Si éxito: marcar `"done"`, actualizar memoria/estado
6. Si fallo: intentar fix inmediato
7. Si problema estructural: volver a **PLAN/CLARIFY**

**Reglas de ejecución:**
- Solo UN task en `"doing"` a la vez
- No se permite ejecución paralela
- Verificación obligatoria antes de `"done"`

**Estado:** `stage: "execution"`

---

### 6. DONE

Completado cuando:
- Todos los tasks están `"done"`
- No hay dependencias faltantes
- El resultado coincide con la intención original

**Estado:** `stage: "done"`
**Progreso:** `progress: 100`

---

## 🔄 Auto-Recuperación

**AUTO-RECOVERY RULE:**

Si se detecta inconsistencia o conflicto estructural:
1. Detener ejecución inmediatamente
2. Volver a **PLAN phase**
3. Re-evaluar estructura
4. Actualizar TASKS si es necesario
5. Continuar desde TASKS phase

---

## 📊 Estados Válidos

| Stage | Descripción |
|-------|-------------|
| `context` | Recopilación inicial |
| `clarify` | Preguntas y clarificación |
| `plan` | Diseño de arquitectura |
| `tasks` | Creación de tasks |
| `execution` | Ejecución del loop |
| `done` | Completado |

---

## 🚫 Restricciones (HARD CONSTRAINTS)

1. **HARD GATE BEFORE CODE** - No hay código hasta que TASKS exista y sea válido
2. **TASK STRUCTURE REQUIREMENT** - Formato JSON específico requerido
3. **TASK LOCK** - Inmutabilidad de TASKS después de creación
4. **SINGLE TASK EXECUTION** - Un task a la vez
5. **TASK VERIFICATION RULE** - Verificación obligatoria para "done"
6. **EXECUTION LOOP** - Seguir el loop estrictamente
7. **FLOW LOCK** - No saltar fases
8. **AUTO-RECOVERY** - Volver a PLAN ante inconsistencias
