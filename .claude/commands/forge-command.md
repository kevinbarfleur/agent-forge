# /forge-command - Creer ou modifier une commande

## Usage

- `/forge-command {nom}` - Cree une nouvelle commande
- `/forge-command {nom} --edit` - Modifie une commande existante
- `/forge-command --list` - Liste les commandes disponibles

## Description

Cree une nouvelle commande Claude Code pour le projet. La commande sera creee dans `.claude/commands/{nom}.md`.

## Workflow

### 1. Si nouvelle commande

Poser les questions essentielles:

```
Creation de la commande: /{nom}

1. Que fait cette commande?
   (ex: "Lance les tests", "Deploy en production")

2. Arguments optionnels?
   (ex: "--verbose", "{fichier}", "--env {prod|staging}")

3. Quels agents utilise-t-elle?
   [ ] Aucun (workflow simple)
   [ ] reviewer
   [ ] test-runner
   [ ] {autres agents du projet}

4. Actions bash requises?
   (ex: "npm test", "git push", "docker build")
```

### 2. Generation

Creer le fichier:

```markdown
# /{nom} - {description courte}

## Usage

- `/{nom}` - {action par defaut}
- `/{nom} {args}` - {si arguments}

## Description

{Description detaillee de ce que fait la commande}

## Workflow

### 1. {Premiere etape}
{Details}

### 2. {Deuxieme etape}
{Details}

...

## Agents utilises

{Liste des agents appeles par cette commande, si applicable}

## Output

{Ce que la commande affiche/produit}

## Exemples

```bash
# Exemple 1
/{nom}

# Exemple 2 avec arguments
/{nom} --verbose
```

## Notes

{Informations supplementaires}
```

### 3. Mise a jour de CLAUDE.md

Ajouter la commande dans la liste des commandes disponibles.

## Options

| Option | Description |
|--------|-------------|
| `--edit` | Modifie une commande existante |
| `--list` | Liste toutes les commandes |
| `--template {type}` | Utilise un template (test, deploy, review, etc.) |

## Templates de commandes

| Template | Description |
|----------|-------------|
| `test` | Lance les tests du projet |
| `deploy` | Deploy en production/staging |
| `review` | Lance une code review |
| `lint` | Verifie le code (lint + types) |
| `docs` | Genere la documentation |

## Exemples

```bash
# Creer une commande de deploy
/forge-command deploy

# Modifier une commande
/forge-command test --edit

# Utiliser un template
/forge-command ci --template test

# Lister les commandes
/forge-command --list
```

## Output

```
## Commande creee: /deploy

Fichier: .claude/commands/deploy.md

Usage:
- /deploy - Deploy en production
- /deploy --staging - Deploy en staging

Actions:
1. Verification des tests
2. Build du projet
3. Push vers le registry
4. Deploy

Pour tester: /deploy --dry-run
Pour modifier: /forge-command deploy --edit
```
