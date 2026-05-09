[🇬🇧 English](README.md) | [🇪🇸 Español](README.es.md)

---

# Project-Flow v1.0

Protocolo de ejecución universal para agentes de IA de programación.

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

## ⚙️ Bucle de Ejecución y Reglas de Seguridad

Cada tarea debe seguir este estricto bucle de ejecución:

1. Seleccionar la próxima tarea "pending"
2. Marcar la tarea como "doing"
3. Ejecutar la tarea completamente
4. Verificar el resultado contra la intención
5. Si es válido → marcar como "done"
6. Si es inválido → corregir inmediatamente o volver a PLAN phase

**Reglas:**
- Solo una tarea puede estar en "doing" a la vez
- Ninguna tarea puede marcarse "done" sin verificación
- Las tareas fallidas no pueden omitirse

---

## ✅ Criterios de Finalización de Tareas

**Terminar inmediatamente cuando:**
- El servidor responda correctamente (HTTP 200/OK)
- La funcionalidad principal funcione
- Las validaciones mínimas pasen

**NO continuar** con verificaciones innecesarias después de completar el build.

---

## 📏 Límites de Output

**Nunca:**
- Listar directorios completos recursivamente
- Mostrar contenido de node_modules
- Imprimir más de 200 líneas seguidas
- Usar `Get-ChildItem -Recurse` sin exclusiones

**Al listar archivos:**
- Mostrar solo archivos relevantes del proyecto
- Excluir: `node_modules/`, `.git/`, `dist/`, `build/`

---

## 🖥️ Procesos en Background

**Todos los dev servers DEBEN ejecutarse detached/background:**
1. Iniciar servidor en background
2. Guardar PID o puerto
3. Continuar con otras tareas
4. Nunca esperar indefinidamente logs en vivo
5. Cleanup al completar tarea

---

## ⏱️ Timeout & Auto-Completado

**Si no hay cambios reales por 5 minutos:**
1. Realizar validación final
2. Resumir estado
3. Finalizar tarea limpiamente

---

## 🔇 Modo Conciso (Por Defecto)

**El comportamiento por defecto prioriza:**
- Outputs cortos
- Resúmenes accionables
- Mínimo spam de terminal

---

## 🧠 Manejo de Inconsistencias

Si ocurre algo de lo siguiente:
- Dependencias faltantes
- Requisitos poco claros durante la ejecución
- Resultados conflictivos entre tareas
- Errores inesperados

**El agente DEBE:**
→ Volver a PLAN phase  
→ Ajustar o regenerar TASKS si es necesario  
→ Continuar solo después de la corrección

---

## 🔒 Restricciones del Sistema (Reglas Duras)

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
| `README.md` | Documentación principal |
| `FLOW.md` | Flujo completo inmutable |
| `EXECUTION.md` | Directrices de ejecución y límites |
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
- Prioriza velocidad y estabilidad sobre logging excesivo

---

## 🔒 Estado Final

Project-Flow v1.0 es un protocolo de ejecución cerrado y consistente. No está diseñado para evolucionar durante su uso.
