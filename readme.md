# LangChain Currency Converter Agent

This repository features an intelligent AI agent built using **LangChain** and **HuggingFace** (`meta-llama/Llama-3.1-8B-Instruct`) [cite: 1]. It handles real-time foreign currency conversions [cite: 1]. The agent dynamically interacts with the ExchangeRate-API to retrieve live conversion factors and perform precise numerical calculations via custom functional tools [cite: 1]. 

By binding custom `@tool` functions to the LLM, the model detects when currency conversion data is missing and invokes appropriate code structures seamlessly [cite: 1]. It showcases both manual LangChain tool orchestration and automated execution using a unified agent workflow (`create_agent`) [cite: 1].

---

## Technical Features
* **LLM Engine:** Hosted HuggingFaceEndpoint running Llama-3.1-8B-Instruct [cite: 1].
* **Tool Binding:** Seamless attachment of Python utility functions directly to the LLM interface using `model.bind_tools()` [cite: 1].
* **Real-time Data:** Live currency exchange calculations via external API fetches [cite: 1].
* **Agent Architecture:** Modular workflow utilizing `create_agent` for interactive conversational cycles [cite: 1].

---

## Installation & Setup

1. **Install Dependencies:**
   ```bash
   pip install langchain-openai langchain-core requests langchain-huggingface
   ```

2. **Set API Tokens:**
   Configure your Hugging Face access token environment variable before runtime:
   ```python
   import os
   os.environ["HUGGINGFACEHUB_API_TOKEN"] = "your_hf_token"
   ```

---

## Code Overview & Architecture

### 1. Custom Tool Definitions
The agent leverages two primary tool functions decorated with LangChain’s `@tool` wrapper:
* `get_conversion_factor(base, target)`: Fetches current pair rates from ExchangeRate-API [cite: 1].
* `convert(base_value, conversion_rate)`: Computes final valuations using injected argument structures [cite: 1].

### 2. Manual Invocation Framework
Tracks the standard interaction structure where the LLM flags necessary `tool_calls`, triggers Python processing routines locally, appends individual `ToolMessage` payloads, and generates final text output [cite: 1].

### 3. Automated Agent Framework
Implements standard agent execution paths [cite: 1]:
```python
from langchain.agents import create_agent

agent_executor = create_agent(
    model=model,
    tools=[get_conversion_factor, convert]
)
```
