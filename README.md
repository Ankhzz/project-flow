# Project-Flow v1.0

**Protocolo de ejecución universal para agentes de IA de programación**

---

## 🚀 Activación

```bash
/project "<idea>" --mode <safe|autopilot>
```

### Ejemplo

```bash
/project "offline notes app" --mode autopilot
```

---

## ⚙️ Modos de Ejecución

| Modo | Descripción |
|------|-------------|
| **SAFE** | Realiza preguntas de clarificación, solicita confirmación antes de decisiones críticas |
| **AUTOPILOT** | Ejecución continua con mínimos cuestionamientos, usa defaults razonables |

---

## 📋 Flujo Central

```
CONTEXT → CLARIFY → PLAN → TASKS → EXECUTION LOOP → DONE
```

> **IMPORTANTE:** Este orden es **ESTRICTO** y **NO PUEDE** ser omitido.

---

## 📜 Reglas Principales

1. **No hay código sin TASKS** - Los tasks deben existir y ser válidos antes de codificar
2. **Estructura de TASKS requerida** - Formato JSON específico con id, title, status, verified
3. **TASK LOCK** - Una vez creados, los TASKS son inmutables
4. **Ejecución de a un TASK** - Solo un task en estado "doing" a la vez
5. **Verificación obligatoria** - Un task solo se marca "done" si está verificado
6. **Auto-recuperación** - Si hay inconsistencia, volver a PLAN phase

---

## 📁 Archivos del Sistema

| Archivo | Descripción |
|---------|-------------|
| `FLOW.md` | Flujo completo inmutable |
| `commands.md` | Definición de comandos y modos |
| `state.json` | Estado base del proyecto |
| `memory.json` | Memoria del agente |
| `decisions.md` | Log de decisiones |
| `log.md` | Log de ejecución |

---

## 🧠 Comportamiento del Sistema

- Convierte idea → plan estructurado → tasks ejecutables
- Fuerza ejecución paso a paso
- Previene codificar sin planificar
- Asegura verificación antes de completar
- Mantiene estado persistente del proyecto

---

## 🔒 Estado Final

Project-Flow v1.0 es un protocolo de ejecución cerrado y consistente. No está diseñado para evolucionar durante su uso.
