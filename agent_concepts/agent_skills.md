Agent Skills => Depends on skills.md and subagents.md


  Agent Skills
    https://agentskills.io/home
    An agent skill is a skill specifically designed to be used by a Claude sub-agent (or specialized agent) when Claude delegates a task.
    Where a command is a reusable prompt, and a skill is reusable knowledge, an agent is a reusable role with its own instructions, responsibilities, and boundaries.
    An agent file is usually a Markdown document describing:
      what the agent is responsible for
      what it should focus on
      what it should ignore
      how it should report findings
    When you ask:
      Why is my MCP server not connecting?
      Claude might decide:
        This looks like an MCP problem. I'll delegate analysis to the mcp-expert agent.
    eg create an agent in the mcp server
