# LangChain Test Project

This repository contains various Jupyter notebooks demonstrating different aspects of LangChain functionality, including basic usage, sequential chains, and tool integration.

## Prerequisites

- Python 3.8+
- OpenAI API key
- Required packages (installed via pip in each notebook)

## Setup

1. Clone this repository
2. Set up your OpenAI API key as an environment variable or provide it when prompted in the notebooks
3. Run the notebooks in your preferred Jupyter environment

## Notebooks Overview

### 1. `langchain_test.ipynb`
**Basic LangChain Setup and Usage**

This notebook demonstrates the fundamental setup and basic usage of LangChain with OpenAI models.

**Key Features:**
- Installing LangChain with OpenAI support
- Setting up environment variables for API keys
- Initializing chat models
- Basic model invocation

**Usage:**
```python
from langchain.chat_models import init_chat_model
model = init_chat_model("gpt-4o-mini", model_provider="openai")
model.invoke('Hello world')
```

### 2. `simple_sequential_chain.ipynb`
**Prompt Templates and Chain Operations**

This notebook explores prompt templates and chaining operations in LangChain.

**Key Features:**
- Creating and using prompt templates
- Chaining prompts with language models
- Multi-parameter prompt templates
- Translation examples

**Usage:**
```python
from langchain_core.prompts import PromptTemplate
prompt = PromptTemplate.from_template("Translate this sentence from English to French. Sentence: {text}")
chain = prompt | llm
```

### 3. `simple_tools.ipynb`
**Tool Integration and Agents**

This notebook demonstrates how to create custom tools and integrate them with LangChain agents.

**Key Features:**
- Creating custom tools using the `Tool` class
- Setting up agents with tool capabilities
- Zero-shot React description agent
- Tool execution and reasoning

**Usage:**
```python
from langchain_core.tools import Tool
from langchain.agents import initialize_agent, AgentType

double_tool = Tool(
    name="Double",
    description="Double the input number",
    func=lambda num : double(int(num))
)

agent = initialize_agent(
    [double_tool],
    llm,
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)
```

## Running the Notebooks

1. **Start with `langchain_test.ipynb`** - Basic setup and model initialization
2. **Move to `simple_sequential_chain.ipynb`** - Learn about prompt templates and chains
3. **Explore `simple_tools.ipynb`** - Understand tool integration and agent behavior

## Dependencies

Each notebook installs its own dependencies, but the main packages include:

- `langchain-openai` - OpenAI integration for LangChain
- `langchain` - Core LangChain functionality
- `getpass` - Secure password/API key input
- `os` - Environment variable management

## API Key Setup

All notebooks include secure API key setup using `getpass`:

```python
import getpass
import os

if not os.environ.get("OPENAI_API_KEY"):
    os.environ["OPENAI_API_KEY"] = getpass.getpass("")
```

## Notes

- All notebooks use `gpt-4o-mini` as the default model
- The tools notebook includes verbose output for debugging agent reasoning
- Temperature is set to 0 for deterministic outputs in the tools example

## Contributing

Feel free to add more notebooks demonstrating different LangChain features such as:
- Memory and conversation handling
- Custom chains
- Vector stores and retrieval
- Advanced agent types
- Streaming responses

## License

This project is for educational and testing purposes.
