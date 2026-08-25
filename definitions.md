#### High Level Concepts
LLM
  The 'thing' that takes input (context) and produces output (simple view - internals of LLMs can get much more complex)
Harness
  Program that manages input and output to an LLM
  It's just a program. The program manages how the LLM is called and what to do with its outputs.
  But these programs follow certain patterns (which brings us to other agent concepts).
Agent
  Agent = LLM + Harness
  How the agent does this is its secret sauce (if it's not open source). It might add data to your "prompt" before it dispatches is to the LLM or decide to run a script - it often uses shell to achieve its goals.
  Specifically a claude agent (in .claude/agents)
Agentic AI
  AI that can pursue a goal by independently deciding what actions to take, using tools, observing the results, and adapting its approach—often across multiple steps—with limited human direction.
Tools
  LLMs ask for the harness to run a tool using JSON
  eg for a weather tool, tool is defined as:
    ```
    {
      "name": "weather",
      "description": "Get the current weather",
      "parameters": {
        "location": {"type": "string"}
      }
    }
    ```
  Example call and response:
    ```
    {
      "name": "get_weather",
      "arguments": {
        "location": "London",
        "units": "celsius"
      }
    }

    {
      "temperature": 18,
      "conditions": "light rain"
    }
    ```
  Harness executes and returns json. That JSON is then interpreted by the LLM into a human response.
  Agent tells the LLM through context what tools are available.
  Tools can be internal (to claude) and external (MCP Server)
    internal: https://code.claude.com/docs/en/tools-reference
  'Skill' is an internal tool designed to execute skills where needed.

Commands

Hooks

Plugins

Skills

Subagent
