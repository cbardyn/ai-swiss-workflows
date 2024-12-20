<div align="center">
  <h1>AI Workflows Framework</h1>
  <p><i>Turn your text instructions into Python code</i></p>
</div>

## What This Framework Does

This framework helps you convert text-based AI workflows into Python code. It:
- Takes your instructions (as a YAML file)
- Sets up the AI tools you choose
- Runs your tasks in sequence
- Saves results as files

## Quick Example

```python
from ai_workflows import Workflow

# Create a workflow from your instructions
workflow = Workflow(
    config_path='config.yaml',      # Your AI tools configuration
    instructions_path='tasks.yaml'  # Your workflow instructions
)

# Run it!
result = workflow.run()
```

## Core Components

### 1. Instructions File (tasks.yaml)
Define what you want to do:
```yaml
goal: "Analyze customer feedback"
tasks:
  - key: 'extract_topics'
    description: 'Find main topics in feedback'
  - key: 'analyze_sentiment'
    description: 'Analyze sentiment per topic'
```

### 2. Config File (config.yaml)
Choose your AI tools:
```yaml
llm:
  type: "langchain_groq.ChatGroq"
  model_name: "llama-3.3-70b-versatile"

embeddings:
  type: "langchain_huggingface.HuggingFaceEmbeddings"
  model_name: "all-MiniLM-L6-v2"
```

## Installation

1. **Requirements**
   - Python 3.10
   - Poetry (package manager)

2. **Set Up**
   ```bash
   # Get the code
   git clone https://github.com/cbardyn/ai-swiss-workflows
   cd _ai_workflows_packages/ai_workflows

   # Install dependencies
   poetry install

   # Activate environment
   source .venv/bin/activate  # (or .\.venv\Scripts\activate on Windows)
   ```

3. **Configure**
   ```bash
   # Add your API key
   echo "GROQ_API_KEY=your-key-here" > .env
   ```

## How to Use

### 1. Write Your Instructions
Create `tasks.yaml`:
```yaml
goal: "Your workflow goal"
tasks:
  - key: 'task_1'
    description: 'What to do'
    inputs:
      - from_context: ['some_file']
    outputs:
      - key: 'result'
        file: 'output.md'
```

### 2. Configure AI Tools
Create `config.yaml`:
```yaml
llm:
  type: "langchain_groq.ChatGroq"
  model_name: "llama-3.3-70b-versatile"
  temperature: 0  # More precise answers
```

### 3. Run Your Workflow
```python
from ai_workflows import setup_logging, Workflow

# Set up logging (optional but helpful)
setup_logging()

# Create and run workflow
workflow = Workflow('config.yaml', 'tasks.yaml')
result = workflow.run()
```

## Framework Features

### Smart Context Management
```python
# The framework automatically:
# - Loads files and URLs
# - Creates searchable vector database
# - Finds relevant information for each task
```

### Task Orchestration
```python
# The framework handles:
# - Task sequencing
# - Information passing between tasks
# - Progress tracking
```

### Error Handling
```python
# Built-in handling for:
# - Missing files
# - API failures
# - Invalid configurations
```

## Missing Features That We'd Like to Add

- More connectors to external systems (Dropbox, Google Drive, etc.)
- Better testing: No automated tests yet to ensure everything works perfectly
- Better security: API keys are stored in simple text files
- Better performance: Tasks run one after another instead of in parallel
- Better reliability: No backup AI models if the main one fails
- Better data safety: No automatic backups of your data
- Better monitoring: Can't track how well the system performs
- And more!

---

<div align="center">
  <sub>Built with ❤️ by AI Swiss</sub>
</div>