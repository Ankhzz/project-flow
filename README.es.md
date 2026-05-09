[🇬🇧 English](README.md) | [🇪🇸 Español](README.es.md)

---

# Project-Flow v1.0

**Flujo estructurado para agentes de IA de programación.**

> **Importante:** Project-Flow **NO** reemplaza tu agente de IA. Solo proporciona el flujo de trabajo y las reglas de ejecución. Todavía necesitás un agente de IA (OpenCode, Claude Code, Cursor, etc.) para usar este protocolo.

---

## 🚀 Inicio Rápido

### 1. Obtener los archivos

```bash
git clone https://github.com/Ankhzz/project-flow.git
```

### 2. Dónde ponerlos

Dentro de tu carpeta de proyecto:

```
mi-proyecto/
└── project-flow/ ← clonado aquí
```

### 3. (Opcional) Agregar skills para tu stack

Skills son archivos markdown **opcionales** para tecnologías específicas (Web3, wallets, etc.).

**NO son parte de Project-Flow** - los creás o descargás por separado.

```
mi-proyecto/
├── skills/
│   ├── solidity-base.md ← para contratos inteligentes
│   └── wallet-auth.md ← para conexiones de wallet
└── project-flow/
```

> 💡 **Tip:** Si vas a usar Web3, contratos, wallets, etc., instalá tus skills **ANTES** de iniciar el proyecto. El agente los detectará automáticamente durante la ejecución.

### 4. Iniciar tu agente de IA

Abrí tu agente preferido:

- OpenCode
- Claude Code
- Cursor (con comandos personalizados)
- Cualquier agente de IA con soporte de comandos personalizados

### 5. Activar Project-Flow

```bash
/project "crear dashboard web3 con login de wallet" --mode safe
```

**Eso es todo.** Project-Flow guiará al agente para:

1. Preguntar sobre tu idea
2. Crear un plan
3. Construir paso a paso
4. Verificar que todo funcione

---

## 🎯 Flujo Simple

```
1. Descargás Project-Flow
2. (Opcional) Agregás tus skills
3. Abrís tu agente de IA
4. Ejecutás: /project "tu idea" --mode safe
5. El agente construye tu proyecto
```

Sin caos. Sin código aleatorio. Solo construcción estructurada.

---

## 🟢 MODO SAFE vs 🔴 MODO AUTOPILOT

### MODO SAFE - "Preguntame antes de decisiones importantes"

**Mejor para:**

- Proyectos complejos que querés controlar
- Cuando no estás seguro de lo que querés
- Aprender el protocolo
- Proyectos sensibles en seguridad

**Qué hace:**

- ✅ Realiza preguntas de clarificación
- ✅ Muestra opciones antes de decidir
- ✅ Espera tu confirmación

**Ejemplo:**

```
Usuario: /project "sitio de e-commerce" --mode safe
Agente: Entendido. Para clarificar:
1. ¿Qué stack? (React/Vue/Next.js)
2. ¿Integración de pagos? (Stripe/PayPal)
3. ¿Requisitos de base de datos?
```

### MODO AUTOPILOT - "Solo constrúyelo"

**Mejor para:**

- Proyectos estándar con patrones conocidos
- Cuando confiás en defaults razonables
- La velocidad es prioridad

**Qué hace:**

- ✅ Usa defaults inteligentes (Node.js, SQLite, etc.)
- ✅ Asume basado en contexto
- ✅ Continúa sin detenerse

**Importante:** AUTOPILOT sigue usando PLAN → TASKS → EXECUTION. La diferencia es que toma decisiones razonables automáticamente sin preguntarte cada paso.

**Ejemplo:**

```
Usuario: /project "app de todo en CLI" --mode autopilot
Agente: Entendido. Usando defaults:
- Stack: Node.js + TypeScript
- Almacenamiento: SQLite local
- UI: Terminal (TUI)
Construyendo...
```

### Comparación Rápida

| Querés... | SAFE | AUTOPILOT |
|-----------|------|-----------|
| Que te pregunte | ✅ Sí | ❌ No |
| Velocidad sobre control | ❌ No | ✅ Sí |
| Proyecto estándar | ⚠️ Excesivo | ✅ Perfecto |
| Proyecto complejo/personalizado | ✅ Perfecto | ⚠️ Arriesgado |

---

## 🧠 Sobre Skills

### ¿Qué son los skills?

Skills son archivos markdown **opcionales** que guían al agente en tecnologías específicas.

**NO son parte de Project-Flow** - son archivos separados que creás o descargás.

### ¿Dónde van?

```
mi-proyecto/
├── skills/
│   ├── solidity-base.md
│   └── wallet-auth.md
└── project-flow/
```

### ¿Cómo usarlos?

1. **Dejar que el agente descubra:** El agente encuentra skills relevantes automáticamente
2. **Especificar manualmente:**
   ```bash
   /project "dashboard web3" --mode safe
   # Usa: skills/solidity-base.md, skills/wallet-auth.md
   ```

### ¿Son requeridos los skills?

**No.** Pero ayudan a:

- Mantener consistencia en decisiones técnicas
- Acelerar la planificación
- Asegurar que el agente conozca tu stack
- Mantener consistencia en el equipo

---

## 📁 Estructura del Proyecto

Después de configurar:

```
mi-proyecto/
├── project-flow/ ← Este protocolo
│   ├── README.md
│   ├── FLOW.md
│   └── ...
├── skills/ ← Tus skills opcionales
│   └── solidity-base.md
└── src/ ← Tu código real
```

**Importante:** La carpeta `project-flow/` debe existir para que el protocolo funcione.

---

## 🧠 Cómo Funciona (Técnico)

Project-Flow aplica un bucle de ejecución estricto:

```
CONTEXT → CLARIFY → PLAN → TASKS → EXECUTION LOOP → DONE
```

**Reglas clave:**

- No hay código hasta definir tasks
- Una tarea a la vez
- Verificar antes de marcar done
- Auto-recuperación en errores

Ver [FLOW.md](./FLOW.md) para detalles técnicos completos.

---

## 🔒 Reglas del Sistema

No se pueden saltear:

1. **No hay código sin TASKS** - Definir tasks primero
2. **Estructura de TASKS requerida** - Formato JSON específico
3. **TASK LOCK** - Tasks no cambian una vez creados
4. **Ejecución de a un task** - De a uno por vez
5. **Verificación obligatoria** - Verificar antes de done
6. **Auto-recuperación** - Volver a plan en errores

---

## 📚 Documentación

| Archivo | Para qué sirve |
|---------|----------------|
| **README.md** | Esta guía |
| **FLOW.md** | Reglas del protocolo |
| **EXECUTION.md** | Límites de output, servidores |
| **commands.md** | Sintaxis de comandos |
| **state.json** | Plantilla de estado |
| **memory.json** | Estructura de memoria |
| **decisions.md** | Log de decisiones |
| **log.md** | Log de ejecución |

---

## 🛠️ Agentes Compatibles

Funciona con agentes que soportan comandos personalizados:

- ✅ OpenCode
- ✅ Claude Code
- ✅ Cursor (configurado)
- ✅ Agentes de IA personalizados

**Requisito:** Debe soportar activación estilo slash-command.

---

## 🔒 Licencia

MIT - Ver archivo LICENSE
