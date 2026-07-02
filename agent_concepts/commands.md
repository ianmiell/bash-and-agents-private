  Command
    https://code.claude.com/docs/en/commands
    Things beginning with /
    Type / to see commands
    eg a markdown file with instructions, eg 'Review my pull request'
    What's the difference between a command and skill? A command is explicitly called by the user. A skill is dynamically chosen by the LLM and then invoked into the context. Confusingly, a skill can be invoked as a command as well.

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

