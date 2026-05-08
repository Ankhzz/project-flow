# Commands

## Activación

```bash
/project "<idea>" --mode <safe|autopilot>
```

### Parámetros

| Parámetro | Descripción | Valores |
|-----------|-------------|---------|
| `<idea>` | Descripción natural de la idea/proyecto | string |
| `--mode` | Modo de ejecución | `safe` \| `autopilot` |

---

## Modos de Ejecución

### 🟢 SAFE MODE

**Comportamiento:**
- Realiza preguntas de clarificación cuando hay ambigüedad
- Propone opciones en lugar de hacer suposiciones
- Solicita confirmación antes de decisiones críticas
- Prioriza la corrección sobre la velocidad

**Casos de uso:**
- Proyectos complejos con múltiples interpretaciones posibles
- Usuarios que quieren control total sobre las decisiones
- Cuando los requisitos no están completamente claros

**Ejemplo:**
```bash
/project "tienda online con pagos" --mode safe
```

---

### 🔴 AUTOPILOT MODE

**Comportamiento:**
- Minimiza las preguntas al usuario
- Usa defaults razonables cuando es necesario
- Continúa la ejecución sin detenerse entre fases
- Solo se detiene en bloqueos técnicos o contradicciones

**Casos de uso:**
- Proyectos estándar con patrones conocidos
- Usuarios experimentados que confían en los defaults
- Cuando la velocidad es prioritaria

**Ejemplo:**
```bash
/project "cli para notas" --mode autopilot
```

---

## Comparación

| Característica | SAFE MODE | AUTOPILOT MODE |
|----------------|-----------|----------------|
| Preguntas | Frecuentes | Mínimas |
| Confirmaciones | Requeridas | Omitidas |
| Velocidad | Moderada | Máxima |
| Control | Alto | Bajo |
| Ideal para | Proyectos complejos | Proyectos estándar |

---

## Respuesta del Sistema

Al activar el comando, el sistema responde con:

1. **Reconocimiento del modo** seleccionado
2. **Entrada en CONTEXT phase**
3. **Primera pregunta/acción** según el modo

**Ejemplo SAFE MODE:**
```
🟢 SAFE MODE activado
📍 CONTEXT phase iniciada

Entendido: "tienda online con pagos"

Para clarificar el contexto, necesito saber:
1. ¿Qué stack tecnológico prefieres?
2. ¿Requiere base de datos específica?
3. ¿Algún requisito de seguridad?
```

**Ejemplo AUTOPILOT MODE:**
```
🔴 AUTOPILOT MODE activado
📍 CONTEXT phase iniciada

Entendido: "cli para notas"
Stack: Node.js (default)
Persistencia: Local file (default)

Continuando a CLARIFY phase...
```
