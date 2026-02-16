# Bruno's tutorial to Running AI Locally

---

## Table of Contents

1. [Install Git on Windows](#install-git-on-windows)
2. [Learn Git Basics](#learn-git-basics)
3. [Install Ollama (The AI Engine)](#install-ollama-the-ai-engine)
4. [Download and Run Your First AI Model](#download-and-run-your-first-ai-model)
5. [Install VS Code & AI Extensions](#install-vs-code--ai-extensions)
6. [Install OpenCode (AI Terminal Assistant)](#install-opencode-ai-terminal-assistant)
7. [Understanding Skill Files](#understanding-skill-files)

---

## Install Git on Windows

Git is a tool for **saving different versions of your code** and **sharing code with others**. Think of it like "Track Changes" in Microsoft Word, but for code.

* **Download**: [git-scm.com](https://git-scm.com/install/windows)

Git needs to know who you are. Run these commands in PowerShell:

```powershell
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Replace "Your Name" with your actual name and "your.email@example.com" with your email. For example:
```powershell
git config --global user.name "Bruno"
git config --global user.email "bruno@example.com"
```

---

## Learn Git Basics

### Understanding Git Concepts

**Repository (Repo)**: A folder where Git tracks your files. It's like a project folder with history.

**Commit**: Saving a snapshot of your code with a message explaining what changed. Think of it like saving a version in Word.

**Branch**: A separate copy of your code where you can make changes without affecting the original. Like working on a "draft" version.

**GitHub**: A website where you can upload your repositories so others can see your code or collaborate with you.

### Basic Git Workflow

#### 1. Create a New Repository

* Open [Github](https://github.com/).  
* Login  
* Click to [Create Repository](https://github.com/new)
* Clone the repository and open in vscode


### Creating Branches (Making a Copy)

Branches let you work on new features without changing your main code.

```powershell
# Create a new branch
git branch feature/add-chat

# Switch to that branch
git checkout feature/add-chat

# Or create and switch in one command
git checkout -b feature/add-chat
```

Make changes, then commit them:
```powershell
git add .
git commit -m "Add chat feature"
```

### Merging Branches (Combining Changes)

When your feature is ready, merge it back to main:

```powershell
# Switch back to main
git checkout main

# Merge the feature
git merge feature/add-chat
```

---

## Install Ollama (The AI Engine)

Ollama is the software that actually runs AI models on your computer. It's like the "engine" that powers everything.

### Step 1: Download Ollama

1. Go to: **https://ollama.com/download**
2. Click the **"Download for Windows"** button (or the link)
3. A file `OllamaSetup.exe` will download

### Step 2: Install Ollama

1. Double-click `OllamaSetup.exe`
2. Click **"Install"**
3. Ollama will install automatically
4. You may see a prompt to restart your computer - do it
5. Ollama will start automatically (you'll see a small icon in your system tray - bottom right)

### Step 3: Verify Ollama is Running

You should see an **Ollama icon** in your system tray (bottom right corner):

- Look for a small icon that looks like a llama or colorful symbol
- If it's there, Ollama is running

To verify, open PowerShell and run:

```powershell
ollama --version
```

You should see a version number (e.g., `0.1.15`).

---

## Download and Run Your First AI Model

### What are AI Models?

AI models are like pre-trained "brains" that have learned patterns from lots of data. Different models are good at different things:

- **Mistral**: Fast, general-purpose, good for most things
- **Llama2**: High quality, but slower
- **CodeLlama**: Specialized for programming
- **Neural-Chat**: Optimized for conversations
- **Orca-Mini**: Very small and fast (good for older computers)

### Step 1: Download a Model

Open PowerShell and run:

```powershell
ollama pull mistral
```

This downloads Mistral (about 4GB). It may take 5-10 minutes depending on your internet.

You'll see download progress:
```
pulling manifest
pulling 2c051247ff01
downloading 1.2 GB
```

When done, you'll see `success`.

### Step 2: Run the Model

In PowerShell, run:

```powershell
ollama run mistral
```

This opens an interactive chat with the AI. You'll see:

```
>>> 
```

Type a question and press Enter:

```
>>> What is the capital of France?
```

The AI will think for a few seconds, then respond:

```
The capital of France is Paris.

>>> 
```

Great! You're talking to AI on your local computer!

Type `exit` to close the chat.

### Step 3: Try Other Models (Optional)

Download and try other models:

```powershell
ollama pull llama2
ollama run llama2

# Or for coding
ollama pull codellama
ollama run codellama
```

### List Downloaded Models

To see all models you've downloaded:

```powershell
ollama list
```

### Using Ollama in the Background

Ollama can run as a service in the background. To start it:

```powershell
ollama serve
```

This starts a server on your computer at: `http://localhost:11434`

You can keep this running in one PowerShell window and use Ollama from other programs in other windows.

---

## Install VS Code & AI Extensions

VS Code is a free code editor. We'll add AI extensions to help you code faster.

### Step 1: Download VS Code

1. Go to: **https://code.visualstudio.com**
2. Click **"Download"** (Windows version)
3. A file will download

### Step 2: Install VS Code

1. Double-click the downloaded file
2. Click **"Next"** through all screens
3. Click **"Install"**
4. Click **"Finish"**
5. VS Code will open

### Step 3: Install Continue (AI Coding Assistant)

Continue is an AI assistant inside VS Code that works with local models like Ollama.

1. In VS Code, click the **Extensions** icon (left sidebar, looks like 4 squares)
2. Search for **"Continue"**
3. Click **"Install"** on the "Continue" extension (by Continue Dev)
4. VS Code will install it

### Step 4: Configure Continue for Ollama

1. Click **"Continue"** icon in the left sidebar
2. Click the **settings icon** (gear or ⚙️)
3. A file called `config.json` will open
4. Replace the entire contents with:

```json
{
  "models": [
    {
      "title": "Mistral",
      "provider": "ollama",
      "model": "mistral",
      "apiBase": "http://localhost:11434"
    }
  ],
  "tabAutocompleteModel": {
    "title": "Mistral",
    "provider": "ollama",
    "model": "mistral",
    "apiBase": "http://localhost:11434"
  }
}
```

5. Save the file (Ctrl+S)

### Step 5: Use Continue

First, make sure Ollama is running:
```powershell
ollama serve
```

Then in VS Code:

- Press **Ctrl+L** to open the Continue chat
- Type a question or ask for code help
- The AI will respond using your local Ollama model

Example:
```
Write a Python function to add two numbers
```

Continue will generate code for you!

---

## Install OpenCode (AI Terminal Assistant)

OpenCode is an open-source AI coding assistant that runs directly in your terminal. It provides intelligent code generation and assistance right from the command line, and it integrates seamlessly with Ollama to use your local AI models.

### What is OpenCode?

OpenCode is a powerful terminal-based AI assistant that helps you write, debug, and understand code. You can ask it questions, request code generation, and get suggestions—all without leaving your terminal. It's perfect if you prefer working in the command line or want a lightweight alternative to VS Code extensions.

**Key Benefits:**
- Runs directly in your terminal
- Uses local AI models via Ollama
- Fast and lightweight
- Requires a larger context window (64k tokens recommended)
- Supports multiple AI models

### Step 1: Install OpenCode

Open PowerShell and run:

```powershell
curl -fsSL https://opencode.ai/install | bash
```

This downloads and installs the OpenCode CLI tool.

### Step 2: Quick Setup with Ollama

The easiest way to use OpenCode with Ollama is to run:

```powershell
ollama launch opencode
```

This automatically configures OpenCode to work with Ollama on your local computer.

### Step 3: Manual Configuration (Optional)

If you prefer to configure OpenCode manually, edit `~/.config/opencode/opencode.json` and add this configuration:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      },
      "models": {
        "mistral": {
          "name": "mistral"
        }
      }
    }
  }
}
```

### Step 4: Use OpenCode

Make sure Ollama is running:

```powershell
ollama serve
```

Then in another PowerShell window, use OpenCode by typing:

```powershell
opencode
```

You can ask it questions and request code help:

```
opencode "Write a Python function to check if a number is prime"
```

Or start an interactive session:

```powershell
opencode
```

### Recommended Models for OpenCode

OpenCode works best with models that have larger context windows (at least 64k tokens):

- **mistral**: General-purpose, fast and reliable
- **qwen-3-coder**: Specialized for programming tasks (requires `qwen3-coder` model)
- **codellama**: Excellent for code-related tasks

Download a model with:

```powershell
ollama pull mistral
ollama pull codellama
```

### Using OpenCode with Cloud Models

If you want to use cloud-based models, create an API key at [ollama.com](https://ollama.com/settings/keys) and update your configuration to:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama Cloud",
      "options": {
        "baseURL": "https://ollama.com/v1"
      },
      "models": {
        "glm-4.7:cloud": {
          "name": "glm-4.7:cloud"
        }
      }
    }
  }
}
```

For more details, see the [OpenCode documentation](https://docs.ollama.com/integrations/opencode).

---

## Understanding Skill Files

Skill files are configuration files that define custom behaviors, prompts, and integrations for your AI coding assistants. They act as templates or blueprints that allow you to customize how your AI tools interact with you and your codebase.

### What Are Skill Files?

Skill files are typically JSON or YAML configuration files that extend the capabilities of tools like Continue or OpenCode. They allow you to:

- **Create custom AI personalities** - Define specific behaviors and communication styles
- **Set system prompts** - Specify how the AI should behave in certain contexts
- **Configure model parameters** - Customize temperature, token limits, and other settings
- **Define custom commands** - Create shortcuts for common tasks
- **Integrate with your codebase** - Make the AI aware of your project structure and conventions

### Where to Get Skill Files

Skill files can come from several sources:

#### 1. **Official Documentation**
- Continue: [Continue.dev](https://docs.continue.dev)
- OpenCode: [OpenCode.ai](https://opencode.ai)
- Ollama: [Ollama.com](https://ollama.com)

#### 2. **Community Repositories**
- GitHub repositories that curate skill files for various use cases
- Community-contributed configurations shared on forums and discussion boards
- Package managers like npm or pip that distribute skill packs

#### 3. **Create Your Own**
You can create custom skill files from scratch based on your specific needs.

### How to Use Skill Files

#### For Continue (VS Code)

Skill files are typically stored in your Continue configuration:

1. Open Continue settings: Click the settings icon (⚙️) in the Continue sidebar
2. Edit `config.json` to include custom skill definitions
3. Example custom skill:

```json
{
  "models": [
    {
      "title": "Mistral",
      "provider": "ollama",
      "model": "mistral",
      "apiBase": "http://localhost:11434"
    }
  ],
  "systemPrompt": "You are a helpful Python programmer. Focus on writing clean, readable code with good documentation.",
  "customCommands": [
    {
      "name": "refactor",
      "description": "Refactor the selected code for better readability",
      "prompt": "Please refactor this code to be more readable and maintainable"
    }
  ]
}
```

#### For OpenCode (Terminal)

Edit `~/.config/opencode/opencode.json` to include skill definitions:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      },
      "models": {
        "mistral": {
          "name": "mistral"
        }
      }
    }
  },
  "globalSystemPrompt": "You are an expert programmer who writes clean, well-documented code."
}
```

### Example Skill Files

Here are some example skill file configurations:

**Python Developer Skill:**
```json
{
  "systemPrompt": "You are a Python expert. Focus on PEP 8 standards, type hints, and efficient algorithms.",
  "defaultModel": "mistral"
}
```

**Code Reviewer Skill:**
```json
{
  "systemPrompt": "Review the code for: 1) Security vulnerabilities, 2) Performance issues, 3) Best practices violations, 4) Documentation gaps.",
  "defaultModel": "codellama"
}
```

**Documentation Generator Skill:**
```json
{
  "systemPrompt": "Generate comprehensive documentation including docstrings, comments, and README sections. Use clear examples.",
  "defaultModel": "mistral"
}
```

### Community Skill File Resources

- Check GitHub for "continue-dev-skills" or "opencode-skills" repositories
- Look for Ollama community integrations at [ollama.com/library](https://ollama.com/library)
- Join discussions on Continue and OpenCode community forums for shared configurations

---
