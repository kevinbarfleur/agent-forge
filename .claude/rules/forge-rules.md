# Regles de Generation AgentForge

## Regles Critiques

### 1. Ne jamais ecraser sans confirmation

Avant d'ecrire dans `.claude/`:
- Verifier si le fichier existe
- Si oui, proposer backup ou merge
- Toujours confirmer avant d'ecrire

### 2. Model routing intelligent

| Criticite | Model | Exemples |
|-----------|-------|----------|
| **Critique** | Opus | Architecture, security review, API design |
| **Standard** | Sonnet | Tests, docs, deployment, routine |
| **Trivial** | Haiku | Formatting, simple queries |

Selon [Anthropic best practices](https://www.anthropic.com/engineering/claude-code-best-practices), Haiku 4.5 delivre 90% de la performance de Sonnet a 3x moins cher.

### 3. Tools whitelisting

Chaque agent doit avoir une liste explicite de tools:
- Ne pas laisser `tools: all` par defaut
- Principe du moindre privilege
- Read-only quand possible

### 4. Descriptions riches

Les descriptions d'agents doivent etre detaillees pour le routing automatique:

**Mauvais**: `description: "Helps with testing"`

**Bon**: `description: "Runs unit tests, integration tests, and generates coverage reports. Call when user asks to test code, check test status, or verify coverage."`

### 5. Anti-hallucination

Ne pas generer de features Claude Code qui n'existent pas:
- Verifier la doc officielle si incertain
- Ne pas inventer de syntaxes YAML
- Utiliser les patterns documentes

## Patterns Recommandes

### Structure d'agent

```yaml
---
name: nom-kebab-case
description: Description detaillee pour routing (50-100 mots)
model: sonnet  # ou opus, haiku
tools:
  - Read
  - Grep
  - Glob
---
```

### Structure de commande

```markdown
# /{nom} - Description courte

## Usage
## Workflow
## Output
```

### Model routing dans config.yaml

```yaml
models:
  critical:
    agents: [reviewer, architect]
    model: opus
  operational:
    agents: [test-runner, docs-writer]
    model: sonnet
  quick:
    agents: [formatter]
    model: haiku
```

## Contexte Utilisateur

L'utilisateur est un developpeur experimente avec Claude Code.

Implications:
- Ne pas surestimer les temps de dev
- MVP = 1-2 jours, pas 2-3 mois
- "C'est trop complexe" n'est pas un argument valide
- Focus sur les vrais challenges: architecture, UX, marche
