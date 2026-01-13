# /forge-agent - Creer ou modifier un agent

## Usage

- `/forge-agent {nom}` - Cree un nouvel agent
- `/forge-agent {nom} --edit` - Modifie un agent existant
- `/forge-agent --list` - Liste les agents disponibles

## Description

Cree un nouvel agent Claude Code adapte au projet. L'agent sera cree dans `.claude/agents/{nom}.md`.

## Workflow

### 1. Si nouvel agent

Poser les questions essentielles:

```
Creation de l'agent: {nom}

1. Quel est le role de cet agent?
   (ex: "Review le code pour la securite", "Gere les deployments")

2. Quand doit-il etre appele?
   (ex: "Quand l'utilisateur demande une review", "Avant chaque deploy")

3. Quels outils a-t-il besoin?
   [ ] Read - Lire des fichiers
   [ ] Write - Ecrire des fichiers
   [ ] Edit - Modifier des fichiers
   [ ] Bash - Executer des commandes
   [ ] Grep - Rechercher dans le code
   [ ] Glob - Trouver des fichiers
   [ ] WebSearch - Rechercher sur le web

4. Quel modele?
   - Opus (decisions critiques, architecture)
   - Sonnet (execution, taches standard)
   - Haiku (taches simples, rapides)
```

### 2. Generation

Creer le fichier avec le template:

```markdown
---
name: {nom}
description: {description pour routing automatique}
model: {model choisi}
tools:
  - {tools selectionnes}
---

# {Nom de l'Agent}

{Role et contexte}

## Quand utiliser cet agent

{Triggers detectes automatiquement par Claude}

## Workflow

1. {etape 1}
2. {etape 2}
...

## Output attendu

{Format de sortie}

## Regles specifiques

{Contraintes et limites}
```

### 3. Mise a jour de CLAUDE.md

Ajouter l'agent dans la liste des agents disponibles.

## Options

| Option | Description |
|--------|-------------|
| `--edit` | Modifie un agent existant |
| `--list` | Liste tous les agents |
| `--template {type}` | Utilise un template d'agent (reviewer, test-runner, etc.) |

## Templates d'agents

| Template | Description |
|----------|-------------|
| `reviewer` | Code review avec focus qualite |
| `test-runner` | Execution et analyse des tests |
| `deploy-manager` | Gestion des deployments |
| `docs-writer` | Generation de documentation |
| `security-reviewer` | Audit de securite |

## Exemples

```bash
# Creer un agent de review
/forge-agent security-reviewer

# Modifier un agent existant
/forge-agent reviewer --edit

# Utiliser un template
/forge-agent my-reviewer --template reviewer

# Lister les agents
/forge-agent --list
```

## Output

```
## Agent cree: security-reviewer

Fichier: .claude/agents/security-reviewer.md
Model: Opus
Tools: Read, Grep, Glob

L'agent sera appele quand:
- L'utilisateur mentionne "securite", "security", "audit"
- Une review de code est demandee

Pour tester: demande une review de securite
Pour modifier: /forge-agent security-reviewer --edit
```
