# AgentForge

> Genere une configuration Claude Code complete en 10 minutes.

## Qu'est-ce que c'est?

AgentForge est un "core agentique" - un ensemble d'agents Claude Code qui generent d'autres agents, commandes et skills adaptes a ton projet.

Au lieu de copier-coller des configs entre projets et les adapter manuellement, tu reponds a quelques questions et AgentForge genere tout pour toi.

## Installation

1. Copie le dossier `.claude/` dans ton projet
2. Lance Claude Code
3. Tape `/forge-init`

```bash
# Clone ou telecharge
git clone https://github.com/kevinbarfleur/agent-forge.git

# Copie dans ton projet
cp -r agent-forge/.claude/ /path/to/your/project/
```

## Usage

### Initialisation rapide

```bash
# Mode Express (3 questions, 1-2 min)
/forge-init --express

# Mode interactif
/forge-init
```

### Creer des agents supplementaires

```bash
# Nouvel agent
/forge-agent security-reviewer

# Modifier un agent
/forge-agent reviewer --edit
```

### Creer des commandes

```bash
# Nouvelle commande
/forge-command deploy

# Utiliser un template
/forge-command ci --template test
```

## Modes de configuration

| Mode | Questions | Duree | Pour qui |
|------|-----------|-------|----------|
| **Express** | 3 | 1-2 min | Setup rapide, config standard |
| **Light** | 5-10 | 5 min | Personnalisation basique |
| **Deep** | 20-30 | 15-20 min | Configuration complete |

## Ce qui est genere

```
.claude/
├── CLAUDE.md              # Instructions principales
├── agents/
│   ├── reviewer.md        # Code review
│   ├── test-runner.md     # Tests
│   └── {custom}.md        # Tes agents
├── commands/
│   ├── test.md
│   ├── deploy.md
│   └── {custom}.md
└── rules/
    └── {domain}.md
```

## Templates disponibles

| Template | Description | Agents |
|----------|-------------|--------|
| `saas` | Application SaaS | reviewer, test-runner, deploy |
| `cli` | Outil CLI | cli-architect, docs-writer |
| `lib` | Bibliotheque npm | api-designer, test-runner |
| `general` | Minimal | reviewer |

## Model Routing

AgentForge configure automatiquement le model routing optimal:

| Model | Usage | Cout relatif |
|-------|-------|--------------|
| **Opus** | Decisions critiques (architecture, security) | $$$ |
| **Sonnet** | Execution standard (tests, docs) | $$ |
| **Haiku** | Taches simples (formatting) | $ |

## License

MIT

## Auteur

Kevin Barfleur - [@kbarfleur](https://twitter.com/kbarfleur)

---

Built with Claude Code.
