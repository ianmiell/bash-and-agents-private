COURSE RESEARCH NOTES

How does claude use shell to research a codebase? Can  you get a list of shell commands run?

Course submission:
  https://docs.google.com/document/d/1puS896JkDgNtpo41cLRjMpq1qkRvRuXhSRl7w-PllPY/edit?tab=t.0


General
  "AI uses shell as its hands"
  AI uses shell and the command line to quickly inspect things, just like people do
  Shells allow AI to glue processes together
  Shells are very concise - fewer tokens!

The `.claude` folder
  Where all the claude related stuff is. There's one in your home folder, and in each folder you've spun claude up in.
  claude sets the ~/.gitignore file to ignore .claude/settings.local.json files, so it doesn't get added to git

Terminology:
  Agent
    And, specifically a claude agent (in .claude/agents)
  Agentic AI
  Command
    https://code.claude.com/docs/en/commands
    Things beginning with /
    Type / to see commands
    eg a markdown file with instructions, eg 'Review my pull request'
    What's the difference between a command and skill? A command is explicitly called by the user. A skill is dynamically chosen by the LLM and then invoked into the context. Confusingly, a skill can be invoked as a command as well.
  Tool
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
  Hooks
  Monitor
  Skills
    https://support.claude.com/en/articles/12512176-what-are-skills
    A skill can become a command
  Plugins
  Subagents

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

Syllabus:
  1) Create skill in course
  2) Create hook in course
  ) Cover hooks / skills / plugins
  ) How agentic AI uses shell

## PRACTICAL

### Create skill in course

```
cd ~/.claude/skills/
mkdir hellworld
cd helloworld
cat > SKILL.md << EOF
Say hello world
EOF
cd
claude
/helloworld
```

How does a skill get triggered automatically?
  The application internally asks the model which skills look appropriate. If it gets a certain response, it will load up the skill into the context.
  It's not entirely predictable, but you can reduce the risk of failure:
    ❯ say hello
  ⏺ Hello! How can I help you today?
  ✻ Churned for 5s
  ❯ say hello world to me
  ⏺ Skill(helloworld)
    ⎿  Successfully loaded skill

To clear context:

```
/clear
```

To reload skills:

``
/reload
```

Adding scripts:

```
cd ~/.claude/skills/helloworld
mkdir scripts
cd scripts
cat > hello_world.sh << EOF
echo Hello World from scripts
EOF
chmod +x hello_world.sh
cd
claude
say hello world  # Doesn't trigger script
EXIT CLAUDE
cat > ~/.claude/skills/helloworld/SKILL.md << EOF
This skills says hello world. Call the script hello_world.sh if asked to say hello world.
EOF
cd -
claude
say hello world  # Doesn't trigger script - does not find it
cat > ~/.claude/skills/helloworld/SKILL.md << EOF
This skills says hello world. Call the script scripts/hello_world.sh if asked to say hello world.
EOF
```

### Create hook

https://code.claude.com/docs/en/hooks-guide

Add this to ~/.claude/settings

```
  "hooks": {
  "PreToolUse": [
    {
    "matcher": "Bash",
    "hooks": [
      {
      "type": "command",
      "command": "jq -c '. + {logged_at: now | todate}' >> ~/.claude/bash-commands.jsonl"
      }
    ]
    }
  ]
  }
```


Questions:

- What is {logged_at: now | todate} doing?
  - adds the date of logging to the json

- How do you list the existing tools? ('matcher')
  - You can't. There is a reference: https://code.claude.com/docs/en/tools-reference
  - You can see that there is a mapping from shell and command line tools to many tools (Grep, Glob)

- How is data passed to the command?
  - Your hook receives the JSON once on stdin to the command

- How do tools manage permissions?
  - eg: '/clear; lookup the ls man page and give me the most interesting flags' - asks for permission for col -b.
  - .claude/settings.local.json in local folder

- What other hooks are there?
  - https://code.claude.com/docs/en/hooks
  - or /hooks in claude

To log all tool uses:

```
  "hooks": {
  "PreToolUse": [
    {
    "matcher": "*",
    "hooks": [
      {
      "type": "command",
      "command": "jq -c '{tool_name, tool_input, event: .hook_event_name}' >> ~/.claude/all-tools.jsonl"
      }
    ]
    }
  ]
  }
```

in ~/.claude/settings

Worth reading: https://code.claude.com/docs/en/tools-reference

### Create a tool

TODO: Replace with ~/git/ianmiell-mcp-server on klimt

Break down the tool and how it works.

A tool is a command to be run if the agent deems it relevant.
One tool is the 'Skill' tool, which we have already covered.

eg

https://code.claude.com/docs/en/tools-reference



### What is a monitor? Create a montitor

Inbuilt tool. It can watch for things and take actions.

https://code.claude.com/docs/en/tools-reference#monitor-tool

Can this be done as a reproducible? No. But you can create a skill to do it, and it's more or less the same.

#### Create two commands

cat .claude/commands/ok.md
watch for the removal of a file 'asd' in this folder, and when it is created, output 'ok!'

cat .claude/commands/argh.md
watch for the creation of a file 'asd' in this folder, and when it is created, output 'argh!'

Then start claude:

```
/ok
/argh
```

Create and remove the files

```
touch asd
rm asd
```

touch asd ## The monitor only runs once.

### Plugins

- What is a plugin?
  - Plugins package hooks, skills, agents (?), MCP Servers (tools), LSP Servers (Language Server Protocol), Monitors,

Plugins have scopes: user, project, local, managed

Plugins give you a namespace for plugin calls, eg /myplugin:hello

#### Creating a plugin
https://code.claude.com/docs/en/plugins#convert-existing-configurations-to-plugins
