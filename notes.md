## COURSE STRUCTURE

"In this course with Ian Miell, developers and technical practitioners will learn how AI coding agents use shell and command-line tools in real work and how Claude Code uses tools, commands, skills, hooks, plug-ins, subagents, and monitors. Through live demonstrations and practical exercises, you’ll create a simple skill, add a script to that skill, configure hooks to log shell and tool use, and examine the security implications of allowing an AI agent to execute commands."

Questions answered:

- How does claude use shell to research a codebase?
- Can you get a list of shell commands run?

TODO look at these suggestions:
  - I believe things like NVIDIA’s OpenShell, and their secure sandbox approach to agents might be worth covering?
  - Can recommend to look at Wave, I moved from my Alacritty/tmux setup and very much enjoy it
  - language servers (LSP)
  - Task scheduling is a good one - my agents lean on `atd` pretty hard and cron for other things, I like both better than the built-in scheduling tooling which I have poor visibility into and can't modify without a chat. Also I'd be sure to discuss the value of a pre-flight api health check hook and configuring fallback models.

Course submission:
  https://docs.google.com/document/d/1puS896JkDgNtpo41cLRjMpq1qkRvRuXhSRl7w-PllPY/edit?tab=t.0

## PROPOSED STRUCTURE

- Definitions
  - `definitions.md`
- Context engineering
  - `context_engineering/context_engineering.md`
- Command design for agents
  - `command_design/command_design.md`
- Skill creation
  - `agent_concepts/skills.md`
- Monitors / commands etc
  - Monitors and shell concepts (bg / fg etc)
  - Hooks for logging
- Security
  - `security/security.md`

SUGGESTIONS:
Ask an agent to explain an unfamiliar repository and reconstruct its search process.
Put malicious prompt-injection text in a repository.

### General comments
  "AI uses shell as its hands"
  AI uses shell and the command line to quickly inspect things, just like people do
  Shells allow AI to glue processes together
  Shells are very concise - fewer tokens!
  Focussing on Claude

### Other
You can run commands with `shell command`
It burns tokens (obvs) and takes longer though!

#### Agent Concepts (covered in own sections)

```
agent_concepts/commands.md
agent_concepts/hooks.md
agent_concepts/monitors.md
agent_concepts/plugins.md
agent_concepts/skills.md
agent_concepts/subagent.md
agent_concepts/tools.md
```

Any more terminology of interest?

#### LLM Architectures:
    https://medium.com/@damianvtran/the-anatomy-of-a-modern-llm-0347afd72514
    https://magazine.sebastianraschka.com/p/the-big-llm-architecture-comparison
    https://sebastianraschka.com/llm-architecture-gallery/
  Not covered here, but interesting

### Shell and Agents
The `.claude` folder
  Where all the claude related stuff is. There's one in your home folder, and in each folder you've spun claude up in.
  claude sets the ~/.gitignore file to ignore .claude/settings.local.json files, so it doesn't get added to git

Searching
  grep / rg
  find / fd

Data preparation:
  Uses fiddly commands to carry out user demands, eg:
    sed
    awk

API calling commands:
  az
  aws
  gcloud
  Docker
  kubectl
  terraform
  helm

What to do if you are being asked to run a command?
  Security risks
    How do permissions work?
      https://llmgame.scalex.dev/
      https://scalex.dev/blog/ai-agent-permissions/
      How do you know which commands are a problem?
    Attack vectors
      Changing PATH
      Injection

JSON:
  How AI uses JSON under the hood
  jq .
  AI tools often produce fragments: a command, a script, a file, a config, a report, a test run. Shell scripting turns those fragments into repeatable workflows.
  UNIX principle - building tools together

Environments:
  Browser
  Desktop Application
  Command Line
  operates in directory context

### Security implications


### Suggestion (from AI)
Follow a cycle:

User request
    ↓
Gather context
    ↓
Choose tools and commands
    ↓
Execute
    ↓
Inspect output
    ↓
Update plan
    ↓
Repeat or report

```
pwd
find .
rg "auth|login|token"
sed -n '1,200p' src/auth.py
git diff
pytest tests/test_auth.py
```

“Find where authentication is implemented, explain it, make a small change, run the relevant tests.”

See suggestion.md for more.

1. What an agent actually is
2. Bash as the agent’s interface to context
3. How agents investigate codebases
4. Files, search and controlled context
5. Pipes, JSON and composition
6. Exit codes, errors and verification
7. Git-based safety and recovery
8. Permissions, secrets and sandboxing
9. Prompt injection and hostile environments
10. Hooks, logs and observability
11. Skills, commands, tools, MCP and LSP
12. Subagents, processes and concurrency
13. Scheduling and unattended agents
14. Cost, performance and model selection
15. Turning agent work into reproducible automation
16. Final exercise: inspect, modify, test and audit a repository



### Links:
  https://claude.com/blog/how-claude-code-works-in-large-codebases-best-practices-and-where-to-start
  https://joe.dev/posts/nine-kinds-of-agents/
