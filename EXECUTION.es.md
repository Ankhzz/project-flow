[🇬🇧 English](EXECUTION.md) | [🇪🇸 Español](EXECUTION.es.md)

---

# Directrices de Ejecución

## 🎯 Criterios de Finalización de Tareas

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
- Excluir:
  - `node_modules/`
  - `.git/`
  - `dist/`
  - `build/`

**Ejemplo (PowerShell):**
```powershell
# ✅ Bueno: Listado limitado y filtrado
Get-ChildItem -Path "." -Exclude node_modules,.git,dist,build |
  Where-Object { $_.Name -match "\.(ts|js|json|md)$" } |
  Select-Object -First 50 Name

# ❌ Malo: Listado recursivo sin límites
Get-ChildItem -Recurse  # Nunca hacer esto
```

---

## 🖥️ Procesos en Background

**Todos los dev servers DEBEN ejecutarse detached/background:**

1. Iniciar servidor en background
2. Guardar PID o puerto
3. Continuar con otras tareas
4. Nunca esperar indefinidamente logs en vivo

**Ejemplo (Node.js):**
```bash
# ✅ Bueno: Proceso detached
npm start &
SERVER_PID=$!

# Guardar PID para cleanup
echo $SERVER_PID > .server.pid

# Continuar trabajando...

# Cleanup al salir
kill $SERVER_PID
```

**Ejemplo (PowerShell):**
```powershell
# ✅ Bueno: Iniciar detached
Start-Process npm -ArgumentList "start" -WindowStyle Hidden -PassThru |
  ForEach-Object { $_.Id } |
  Out-File .server.pid

# Continuar trabajando...

# Cleanup al salir
Get-Content .server.pid | Stop-Process
```

---

## ⏱️ Timeout & Auto-Completado

**Si no hay cambios reales por X minutos:**
1. Realizar validación final
2. Resumir estado
3. Finalizar tarea limpiamente

**Timeout por defecto:** 5 minutos sin progreso significativo

**Flujo de ejemplo:**
```
[10:00] Tarea iniciada
[10:02] Último cambio significativo
[10:03] No se detectan cambios
[10:05] Timeout activado → validación final
[10:06] Resumen escrito → tarea completada
```

---

## 🔇 Modo Conciso (Por Defecto)

**El comportamiento por defecto prioriza:**
- Outputs cortos
- Resúmenes accionables
- Mínimo spam de terminal

**Ejemplo:**
```
✅ Build exitoso
   - 3 archivos compilados
   - 0 errores
   - Server: http://localhost:3000

Próximos pasos:
- Run: npm test
- Deploy: npm run build
```

**No:**
```
[LOG] Compilando...
[LOG] Procesando archivo 1 de 150...
[LOG] Procesando archivo 2 de 150...
... (148 líneas más)
[LOG] Compilación terminada
```

---

## 🧹 Ciclo de Vida de Servidores

**Cada vez que el agente inicia un servidor local:**

1. **Iniciar detached:**
   ```bash
   npm start &
   SERVER_PID=$!
   echo $SERVER_PID > .server.pid
   echo "3000" > .server.port
   ```

2. **Rastrear servidores activos:**
   ```json
   // .servers.json
   {
     "servers": [
       { "pid": 12345, "port": 3000, "task": "dev" }
     ]
   }
   ```

3. **Reutilizar si ya está corriendo:**
   ```bash
   if port-in-use 3000; then
     echo "Servidor ya está corriendo en puerto 3000"
   else
     start-server 3000
   fi
   ```

4. **Cleanup al completar tarea:**
   ```bash
   # Matar todos los procesos rastreados
   if [ -f .server.pid ]; then
     kill $(cat .server.pid)
     rm .server.pid
   fi

   # Liberar puertos
   release-port 3000
   ```

---

## 🛠️ Ejemplos Prácticos

### 1. Build & Verificación Rápida

```bash
# Build
npm run build

# Verificación rápida (no exhaustiva)
if [ -f dist/index.js ]; then
  echo "✅ Build exitoso"
else
  echo "❌ Build falló"
  exit 1
fi

# Stop - no es necesario listar todos los archivos dist
```

### 2. Servidor con Cleanup

```bash
# Iniciar servidor
npm start &
SERVER_PID=$!
echo $SERVER_PID > .server.pid

# Esperar readiness
wait-for-localhost 3000 --timeout 10

# Test
curl http://localhost:3000/health

# Cleanup
kill $SERVER_PID
rm .server.pid
```

### 3. Listado de Archivos (Seguro)

```powershell
# ✅ Bueno: Filtrado, limitado
Get-ChildItem -Path "src" -Include "*.ts","*.js" |
  Select-Object -First 20 -Property Name, Length

# Output:
# Name        Length
# ----        ------
# index.ts    1024
# utils.ts    512
```

---

## ✅ Checklist

Antes de marcar tarea como done:
- [ ] Funcionalidad principal verificada
- [ ] Output dentro de límites (< 200 líneas)
- [ ] Servidores en background (si corresponde)
- [ ] PIDs/puertos rastreados
- [ ] Sin directorios recursivos
- [ ] Resumen conciso y accionable
- [ ] Plan de cleanup definido

Después de completar tarea:
- [ ] Servidores temporales detenidos
- [ ] Puertos liberados
- [ ] Procesos huérfanos limpiados
- [ ] Archivo de estado actualizado
