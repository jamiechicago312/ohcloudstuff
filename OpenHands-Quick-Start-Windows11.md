# OpenHands Quick Start - Windows 11

*Get OpenHands running in 15 minutes on a clean Windows 11 system*

## What You Need to Install

Starting with a clean Windows 11 Home, install these in order:

1. **WSL (Windows Subsystem for Linux)** ⭐ **REQUIRED**
   - Open PowerShell as Administrator
   - Run: `wsl --install`
   - Restart computer when prompted
   - Verify: `wsl --version` (should show "Default Version: 2")
   - **Update**: `wsl --update` (gets latest WSL version)

2. **Ubuntu Linux Distribution** ⭐ **REQUIRED**
   - **Usually installs automatically** with WSL, but often fails
   - **After restart**: Check if "Ubuntu" appears in Start menu
   - **If Ubuntu is missing** (very common!):
     1. Open PowerShell as Administrator
     2. Run: `wsl --install -d Ubuntu`
         -  Can also download and install from the Microsoft Store
     4. Wait 5-10 minutes for download/installation
     5. Restart computer again
     6. Search "Ubuntu" in Start menu - should appear now
     7. Open Ubuntu to complete setup (create username/password)
   - **Check version**: In Ubuntu terminal: `lsb_release -a`
   - **Update**: In Ubuntu terminal: `sudo apt update && sudo apt upgrade -y`

3. **uv (Python Package Manager)** ⭐ **REQUIRED** 
   - **Why needed**: Official OpenHands method + required for MCP servers
   - **Install in Ubuntu terminal**:
     ```bash
     curl -LsSf https://astral.sh/uv/install.sh | sh
     source $HOME/.cargo/env //may not need to send this line of code
     ```
   - **Verify**: `uv --version`
      -  You will need a new terminal tab or restart the terminal before you run this after installing.
   - **Update**: `uv self update`

4. **Docker Desktop** ⭐ **REQUIRED**
   - Download: [docker.com](https://www.docker.com/products/docker-desktop/)
   - During setup: Enable "Use the WSL 2 based engine"
   - If you installed Docker before the above, check & configure WSL integration:
     - Open Docker Desktop → Settings → Resources → WSL Integration
     - Enable "Enable integration with my default WSL distro"
     - Enable integration with "Ubuntu"
     - Click "Apply & Restart"
   - **Update**: Docker Desktop → Check for updates

5. **Git for Windows** (Optional but recommended)
   - Download: [git-scm.com](https://git-scm.com/download/win)
   - Recommended when using GitHub repos and the like
   - Use default installation options
   - **Update**: Download latest version from website

## Quick Setup Steps

### Step 1: Open the WSL Terminal

- **Method 1 (Recommended)**: Search "Ubuntu" in Start menu and open it
- **Method 2**: In the Terminal, run `wsl`

**Set Ubuntu as Default (Recommended):**
If you do not, running `wsl` may open the wrong distribution.
```powershell
# In PowerShell - check what distributions you have
wsl --list

# Set Ubuntu as default so 'wsl' opens Ubuntu
wsl --set-default Ubuntu

# Verify Ubuntu version
wsl -d Ubuntu -- lsb_release -a
```

### Step 2: Verify Docker & uv
In the Ubuntu terminal, run:
```bash
docker --version
```
You should see a version number.

Then, run:
```bash
uv --version
```
You should see a version number.

### Step 3: Run OpenHands

**Preferred uv Method (Recommended)**
In the Ubuntu terminal, run:
```bash
# Official OpenHands method using uv (recommended)
uvx --python 3.12 --from openhands-ai openhands serve
```

**Alternative Docker Method:**
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

With either option, wait for this message:
```
INFO:     Uvicorn running on http://0.0.0.0:3000 (Press CTRL+C to quit)
```

### Step 4: Open in Browser
Go to: `http://localhost:3000`

### Step 5: Configure OpenHands
1. Choose your AI provider (OpenAI, Anthropic, etc.)
2. Enter your API key
3. Start chatting!

## Stopping OpenHands
Press `Ctrl+C` in the WSL terminal window.

## Common Issues (Most Frequent First)

### 🚨 **BLOCKER #1**: "I don't have Ubuntu" or "You don't have any WSL 2 distros installed"
**This affects 80% of users!**

**What happened**: `wsl --install` only installed WSL itself, but didn't install the Ubuntu Linux distribution (which is a separate dependency).

**Why Ubuntu is required**: OpenHands needs a proper Linux environment to run. WSL by itself is just the framework - you need Ubuntu (or another Linux distribution) as the actual operating system.

**Fix it step-by-step**:
1. Open PowerShell **as Administrator** (right-click → "Run as administrator")
2. Run: `wsl --install -d Ubuntu`
3. Wait for download/installation (can take 5-10 minutes)
4. **Restart your computer** when prompted
5. After restart, search "Ubuntu" in Start menu - should appear now
6. Open Ubuntu app to complete setup (create username/password)
7. **Verify**: Type `wsl --list` in PowerShell - should show Ubuntu

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
*For detailed troubleshooting and advanced setup, check out the official docs: https://docs.all-hands.dev/*
