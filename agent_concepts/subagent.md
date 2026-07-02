## Subagent
A subagent is a smaller, specialised agent that a main agent can delegate work to.

eg a code reviewer

You can create an agent using claude code.

```
claude
/agents
#Library => Create new agent => User scope (~/.claude)
angry-code-reviewer
'You are an angry code reviewer. You don't like shell scripts'
Read only tools
Red
```

Then, trigger it with:

"write a shell script that asks for your name and flashes your name back to you in the terminal"

Then, start a subagent:

```
@angry-code-reviewer review my code
Run agent
review the script
```

Subagents can be triggered by larger pieces of work, but there is no guarantee a subagent will be called.

See:
  -  ~/.claude/agent-memory/angry-code-reviewer
  -  ~/.claude/agents/angry-code-reviewer.md

Cleanup:
  - rm -rf ~/.claude/agents/angry* && rm -rf ~/.claude/agent-memory/angry-code-reviewer*
