  Skills
    https://support.claude.com/en/articles/12512176-what-are-skills
    A skill can become a command

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

