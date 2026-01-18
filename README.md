# AgentForge

Custom Claude Code configuration generator.

## How it works

1. Open Claude Code in this repo
2. Talk about your project (free brainstorming)
3. When ready, run `/forge-init`
4. A config is generated in `forged/{date}-{slug}/.claude/`
5. Copy that folder to your project

## Usage

```bash
# Open Claude Code in this repo
cd agent-forge
claude

# Talk about your project...
# "I want to build a billing SaaS for freelancers"
# "It's Next.js with Supabase and Stripe"
# etc.

# When you're ready
/forge-init
```

## The flow

### 1. Brainstorming (default)

When you arrive, Claude starts a conversation. No robotic questionnaire.

- You explain your project
- Claude asks questions, challenges your ideas
- You discuss freely

### 2. Generation (/forge-init)

When ready, run `/forge-init`. Claude generates a complete config based on the entire exchange.

## Output

```
forged/
├── 2025-01-13-my-saas/
│   └── .claude/
│       ├── CLAUDE.md
│       ├── agents/
│       │   ├── payment-guardian.md
│       │   └── data-architect.md
│       ├── commands/
│       │   ├── deploy.md
│       │   └── fix.md
│       ├── skills/
│       │   └── stripe-patterns/
│       └── rules/
│           └── security.md
├── 2025-01-14-cli-tool/
│   └── .claude/
│       └── ...
```

## Using a generated config

```bash
# Copy to your project
cp -r forged/2025-01-13-my-saas/.claude/ /path/to/your/project/

# Run Claude Code in your project
cd /path/to/your/project
claude

# Your commands are available
/deploy
/fix
```

## What gets generated

Files are NOT templates. Claude invents everything specifically for your project:

- **Agents** with roles tailored to your needs
- **Commands** for your daily workflows
- **Skills** with your project's patterns
- **Rules** based on your constraints

## License

MIT - Kevin Barfleur
