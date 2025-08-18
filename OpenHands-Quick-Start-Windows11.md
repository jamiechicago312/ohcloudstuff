# OpenHands Quick Start - Windows 11

*Get OpenHands running in 15 minutes on a clean Windows 11 system*

## What You Need to Install

Starting with a clean Windows 11 Home, install these in order:

1. **WSL (Windows Subsystem for Linux)** ⭐ **REQUIRED**
   - Open PowerShell as Administrator
   - Run: `wsl --install`
   - Restart computer when prompted
   - **After restart**: Ubuntu should appear in Start menu
   - **If Ubuntu is missing**: Run `wsl --install -d Ubuntu` in PowerShell
   - Verify: `wsl --version` (should show "Default Version: 2")

2. **Docker Desktop** ⭐ **REQUIRED**
   - Download: [docker.com](https://www.docker.com/products/docker-desktop/)
   - During setup: Enable "Use the WSL 2 based engine"
   - **Important**: After installation, configure WSL integration:
     - Open Docker Desktop → Settings → Resources → WSL Integration
     - Enable "Enable integration with my default WSL distro"
     - Enable integration with "Ubuntu" (or your installed Linux distro)
     - Click "Apply & Restart"

3. **Git for Windows** (Optional but recommended)
   - Download: [git-scm.com](https://git-scm.com/download/win)
   - Use default installation options

## Quick Setup Steps

### Step 1: Open the Correct WSL Terminal
**⚠️ CRITICAL**: Never just type `wsl` - it opens the wrong distribution!

**✅ CORRECT Methods:**
- **Method 1 (Recommended)**: Search "Ubuntu" in Start menu and open it
- **Method 2**: In PowerShell, type `wsl -d Ubuntu` (not just `wsl`)

**❌ WRONG**: Typing just `wsl` opens docker-desktop distribution (doesn't work with Docker CLI)

**If you don't have Ubuntu yet:**
1. Open PowerShell as Administrator
2. Run: `wsl --install -d Ubuntu`
3. Restart computer
4. Then use Method 1 or 2 above

### Step 2: Verify Docker is Running
In the WSL terminal, run:
```bash
docker --version
```
You should see a version number.

### Step 3: Run OpenHands
Copy and paste this entire command into the WSL terminal:

```bash
docker run -it --rm --pull=always \
    -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik \
    -e LOG_ALL_EVENTS=true \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v ~/.openhands:/.openhands \
    -p 3000:3000 \
    --add-host host.docker.internal:host-gateway \
    --name openhands-app \
    docker.all-hands.dev/all-hands-ai/openhands:0.53
```

Wait for this message:
```
INFO:     Uvicorn running on http://0.0.0.0:3000 (Press CTRL+C to quit)
```

### Step 3: Open in Browser
Go to: `http://localhost:3000`

### Step 4: Configure OpenHands
1. Choose your AI provider (OpenAI, Anthropic, etc.)
2. Enter your API key
3. Start chatting!

## Stopping OpenHands
Press `Ctrl+C` in the WSL terminal window.

## Common Issues (Most Frequent First)

### 🚨 **BLOCKER #1**: "I don't have Ubuntu" or "You don't have any WSL 2 distros installed"
**This affects 80% of users!**

**What happened**: `wsl --install` didn't install Ubuntu properly.

**Fix it step-by-step**:
1. Open PowerShell **as Administrator** (right-click → "Run as administrator")
2. Run: `wsl --install -d Ubuntu`
3. Wait for download/installation (can take 5-10 minutes)
4. **Restart your computer** when prompted
5. After restart, search "Ubuntu" in Start menu - should appear now
6. Open Ubuntu app to complete setup (create username/password)

### 🚨 **BLOCKER #2**: Typing `wsl` opens docker-desktop (wrong distribution)
**This affects 90% of users!**

**What you see**: 
```
docker-desktop:/tmp/docker-desktop-root/...
```

**Why it happens**: Docker Desktop becomes your default WSL distribution.

**Quick fix**: Never type just `wsl`. Instead use:
```powershell
wsl -d Ubuntu
```

**Permanent fix** (after Ubuntu is installed):
```powershell
wsl --set-default Ubuntu
```

### 🚨 **BLOCKER #3**: "docker: command not found" or "This is not supported"
**What happened**: You're in the wrong terminal or Docker integration isn't set up.

**Fix it**:
1. Make sure Docker Desktop is running (check system tray)
2. Make sure you're in **Ubuntu** (not docker-desktop or PowerShell)
3. Go to Docker Desktop → Settings → Resources → WSL Integration
4. Enable "Enable integration with my default WSL distro"
5. Enable toggle for "Ubuntu"
6. Click "Apply & Restart"

### 🔧 **Other Issues**:

**Problem**: Browser shows "This site can't be reached"  
**Solution**: Wait 30-60 seconds for OpenHands to start, then refresh

**Problem**: Multi-line Docker command doesn't work  
**Solution**: Make sure you're in Ubuntu terminal (not PowerShell). The `\` backslashes only work in Linux terminals.

## That's It!
Total time: ~15 minutes including downloads.

---
*For detailed troubleshooting and advanced setup, see: [OpenHands-Windows11-Setup-Guide.md](OpenHands-Windows11-Setup-Guide.md)*