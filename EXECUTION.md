[🇬🇧 English](EXECUTION.md) | [🇪🇸 Español](EXECUTION.es.md)

---

# Execution Guidelines

## 🎯 Task Completion Criteria

**Terminate immediately when:**
- Server responds correctly (HTTP 200/OK)
- Core functionality works
- Minimum validations pass

**Do NOT continue** unnecessary verifications after successful build.

---

## 📏 Output Limits

**Never:**
- List complete directories recursively
- Show node_modules content
- Print more than 200 consecutive lines
- Use `Get-ChildItem -Recurse` without exclusions

**When listing files:**
- Show only relevant project files
- Exclude:
  - `node_modules/`
  - `.git/`
  - `dist/`
  - `build/`

**Example (PowerShell):**
```powershell
# ✅ Good: Limited, filtered listing
Get-ChildItem -Path "." -Exclude node_modules,.git,dist,build | 
  Where-Object { $_.Name -match "\.(ts|js|json|md)$" } |
  Select-Object -First 50 Name

# ❌ Bad: Unbounded recursive listing
Get-ChildItem -Recurse  # Never do this
```

---

## 🖥️ Background Processes

**All dev servers MUST run detached/background:**

1. Start server in background
2. Save PID or port
3. Continue with other tasks
4. Never wait indefinitely for live logs

**Example (Node.js):**
```bash
# ✅ Good: Detached process
npm start &
SERVER_PID=$!

# Save PID for cleanup
echo $SERVER_PID > .server.pid

# Continue working...

# Cleanup on exit
kill $SERVER_PID
```

**Example (PowerShell):**
```powershell
# ✅ Good: Start detached
Start-Process npm -ArgumentList "start" -WindowStyle Hidden -PassThru |
  ForEach-Object { $_.Id } |
  Out-File .server.pid

# Continue working...

# Cleanup on exit
Get-Content .server.pid | Stop-Process
```

---

## ⏱️ Timeout & Auto-Completion

**If no real changes for X minutes:**
1. Perform final validation
2. Summarize state
3. Terminate task cleanly

**Default timeout:** 5 minutes without meaningful progress

**Example flow:**
```
[10:00] Task started
[10:02] Last meaningful change
[10:03] No changes detected
[10:05] Timeout triggered → final validation
[10:06] Summary written → task completed
```

---

## 🔇 Concise Mode (Default)

**Default behavior prioritizes:**
- Short outputs
- Actionable summaries
- Minimal terminal spam

**Example:**
```
✅ Build successful
   - 3 files compiled
   - 0 errors
   - Server: http://localhost:3000

Next steps:
- Run: npm test
- Deploy: npm run build
```

**Not:**
```
[LOG] Compiling...
[LOG] Processing file 1 of 150...
[LOG] Processing file 2 of 150...
... (148 more lines)
[LOG] Done compiling
```

---

## 🧹 Server Lifecycle Management

**Every time agent starts a local server:**

1. **Start detached:**
   ```bash
   npm start &
   SERVER_PID=$!
   echo $SERVER_PID > .server.pid
   echo "3000" > .server.port
   ```

2. **Track active servers:**
   ```json
   // .servers.json
   {
     "servers": [
       { "pid": 12345, "port": 3000, "task": "dev" }
     ]
   }
   ```

3. **Reuse if already running:**
   ```bash
   if port-in-use 3000; then
     echo "Server already running on port 3000"
   else
     start-server 3000
   fi
   ```

4. **Cleanup on task completion:**
   ```bash
   # Kill all tracked processes
   if [ -f .server.pid ]; then
     kill $(cat .server.pid)
     rm .server.pid
   fi

   # Release ports
   release-port 3000
   ```

---

## 🛠️ Practical Examples

### 1. Quick Build & Verify

```bash
# Build
npm run build

# Quick verification (not exhaustive)
if [ -f dist/index.js ]; then
  echo "✅ Build successful"
else
  echo "❌ Build failed"
  exit 1
fi

# Stop - no need to list all dist files
```

### 2. Server with Cleanup

```bash
# Start server
npm start &
SERVER_PID=$!
echo $SERVER_PID > .server.pid

# Wait for readiness
wait-for-localhost 3000 --timeout 10

# Test
curl http://localhost:3000/health

# Cleanup
kill $SERVER_PID
rm .server.pid
```

### 3. File Listing (Safe)

```powershell
# ✅ Good: Filtered, limited
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

Before marking task as done:
- [ ] Core functionality verified
- [ ] Output within limits (< 200 lines)
- [ ] Servers running in background (if needed)
- [ ] PIDs/ports tracked
- [ ] No recursive directory dumps
- [ ] Summary is concise and actionable
- [ ] Cleanup plan defined

After task completion:
- [ ] Temporary servers stopped
- [ ] Ports released
- [ ] Orphan processes cleaned
- [ ] State file updated
