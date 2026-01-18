# AgentForge

I'm the blacksmith. I forge custom Claude Code configurations.

No catalog, no templates. You tell me about your project, I craft tools tailored to your needs. Agents, commands, skills - everything custom-made.

## How it works

1. Come to my forge (open Claude Code in this repo)
2. Tell me about your project - and spare me the marketing pitch
3. I'll ask questions. Some might sting. That's how good tools are made.
4. When you're ready, say `/forge-init`
5. I forge your config in `forged/{date}-{slug}/.claude/`
6. Copy it to your project. Done.

## Usage

```bash
cd agent-forge
claude

# Talk to me. Tell me what you're building.
# I'll dig into what you actually need.

# When ready:
/forge-init
```

## The process

### 1. We talk

You arrive, I start asking questions. No forms, no checkboxes.

- You explain your project
- I challenge what sounds shaky
- We figure out what you actually need

### 2. I forge

When you're ready, `/forge-init`. I craft a complete config based on everything we discussed.

## What you get

```
forged/
├── 2025-01-18-your-project/
│   └── .claude/
│       ├── CLAUDE.md          # Your project's brain
│       ├── agents/            # Specialized workers
│       ├── commands/          # Your shortcuts
│       ├── skills/            # Patterns & knowledge
│       └── rules/             # Guardrails
```

## Using your config

```bash
# Copy to your project
cp -r forged/2025-01-18-your-project/.claude/ /path/to/your/project/

# Open Claude Code there
cd /path/to/your/project
claude

# Your custom commands are ready
```

## What I forge

Everything is invented for YOUR project. Not templates. Not copy-paste.

- **Agents** with roles that match your workflows
- **Commands** for what you do every day
- **Skills** with your patterns and conventions
- **Rules** based on your constraints

## One more thing

I know Claude Code inside out - hooks, MCP servers, sub-agents, the works. So the configs I forge aren't just pretty text. They're architecturally sound.

Now. What are you building?

---

MIT - Kevin Barfleur
