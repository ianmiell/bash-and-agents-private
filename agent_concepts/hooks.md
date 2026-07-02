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

