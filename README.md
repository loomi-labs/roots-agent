# roots agent skills

roots is a family-tree app. A tree holds persons, families, events, places, sources and files. An AI agent reads and changes a tree through the MCP server of a roots instance. This repository holds the skills that teach an agent how to do it.

## Install in Claude Code

```
/plugin marketplace add loomi-labs/roots-agent
/plugin install roots@roots
```

Claude Code asks for the MCP URL of your instance, for example `https://roots.example/mcp`. The page `/agents` of your instance shows it.

Do not also add the server by hand with the same name `roots`.

## Install one skill by hand

Download the ZIP of a skill from your instance and unpack it:

```
curl -fsSL https://roots.example/skills/roots-start.zip -o roots-start.zip && unzip roots-start.zip -d ~/.claude/skills/
```

## Upload to claude.ai

Open Customize › Skills and upload the ZIP of a skill.

## Skills

| Skill | Scope | Purpose |
|---|---|---|
| `roots-start` | write | Fill an empty tree |
| `roots-research` | research | The research loop |
| `roots-transcribe` | research (optional write step) | Read a scan |
