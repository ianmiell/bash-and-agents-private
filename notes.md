## COURSE STRUCTURE

"In this course with Ian Miell, developers and technical practitioners will learn how AI coding agents use shell and command-line tools in real work and how Claude Code uses tools, commands, skills, hooks, plug-ins, subagents, and monitors. Through live demonstrations and practical exercises, you’ll create a simple skill, add a script to that skill, configure hooks to log shell and tool use, and examine the security implications of allowing an AI agent to execute commands."

Course submission:
  https://docs.google.com/document/d/1puS896JkDgNtpo41cLRjMpq1qkRvRuXhSRl7w-PllPY/edit?tab=t.0

Presentation:
  https://docs.google.com/presentation/d/1oXzgPDM7NVjt3ePTac_iplPZiemizh4z0pMSqlHmF74

### General comments
  "AI uses shell as its hands"
  AI uses shell and the command line to quickly inspect things, just like people do
  Shells allow AI to glue processes together
  Shells are very concise - fewer tokens!
  Focussing on Claude

### Other
You can run commands with `shell command`
It burns tokens (obvs) and takes longer though!

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

JSON:
  How AI uses JSON under the hood
  jq .
  AI tools often produce fragments: a command, a script, a file, a config, a report, a test run. Shell scripting turns those fragments into repeatable workflows.
  UNIX principle - building tools together

### Links:
  https://claude.com/blog/how-claude-code-works-in-large-codebases-best-practices-and-where-to-start
  https://joe.dev/posts/nine-kinds-of-agents/
