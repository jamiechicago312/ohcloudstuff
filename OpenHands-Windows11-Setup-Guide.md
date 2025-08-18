# OpenHands Setup Guide for Windows 11
*A Complete Beginner's Guide to Getting OpenHands Working on Windows 11*

This guide supplements the [official OpenHands documentation](https://docs.all-hands.dev/usage/local-setup#start-the-app) with Windows 11-specific instructions for inexperienced developers.

## Prerequisites: What You Need to Install First

Starting with a **clean Windows 11** system, you'll need these tools. Install them in this order:

### Required Dependencies

1. **Windows Terminal** (Recommended but Optional)
   - Download from Microsoft Store or [GitHub](https://github.com/microsoft/terminal)
   - Modern terminal app that can run PowerShell, Command Prompt, WSL, etc.
   - **Note**: You can use regular PowerShell instead - both work fine!

2. **Docker Desktop** ⭐ **MOST IMPORTANT**
   - Download from [docker.com](https://www.docker.com/products/docker-desktop/)
   - **Required for OpenHands to work properly**
   - Enable WSL 2 integration during setup

3. **Git for Windows**
   - Download from [git-scm.com](https://git-scm.com/download/win)
   - Choose default options during installation

4. **Python 3.12** (Recommended) or **Python 3.13**
   - Download from [python.org](https://www.python.org/downloads/)
   - ⚠️ **IMPORTANT**: Check "Add Python to PATH" during installation
   - Choose Python 3.12 for best compatibility

5. **uv** (Python package manager)
   - Install via PowerShell: `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`
   - Or download from [astral.sh/uv](https://astral.sh/uv/)

### Optional but Recommended

6. **WSL (Windows Subsystem for Linux)**
   - Run in PowerShell as Administrator: `wsl --install`
   - Restart computer when prompted
   - Useful for advanced development

7. **Visual Studio Code**
   - Download from [code.visualstudio.com](https://code.visualstudio.com/)
   - Great for editing code and files

## Complete Setup Checklist for Beginners

Follow this step-by-step checklist if you're starting from scratch:

### Phase 1: Install Required Software
- [ ] Install Windows Terminal from Microsoft Store
- [ ] Install Docker Desktop from docker.com
- [ ] Install Git for Windows from git-scm.com
- [ ] Install Python 3.12 from python.org (check "Add to PATH")
- [ ] Install uv using PowerShell command above
- [ ] Restart your computer

### Phase 2: Verify Installation
Open PowerShell and run these commands to verify everything is installed:

```powershell
# Check Docker
docker --version

# Check Git
git --version

# Check Python
python --version

# Check uv
uv --version
```

You should see version numbers for all of these.

### Phase 3: Run OpenHands
```powershell
# Run the Docker command (copy and paste the entire line)
docker run -it --rm --pull=always -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik -e LOG_ALL_EVENTS=true -v /var/run/docker.sock:/var/run/docker.sock -v ~/.openhands:/.openhands -p 3000:3000 --add-host host.docker.internal:host-gateway --name openhands-app docker.all-hands.dev/all-hands-ai/openhands:0.53
```

### Phase 4: Access in Browser
- [ ] Open browser and go to `http://localhost:3000`
- [ ] Set up your LLM provider and API key
- [ ] Start using OpenHands!

**Total setup time: 15-30 minutes for a complete beginner**

## Windows Terminal vs PowerShell - What's the Difference?

**You're absolutely right to be confused!** Here's the clarification:

### **PowerShell** = The Shell/Language
- **PowerShell** is the **command language/shell** (like bash on Linux)
- It's what interprets your commands like `docker run`, `git clone`, etc.
- **This is what you're actually using** when you type commands

### **Windows Terminal** = The App/Window
- **Windows Terminal** is just a **modern terminal application**
- It's like a fancy window that can run PowerShell, Command Prompt, WSL, etc.
- Think of it as a "container" for different shells

### **What You're Actually Using:**

When you search "Terminal" and it opens:
- **The app**: Might be Windows Terminal OR the old PowerShell app
- **The shell**: Is PowerShell (you can see `PS C:\Users\dcrul>` in your examples)

### **In VS Code:**
- VS Code uses **PowerShell by default** on Windows
- But it can run inside either the old PowerShell app OR Windows Terminal
- The **commands are the same** regardless of which terminal app you use

### **Why Windows Terminal is "Better":**
- **Tabs** - multiple terminals in one window
- **Better fonts** and colors
- **Copy/paste** works better
- **Customizable** themes and settings
- **Can run multiple shells** (PowerShell, Command Prompt, WSL) in tabs

### **Bottom Line:**
- ✅ **You can keep using regular PowerShell** - it works perfectly fine!
- ✅ **All the commands in this guide work the same** in both
- ✅ **Windows Terminal is just a nicer experience** but not required

**For OpenHands setup**: Regular PowerShell is totally fine! The Docker commands work exactly the same.

## What is OpenHands?

**OpenHands** is an AI-powered coding assistant that can help you with programming tasks, debugging, and development work. It runs in your browser and can interact with your local development environment.

## What is Docker and Why Do We Need It?

**Docker** is a platform that packages applications and their dependencies into containers. For OpenHands:
- ✅ **Avoids dependency conflicts** (like the Python library issues)
- ✅ **Works consistently** across different systems
- ✅ **Official OpenHands recommendation**
- ✅ **Easiest setup method**

## What is WSL?

**WSL (Windows Subsystem for Linux)** is a compatibility layer that allows you to run a Linux environment directly on Windows without the overhead of a traditional virtual machine. Think of it as having a Linux terminal and file system running alongside your Windows system.

### Why might you want WSL for development?
- Many development tools are designed for Linux/Unix environments
- Better compatibility with some Python packages and dependencies
- More reliable package management with tools like `uv`
- Seamless integration with Docker and other development tools

## Important: PowerShell vs Bash Commands

**Key difference for Windows users**: Most development documentation (including OpenHands) shows commands in **Linux/Bash format**, but Windows uses **PowerShell** which has different syntax.

### Line Continuation Differences:
- **Bash/Linux**: Uses backslash `\` to continue lines
- **PowerShell**: Uses backtick `` ` `` to continue lines

### Example:
**Bash format (from docs):**
```bash
docker run -it --rm \
  -e SOME_VAR=value \
  image_name
```

**PowerShell format (what works on Windows):**
```powershell
docker run -it --rm `
  -e SOME_VAR=value `
  image_name
```

**Or just use one line in PowerShell:**
```powershell
docker run -it --rm -e SOME_VAR=value image_name
```

This is why the official OpenHands Docker command doesn't work when copy-pasted directly into PowerShell!

## Best Practices for Cross-Platform Documentation

Here's how to write documentation that works for **Mac, Linux, and Windows** users:

### Method 1: OS-Specific Tabs/Sections ⭐ **Most Professional**

**🐧 Linux / 🍎 macOS:**
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

**🪟 Windows (PowerShell):**
```powershell
docker run -it --rm --pull=always `
 -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik `
 -e LOG_ALL_EVENTS=true `
 -v /var/run/docker.sock:/var/run/docker.sock `
 -v ~/.openhands:/.openhands `
 -p 3000:3000 `
 --add-host host.docker.internal:host-gateway `
 --name openhands-app `
 docker.all-hands.dev/all-hands-ai/openhands:0.53
```

### Method 2: Universal Command First ⭐ **Most User-Friendly**

**✅ Works on all platforms (single line):**
```bash
docker run -it --rm --pull=always -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik -e LOG_ALL_EVENTS=true -v /var/run/docker.sock:/var/run/docker.sock -v ~/.openhands:/.openhands -p 3000:3000 --add-host host.docker.internal:host-gateway --name openhands-app docker.all-hands.dev/all-hands-ai/openhands:0.53
```

<details>
<summary>📋 Multi-line versions (click to expand)</summary>

**Linux/macOS (Bash):**
```bash
docker run -it --rm --pull=always \
 -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik \
 -e LOG_ALL_EVENTS=true \
 # ... rest of command
```

**Windows (PowerShell):**
```powershell
docker run -it --rm --pull=always `
 -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik `
 -e LOG_ALL_EVENTS=true `
 # ... rest of command
```
</details>

### Method 3: Clear Visual Indicators

| Platform | Command Format | Line Continuation |
|----------|----------------|-------------------|
| 🐧 **Linux** | `bash` | `\` (backslash) |
| 🍎 **macOS** | `bash` or `zsh` | `\` (backslash) |
| 🪟 **Windows** | `powershell` | `` ` `` (backtick) |

### Method 4: Copy-Paste Ready Sections

````markdown
### For Linux/macOS users:
```bash
# Copy this entire block
docker run -it --rm \
  --pull=always \
  image_name
```

### For Windows users:
```powershell
# Copy this entire block
docker run -it --rm `
  --pull=always `
  image_name
```
````

## Examples from Popular Projects:

### **Docker's Official Docs** - Uses tabs
- Separate tabs for Linux, macOS, Windows
- Each tab shows the appropriate syntax

### **Node.js Docs** - Universal first, then specific
- Shows `npm install package` (works everywhere)
- Then shows OS-specific installation methods

### **Kubernetes Docs** - Visual indicators
- Uses emojis (🐧 🍎 🪟) for quick identification
- Color-coded sections

### **GitHub's Docs** - Collapsible sections
- Main command visible
- Platform-specific details in expandable sections

## **Recommendation for OpenHands:**

**Best approach would be:**

1. **Universal command first** (single line that works everywhere)
2. **Collapsible sections** for multi-line versions
3. **Clear visual indicators** (emojis/icons)
4. **Explanation of differences** (like we added to this guide)

This way:
- ✅ **Beginners** get a simple copy-paste solution
- ✅ **Advanced users** can see platform-specific optimizations  
- ✅ **All platforms** are clearly supported
- ✅ **Reduces confusion** about syntax differences

## Different Ways to Access WSL (Industry Standards)

### Method 1: Type `wsl` in PowerShell ⭐ **Most Common**
- **What it does**: Enters your default WSL distribution directly in PowerShell
- **Industry standard**: Yes, this is the most common way developers use WSL
- **Pros**: Quick, stays in same window, integrates well with Windows Terminal
- **When to use**: Daily development work, running commands

### Method 2: Open Ubuntu app separately
- **What it does**: Opens Ubuntu in a separate window
- **Industry standard**: Less common for development
- **Pros**: Separate window, feels more like a "real" Linux terminal
- **When to use**: When you want WSL completely separate from Windows

### Method 3: Windows Terminal with WSL profile ⭐ **Professional Standard**
- **What it does**: Windows Terminal with tabs for PowerShell, WSL, etc.
- **Industry standard**: This is what most professional developers use
- **Pros**: Best of both worlds, multiple tabs, modern terminal features
- **Setup**: Install Windows Terminal from Microsoft Store

**Recommendation**: Use Method 1 (`wsl` in PowerShell) or Method 3 (Windows Terminal). Both keep you in the same environment while giving you Linux capabilities.

## Python Version Strategy: Flexible First, Specific Second

### Should you specify Python version?

**Start flexible, get specific if needed:**

1. **Try without version first**: `uvx --from openhands-ai openhands serve`
   - Let uv choose the best available Python
   - More likely to work with your current setup
   
2. **Specify your version if needed**: `uvx --python 3.13 --from openhands-ai openhands serve`
   - Use your installed Python 3.13
   - More predictable and explicit
   
3. **Use OpenHands recommended version if compatibility issues**: `uvx --python 3.12 --from openhands-ai openhands serve`
   - OpenHands docs specify 3.12 for maximum compatibility
   - May require installing Python 3.12

**Why this approach?**
- ✅ **Flexibility first**: Works with what you have
- ✅ **Fallback options**: Clear path if issues arise  
- ✅ **Industry standard**: Start simple, add constraints as needed

## Managing Multiple Python Versions on Windows

### Can I have both Python 3.12 and 3.13? **YES!**

**Absolutely!** Having multiple Python versions is:
- ✅ **Recommended** for developers
- ✅ **Very common** in professional environments  
- ✅ **Safe** - they don't interfere with each other
- ✅ **No need to uninstall** your existing Python 3.13

### Method 1: Use uv (Easiest - You already have this!)

```powershell
# Install Python 3.12 using uv
uv python install 3.12

# List all Python versions uv knows about
uv python list

# Use specific version with any command
uvx --python 3.12 --from openhands-ai openhands serve
uvx --python 3.13 --from some-other-package some-command
```

### Method 2: Install from python.org (Traditional)

1. Go to https://www.python.org/downloads/
2. Download Python 3.12.x (latest 3.12 version)
3. **Important**: During installation, check "Add Python to PATH" 
4. Both versions will be available

### Method 3: Use pyenv-win (Advanced)

```powershell
# Install pyenv-win (Python version manager)
git clone https://github.com/pyenv-win/pyenv-win.git %USERPROFILE%\.pyenv

# Add to PATH (restart PowerShell after)
# Then install Python versions
pyenv install 3.12.0
pyenv install 3.13.0
pyenv global 3.12.0  # Set default
```

### How to check which Python versions you have:

```powershell
# Check default Python
python --version

# Check all Python versions (if installed traditionally)
py -0  # Lists all installed Python versions

# Check uv-managed Python versions
uv python list

# Use specific version
py -3.12 --version
py -3.13 --version
```

### **Recommendation for you:**

Since you already have uv, use **Method 1**:

```powershell
# Install Python 3.12 with uv
uv python install 3.12

# Try OpenHands with 3.12
uvx --python 3.12 --from openhands-ai openhands serve
```

This keeps everything clean and managed by uv!

## Prerequisites Check

You mentioned you have these installed on Windows:
- ✅ .NET Core Runtime
- ✅ PowerShell
- ✅ WSL
- ✅ Docker
- ✅ Python 3.13
- ✅ Git
- ✅ Node.js and npm
- ✅ uv (recently installed)

## Step 1: Verify and Set Up WSL

### Check if WSL is properly installed and running

1. Open PowerShell as Administrator
2. Check WSL status:
```powershell
wsl --list --verbose
```

If you don't see a Linux distribution installed, install Ubuntu:
```powershell
wsl --install -d Ubuntu
```

### Access your WSL environment

1. Open PowerShell or Windows Terminal
2. Type `wsl` or `ubuntu` to enter your Linux environment
3. You should see a Linux prompt like: `username@computername:~$`

**Important**: If you see `docker-desktop:/tmp/docker-desktop-root/...` you're in Docker's WSL environment, not a proper Linux distribution. See troubleshooting section below.

## Step 2: Set Up Python and uv in WSL

Your Windows Python installation is separate from WSL. You need to install Python and uv inside WSL.

### Install Python in WSL

```bash
# Update package list
sudo apt update

# Install Python 3.12 (recommended for OpenHands)
sudo apt install python3.12 python3.12-venv python3.12-dev python3-pip -y

# Set Python 3.12 as default (optional)
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1
```

### Install uv in WSL

```bash
# Install uv using the official installer
curl -LsSf https://astral.sh/uv/install.sh | sh

# Reload your shell or source the profile
source ~/.bashrc
# OR restart your WSL session

# Verify uv installation
uv --version
```

### Verify Python installation

```bash
# Check Python version
python3 --version

# Check if pip is working
python3 -m pip --version
```

## Quick Start: Running OpenHands (Recommended Method)

### Method 1: Using Docker (Easiest and Most Reliable) ⭐

This is the **recommended method** for Windows 11 users:

```powershell
# Open PowerShell and run this single command:
docker run -it --rm --pull=always -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik -e LOG_ALL_EVENTS=true -v /var/run/docker.sock:/var/run/docker.sock -v ~/.openhands:/.openhands -p 3000:3000 --add-host host.docker.internal:host-gateway --name openhands-app docker.all-hands.dev/all-hands-ai/openhands:0.53
```

**What this command does:**
- Downloads OpenHands Docker image (first time only)
- Starts OpenHands server on port 3000
- Sets up proper networking and file access
- Creates a container named `openhands-app`

**You should see output like:**
```
Starting OpenHands...
INFO:     Uvicorn running on http://0.0.0.0:3000 (Press CTRL+C to quit)
```

### Method 2: Using uv (Alternative - May have dependency issues)

If you prefer to use Python directly:

```powershell
# Install and run OpenHands with uv
uvx --python 3.12 --from openhands-ai openhands serve
```

**Note**: This method may encounter Python dependency conflicts (see troubleshooting section).

## Step 2: Access OpenHands in Your Browser

Once you see the "Uvicorn running" message, OpenHands is ready!

### Open Your Browser and Go To:
```
http://localhost:3000
```

**You should see:**
- OpenHands web interface
- Chat area for interacting with the AI
- File explorer on the left
- Settings panel

### First Time Setup in Browser:
1. **Choose your LLM Provider** (e.g., OpenAI, Anthropic, etc.)
2. **Enter your API Key** for your chosen provider
3. **Start chatting** with OpenHands!

### If the page doesn't load:
- **Wait 30-60 seconds** - the interface takes time to start
- **Try refreshing** the page
- **Try these alternative URLs:**
  - `http://127.0.0.1:3000`
  - `http://host.docker.internal:3000`

## Step 3: Using OpenHands

Once you're in the web interface:

1. **Set up your LLM**: Click Settings → LLM → Choose provider and add API key
2. **Start a conversation**: Type a message like "Hello, can you help me write a Python script?"
3. **Give it tasks**: Ask it to create files, debug code, or explain concepts
4. **Use the file explorer**: Browse and edit files in the left panel

## Stopping OpenHands

To stop OpenHands:
- **Press `Ctrl+C`** in the PowerShell window where Docker is running
- Or close the PowerShell window

To start it again, just run the Docker command again.

## Troubleshooting Common Issues

### Issue 0: You're in Docker's WSL instead of your main environment

**Problem**: Your prompt shows `docker-desktop:/tmp/docker-desktop-root/...` and `sudo: not found`
**Cause**: You're in Docker Desktop's minimal WSL environment, not your main Windows environment or a proper Linux distribution

**You have 3 solutions - pick the one that works best for you:**

#### Solution A: Use Windows PowerShell directly (Easiest)
Since you have Python 3.13 and uv installed on Windows, try this first:

```powershell
# Exit WSL first
exit

# Step 1: Try without specifying Python version (most flexible)
uvx --from openhands-ai openhands serve

# Step 2: If that fails, try with your Python 3.13
uvx --python 3.13 --from openhands-ai openhands serve

# Step 3: If compatibility issues, install Python 3.12 and use it
# (Only if the above fail due to Python 3.13 compatibility issues)
uvx --python 3.12 --from openhands-ai openhands serve
```

#### Solution B: Use Docker method (Official OpenHands method)
Since you have Docker working, use OpenHands' official Docker method:

```powershell
# In PowerShell (not WSL)
docker pull docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik

docker run -it --rm --pull=always -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik -e LOG_ALL_EVENTS=true -v /var/run/docker.sock:/var/run/docker.sock -v ~/.openhands:/.openhands -p 3000:3000 --add-host host.docker.internal:host-gateway --name openhands-app docker.all-hands.dev/all-hands-ai/openhands:0.53
```

#### Solution C: Install a proper Linux distribution (Most flexible)
```powershell
# In PowerShell (exit WSL first by typing 'exit')
# List available distributions
wsl --list --online

# Install Ubuntu (recommended)
wsl --install -d Ubuntu

# After installation, set Ubuntu as default
wsl --set-default Ubuntu

# Now when you type 'wsl', you'll enter Ubuntu instead of docker-desktop
wsl
```

**Recommendation**: Try Solution A first (Windows PowerShell), then Solution B (Docker) if that doesn't work.

### Issue 1: ImportError with OpenAI library (Common on Windows)

**Problem**: `ImportError: cannot import name 'ResponseTextConfig' from 'openai.types.responses.response'`
**Cause**: Known issue - OpenAI SDK 1.100.0+ removed `ResponseTextConfig`, but LiteLLM (used by OpenHands) still tries to import it
**Status**: ✅ **OpenHands team is actively fixing this!** See: https://github.com/All-Hands-AI/OpenHands/pull/10471

**Solution A: Use the fix branch (Most up-to-date)**
Try the branch that fixes this exact issue:

```powershell
# Use the fix branch directly
uvx --python 3.12 --from git+https://github.com/All-Hands-AI/OpenHands@pin-openai-1-99-9 openhands serve
```

**Solution B: Use Docker with the fix (Recommended)**
```powershell
# Use Docker with the fix branch
docker run -it --rm -p 3000:3000 -v /var/run/docker.sock:/var/run/docker.sock --add-host host.docker.internal:host-gateway -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:1b68cdf-nikolaik --name openhands-app-1b68cdf docker.all-hands.dev/all-hands-ai/openhands:1b68cdf
```

**Solution C: Use stable Docker (Fallback)**
```powershell
# Use OpenHands' official stable Docker method
docker run -it --rm --pull=always -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik -e LOG_ALL_EVENTS=true -v /var/run/docker.sock:/var/run/docker.sock -v ~/.openhands:/.openhands -p 3000:3000 --add-host host.docker.internal:host-gateway --name openhands-app docker.all-hands.dev/all-hands-ai/openhands:0.53
```

**Solution B: Install Python 3.12 alongside 3.13**
Python 3.13 is very new and may have compatibility issues. You can keep both versions:

**Method 1: Use uv to install Python 3.12 (Easiest)**
```powershell
# uv can install and manage Python versions for you
uv python install 3.12

# Verify it's installed
uv python list

# Now use it with OpenHands
uvx --python 3.12 --from openhands-ai openhands serve
```

**Method 2: Download Python 3.12 from python.org**
1. Go to https://www.python.org/downloads/
2. Download Python 3.12.x (latest 3.12 version)
3. Install it (it will coexist with 3.13)
4. Then run: `uvx --python 3.12 --from openhands-ai openhands serve`

**Solution C: Use WSL with proper Linux distribution**
Set up Ubuntu in WSL (more reliable for Python packages):

```powershell
wsl --install -d Ubuntu
wsl --set-default Ubuntu
wsl
# Then follow the WSL setup steps in this guide
```

### Issue 2: Multi-line Docker command doesn't work in PowerShell

**Problem**: The official OpenHands Docker command from their docs doesn't work when copy-pasted into PowerShell
**Cause**: The official docs show Linux/Bash format with `\` line continuations, but PowerShell uses different syntax

**Solution A: Use the single-line version (Recommended)**
```powershell
# Copy and paste this ENTIRE line as one command:
docker run -it --rm --pull=always -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik -e LOG_ALL_EVENTS=true -v /var/run/docker.sock:/var/run/docker.sock -v ~/.openhands:/.openhands -p 3000:3000 --add-host host.docker.internal:host-gateway --name openhands-app docker.all-hands.dev/all-hands-ai/openhands:0.53
```

**Solution B: Use PowerShell multi-line syntax**
```powershell
docker run -it --rm --pull=always `
 -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.53-nikolaik `
 -e LOG_ALL_EVENTS=true `
 -v /var/run/docker.sock:/var/run/docker.sock `
 -v ~/.openhands:/.openhands `
 -p 3000:3000 `
 --add-host host.docker.internal:host-gateway `
 --name openhands-app `
 docker.all-hands.dev/all-hands-ai/openhands:0.53
```

**Note**: PowerShell uses backticks (`) instead of backslashes (\) for line continuation.

### Issue 3: "Command not found" errors in WSL

**Problem**: Commands like `python`, `uv`, or `git` not found in WSL
**Solution**: Install the tools in WSL separately from Windows:

```bash
# Install git in WSL
sudo apt install git -y

# Install Node.js and npm in WSL (if needed)
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### Issue 2: Permission errors

**Problem**: Permission denied when running commands
**Solution**: 

```bash
# Fix ownership of your home directory
sudo chown -R $USER:$USER ~/

# Or run with proper permissions
sudo uvx --python 3.12 --from openhands-ai openhands serve
```

### Issue 3: Port conflicts

**Problem**: Port already in use
**Solution**: Specify a different port:

```bash
uvx --python 3.12 --from openhands-ai openhands serve --port 3001
```

### Issue 4: Docker integration

**Problem**: OpenHands can't access Docker
**Solution**: Make sure Docker Desktop is running and WSL integration is enabled:

1. Open Docker Desktop
2. Go to Settings → Resources → WSL Integration
3. Enable integration with your WSL distribution
4. Restart WSL: `wsl --shutdown` then `wsl`

## File System Navigation

### Understanding WSL file paths

- **WSL files**: `/home/username/` (Linux-style paths)
- **Windows files from WSL**: `/mnt/c/Users/YourName/` (access Windows C: drive)
- **WSL files from Windows**: `\\wsl$\Ubuntu\home\username\` (access WSL from Windows Explorer)

### Best practices

1. **Keep development projects in WSL**: Store your code in `/home/username/projects/` for better performance
2. **Use WSL terminal for development**: Use Windows Terminal with WSL profile
3. **Access files**: Use VS Code with WSL extension for seamless editing

## Quick Start Commands

Once everything is set up, here's your typical workflow:

```bash
# 1. Open WSL (from PowerShell or Windows Terminal)
wsl

# 2. Navigate to your project directory
cd ~/projects

# 3. Run OpenHands
uvx --python 3.12 --from openhands-ai openhands serve

# 4. Open browser to http://localhost:3000
```

## Alternative: Using PowerShell (Windows Native)

If you prefer to use PowerShell instead of WSL:

1. Make sure Python 3.12 is installed on Windows
2. Install uv for Windows (which you've already done)
3. Try running:
```powershell
uvx --python 3.12 --from openhands-ai openhands serve
```

If this doesn't work, the issue might be:
- Python 3.12 not found (you have 3.13 installed)
- Path issues with uv or Python
- Windows-specific compatibility issues

## Recommended Approach

**For the best experience, I recommend using WSL** because:
1. Better compatibility with OpenHands and its dependencies
2. More reliable package management
3. Easier Docker integration
4. Consistent with most development tutorials and documentation

## Next Steps

1. Set up your WSL environment following the steps above
2. Install Python 3.12 and uv in WSL
3. Run OpenHands using the WSL terminal
4. Consider installing VS Code with the WSL extension for development

## Getting Help

If you encounter issues:
1. Check the OpenHands documentation: https://docs.all-hands.dev/
2. Verify your WSL setup: `wsl --status`
3. Check Python and uv versions in WSL
4. Look at the terminal output for specific error messages

## Tips for New OpenHands Users

### Getting Started with OpenHands
1. **Start simple**: Ask it to create a basic "Hello World" program
2. **Be specific**: Instead of "help me code", try "create a Python script that reads a CSV file"
3. **Use the file explorer**: You can see and edit all files OpenHands creates
4. **Ask for explanations**: "Explain what this code does line by line"

### Common Use Cases
- **Learning to code**: "Teach me Python basics with examples"
- **Debugging**: "This code isn't working, can you help fix it?"
- **Code review**: "Review this code and suggest improvements"
- **Project setup**: "Help me set up a new React project"

### Best Practices
- **Keep Docker Desktop running** when using OpenHands
- **Save your work**: Files created in OpenHands are saved to your computer
- **Use version control**: OpenHands can help you with Git commands
- **Ask follow-up questions**: OpenHands remembers the conversation context

## Getting Help

### If you encounter issues:
1. **Check the troubleshooting section** in this guide
2. **Visit the official docs**: https://docs.all-hands.dev/
3. **Join the community**: OpenHands has Discord and GitHub discussions
4. **Check GitHub issues**: Someone might have had the same problem

### Useful Resources
- **Official Documentation**: https://docs.all-hands.dev/
- **GitHub Repository**: https://github.com/All-Hands-AI/OpenHands
- **Community Discord**: Check the GitHub repo for invite link

## Next Steps

Once you have OpenHands working:
1. **Explore different LLM providers** to find what works best for you
2. **Try different types of projects** (web development, data analysis, etc.)
3. **Learn about Docker** to understand how OpenHands works under the hood
4. **Set up WSL** for more advanced development workflows

---

*This guide was created to help Windows 11 users get OpenHands running locally. It supplements the official OpenHands documentation with Windows-specific instructions for beginners.*

**Last updated**: August 2024  
**Tested on**: Windows 11, Docker Desktop, OpenHands 0.53