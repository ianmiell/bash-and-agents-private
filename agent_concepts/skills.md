## Skills
    https://support.claude.com/en/articles/12512176-what-are-skills

### Walkthrough

```
cd ~/git/bash-and-agents-project
git switch 1-helloworld-simple
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
cd ~/git/bash-and-agents-project
git switch 2-helloworld-script
```

If a skill is not 'chosen' by the harness, you can call it as a 'Command'

```
/helloworld
```
