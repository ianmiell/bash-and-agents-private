## CORSE STRUCTURE
How does claude use shell to research a codebase? Can  you get a list of shell commands run?

TODO look at these suggestions:
  - I believe things like NVIDIA’s OpenShell, and their secure sandbox approach to agents might be worth covering?
  - Can recommend to look at Wave, I moved from my Alacritty/tmux setup and very much enjoy it
  - language servers (LSP)
  - Task scheduling is a good one - my agents lean on `atd` pretty hard and cron for other things, I like both better than the built-in scheduling tooling which I have poor visibility into and can't modify without a chat. Also I'd be sure to discuss the value of a pre-flight api health check hook and configuring fallback models.

Course submission:
  https://docs.google.com/document/d/1puS896JkDgNtpo41cLRjMpq1qkRvRuXhSRl7w-PllPY/edit?tab=t.0




### General comments
  "AI uses shell as its hands"
  AI uses shell and the command line to quickly inspect things, just like people do
  Shells allow AI to glue processes together
  Shells are very concise - fewer tokens!
  Focussing on Claude

### Other
You can run commands with `shell command`
It burns tokens (obvs) and takes longer though!

#### High Level Concepts
LLM
  The 'thing' that takes input (context) and produces output (simple view - internals of LLMs can get much more complex)
Agent
  Program that manages input and output to an LLM
  It's just a program. The program manages how the LLM is called and what to do with its outputs.
  But these programs follow certain patterns (which brings us to other agent concepts).
  And, specifically a claude agent (in .claude/agents)
  How the agent does this is its secret sauce (if it's not open source). It might add data to your "prompt" before it dispatches is to the LLM.
Agentic AI
  TODO
Harness
  Agent = LLM + Harness

#### Agent Concepts (covered in own sections)
commands.md
hooks.md
monitors.md
plugins.md
skills.md
subagent.md
tools.md

Any more terminology of interest?

- LLM Architectures:
    https://medium.com/@damianvtran/the-anatomy-of-a-modern-llm-0347afd72514
    https://magazine.sebastianraschka.com/p/the-big-llm-architecture-comparison
    https://sebastianraschka.com/llm-architecture-gallery/
  Not covered here, but interesting

### Shell and Agents
The `.claude` folder
  Where all the claude related stuff is. There's one in your home folder, and in each folder you've spun claude up in.
  claude sets the ~/.gitignore file to ignore .claude/settings.local.json files, so it doesn't get added to git

Data preparation:
  Uses fiddly commands to carry out user demands, eg:
    sed
    awk
    find

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


Links:
  https://claude.com/blog/how-claude-code-works-in-large-codebases-best-practices-and-where-to-start
  https://joe.dev/posts/nine-kinds-of-agents/
