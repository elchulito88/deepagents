# Deep Agents CLI - Local Setup Guide (macOS)

This guide will help you set up and run the Deep Agents CLI locally on macOS.

## Prerequisites

- macOS (Apple Silicon or Intel)
- Python 3.11 or higher
- Git

## Installation Steps

### 1. Clone and Navigate to Repository

```bash
cd ~/Desktop/deepagents  # Or wherever you cloned the repo
```

### 2. Install Deep Agents Packages

```bash
# Install the core deepagents library
pip install -e .

# Install the CLI in editable/development mode
pip install -e libs/deepagents-cli
```

This installs the CLI with all dependencies and makes the `deepagents` command available.

### 3. Choose Your Model Provider

You have three options: **Ollama (Local/Free)**, **OpenAI**, or **Anthropic**. Choose one:

---

## Option A: Ollama (Recommended for Local/Free Development)

### Install Ollama

1. Download Ollama from [https://ollama.ai](https://ollama.ai)
2. Install the macOS app (drag to Applications folder)
3. Ollama will start automatically on launch

### Pull a Model

```bash
# Recommended for coding tasks
ollama pull qwen2.5-coder:14b

# Other options:
ollama pull qwen2.5-coder:7b    # Faster, smaller
ollama pull llama3.1:8b          # Good general purpose
ollama pull mistral:latest       # Balanced performance
```

### Verify Installation

```bash
ollama list
```

You should see your downloaded models listed.

### Configure Environment Variables

Create a `.env` file in the project root:

```bash
# .env
OLLAMA_BASE_URL=http://localhost:11434
OLLAMA_MODEL=qwen2.5-coder:14b
```

**OR** export environment variables in your shell:

```bash
export OLLAMA_BASE_URL=http://localhost:11434
export OLLAMA_MODEL=qwen2.5-coder:14b
```

To make these permanent, add to your `~/.zshrc` (or `~/.bash_profile`):

```bash
echo 'export OLLAMA_BASE_URL=http://localhost:11434' >> ~/.zshrc
echo 'export OLLAMA_MODEL=qwen2.5-coder:14b' >> ~/.zshrc
source ~/.zshrc
```

---

## Option B: OpenAI

### Get API Key

1. Sign up at [https://platform.openai.com](https://platform.openai.com)
2. Go to API Keys section
3. Create a new API key

### Configure Environment Variables

Create a `.env` file in the project root:

```bash
# .env
OPENAI_API_KEY=your_api_key_here
OPENAI_MODEL=gpt-4o  # Optional, defaults to gpt-5-mini
```

**OR** export in your shell:

```bash
export OPENAI_API_KEY=your_api_key_here
export OPENAI_MODEL=gpt-4o
```

---

## Option C: Anthropic (Claude)

### Get API Key

1. Sign up at [https://console.anthropic.com](https://console.anthropic.com)
2. Go to API Keys section
3. Create a new API key

### Configure Environment Variables

Create a `.env` file in the project root:

```bash
# .env
ANTHROPIC_API_KEY=your_api_key_here
ANTHROPIC_MODEL=claude-sonnet-4-5-20250929  # Optional
```

**OR** export in your shell:

```bash
export ANTHROPIC_API_KEY=your_api_key_here
export ANTHROPIC_MODEL=claude-sonnet-4-5-20250929
```

---

## Running the CLI

Once you've completed installation and configuration:

```bash
deepagents
```

You should see a welcome message and the model you're using:

```
 ██████╗  ███████╗ ███████╗ ██████╗
 ██╔══██╗ ██╔════╝ ██╔════╝ ██╔══██╗
 ██║  ██║ █████╗   █████╗   ██████╔╝
 ██║  ██║ ██╔══╝   ██╔══╝   ██╔═══╝
 ██████╔╝ ███████╗ ███████╗ ██║
 ╚═════╝  ╚══════╝ ╚══════╝ ╚═╝

  █████╗   ██████╗  ███████╗ ███╗   ██╗ ████████╗ ███████╗
 ██╔══██╗ ██╔════╝  ██╔════╝ ████╗  ██║ ╚══██╔══╝ ██╔════╝
 ███████║ ██║  ███╗ █████╗   ██╔██╗ ██║    ██║    ███████╗
 ██╔══██║ ██║   ██║ ██╔══╝   ██║╚██╗██║    ██║    ╚════██║
 ██║  ██║ ╚██████╔╝ ███████╗ ██║ ╚████║    ██║    ███████║
 ╚═╝  ╚═╝  ╚═════╝  ╚══════╝ ╚═╝  ╚═══╝    ╚═╝    ╚══════╝

Using Ollama model: qwen2.5-coder:14b at http://localhost:11434
```

## Available Commands

Once inside the CLI:

- `/help` - Show help information
- `/tokens` - Show token usage for current session
- `/clear` - Clear screen and reset conversation
- `/quit` or `/exit` - Exit the CLI

## Troubleshooting

### "No API key or Ollama configuration found"

Make sure you've set the environment variables. Check:

```bash
echo $OLLAMA_BASE_URL
echo $OLLAMA_MODEL
```

If empty, your `.env` file isn't being loaded or environment variables aren't set.

### "ModuleNotFoundError: No module named 'deepagents'"

Run the installation commands again:

```bash
pip install -e .
pip install -e libs/deepagents-cli
```

### Ollama "Connection refused"

Make sure Ollama is running:

```bash
ollama list
```

If it fails, restart Ollama from Applications or run:

```bash
ollama serve
```

### Model not found

Pull the model:

```bash
ollama pull qwen2.5-coder:14b
```

## Model Priority

The CLI checks for models in this order:

1. **OpenAI** (if `OPENAI_API_KEY` is set)
2. **Anthropic** (if `ANTHROPIC_API_KEY` is set)
3. **Ollama** (if `OLLAMA_BASE_URL` is set)

**⚠️  Note**: Ollama models have limited tool-calling reliability. OpenAI and Anthropic are recommended for production use.

To ensure a specific provider is used, only set environment variables for that provider.

## Performance Tips (Ollama)

- **Larger models (14b+)**: Better quality, slower, requires 16GB+ RAM
- **Smaller models (7b)**: Faster, good for most tasks, 8GB+ RAM
- **GPU acceleration**: Automatic on Apple Silicon (M1/M2/M3)
- **Temperature**: Lower values (0.1-0.3) for deterministic code generation

## Example Usage

### Using Ollama Locally

```bash
# Terminal 1: Make sure Ollama is running
ollama list

# Terminal 2: Start Deep Agents
export OLLAMA_BASE_URL=http://localhost:11434
export OLLAMA_MODEL=qwen2.5-coder:14b
deepagents
```

Then ask the agent:
```
> Write a Python function to calculate fibonacci numbers
```

### Using with .env file (Recommended)

```bash
# Create .env file once
cat > .env << 'EOF'
OLLAMA_BASE_URL=http://localhost:11434
OLLAMA_MODEL=qwen2.5-coder:14b
EOF

# Just run deepagents (reads .env automatically)
deepagents
```

## Updating the CLI

When you make changes to the code:

```bash
# The CLI is installed in editable mode, so changes are reflected immediately
# Just restart the CLI to see your changes
deepagents
```

## Additional Resources

- **Ollama Documentation**: [OLLAMA.md](OLLAMA.md)
- **Development Workflow**: [WORKFLOW.md](WORKFLOW.md)
- **Main Documentation**: [README.md](README.md)
