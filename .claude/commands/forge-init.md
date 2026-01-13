# /forge-init - Initialiser la configuration Claude Code

## Usage

- `/forge-init` - Lance le questionnaire interactif
- `/forge-init --express` - Mode rapide (3 questions)
- `/forge-init --template {saas|cli|lib}` - Utilise un template predetermine

## Description

Cette commande lance le processus de configuration AgentForge. Elle:
1. Detecte le contexte du projet (stack, structure)
2. Pose des questions pour comprendre les besoins
3. Genere une configuration `.claude/` complete

## Workflow

### 1. Detection automatique

Avant de poser des questions, analyser le projet:

```bash
# Detecter la stack
- package.json -> Node.js/TypeScript
- Cargo.toml -> Rust
- go.mod -> Go
- requirements.txt -> Python

# Detecter le type
- src/app/ ou pages/ -> SaaS/Web app
- src/cli/ ou bin/ -> CLI tool
- src/lib/ -> Library

# Detecter les patterns
- .github/workflows/ -> CI/CD existe
- tests/ ou __tests__/ -> Tests existent
- docker-compose.yml -> Containerise
```

### 2. Proposition de mode

Utiliser l'agent `forge-orchestrator` pour:

```
Bienvenue dans AgentForge!

J'ai detecte:
- Stack: {detected}
- Type: {detected}
- Tests: {oui/non}

Quel mode de configuration?

1. Express (1-2 min) - 3 questions, config standard
2. Light (5 min) - Personnalisation basique
3. Deep (15-20 min) - Configuration complete
```

### 3. Collecte des reponses

Deleguer a `forge-orchestrator` selon le mode choisi.

### 4. Generation

Deleguer a `forge-generator` avec le contexte collecte.

### 5. Confirmation

Afficher ce qui va etre genere et demander confirmation AVANT d'ecrire.

## Options

| Option | Description |
|--------|-------------|
| `--express` | Skip le choix de mode, utilise Express |
| `--template {nom}` | Utilise un template sans questions |
| `--dry-run` | Montre ce qui serait genere sans ecrire |
| `--force` | Ecrase la config existante sans backup |

## Exemples

```bash
# Standard - questionnaire interactif
/forge-init

# Rapide - juste 3 questions
/forge-init --express

# Template direct
/forge-init --template saas

# Preview sans ecrire
/forge-init --dry-run
```

## Output

Apres generation:

```
## AgentForge - Configuration terminee

Fichiers crees:
- .claude/CLAUDE.md
- .claude/agents/reviewer.md
- .claude/agents/test-runner.md
- .claude/commands/test.md

Model routing:
- Opus: reviewer (decisions critiques)
- Sonnet: test-runner (execution)

Prochaines etapes:
1. Relance Claude Code pour charger la config
2. /help pour voir les commandes disponibles
3. /test pour lancer les tests

Besoin de modifier? /forge-agent {nom} ou /forge-command {nom}
```

## Notes

- La configuration existante est backupee dans `.claude.backup/` si elle existe
- Les fichiers generes sont commentes pour expliquer leur role
- Utilise `/forge-explain` pour une explication detaillee de chaque fichier
