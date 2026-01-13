# /forge-init

Genere une configuration Claude Code sur mesure pour le projet de l'utilisateur.

---

## TON ROLE

Tu es un **forgeron** qui cree des outils sur mesure. Tu ne pioches pas dans un catalogue - tu **inventes** les agents, commandes et skills adaptes au projet.

Chaque configuration que tu generes est **unique**. Les noms, les roles, le nombre d'agents - tout depend du contexte et des besoins de l'utilisateur.

---

## ETAPE 1: Comprendre le projet

Pose des questions pour comprendre:

1. **Quel type de projet?** (laisse l'utilisateur decrire librement)
2. **Quels outils/technos?** (si applicable)
3. **Quels sont les workflows quotidiens?**
4. **Quels problemes veux-tu resoudre avec Claude?**
5. **Solo ou equipe?**
6. **Des contraintes particulieres?**

Adapte tes questions au contexte. Si c'est un projet de dev, demande la stack. Si c'est autre chose, pose les questions pertinentes.

Tu peux poser plus ou moins de questions selon le mode choisi (Express/Light/Deep).

---

## ETAPE 2: Concevoir la configuration

Apres avoir compris le projet, **reflechis** a ce dont l'utilisateur a besoin.

### Questions a te poser:

**Pour les agents:**
- Quelles sont les taches repetitives que l'utilisateur fait?
- Quels experts seraient utiles pour ce projet?
- Quels problemes specifiques necessitent une attention specialisee?
- Quel niveau de detail/specialisation est necessaire?

**Pour les commandes:**
- Quelles actions l'utilisateur va faire quotidiennement?
- Quels raccourcis lui feraient gagner du temps?
- Quelles taches complexes peuvent etre simplifiees?

**Pour les skills:**
- Quelles connaissances contextuelles seraient utiles?
- Quels patterns/references l'utilisateur a besoin d'avoir sous la main?

### Principes:

- **Pas de minimum, pas de maximum** - genere ce qui est necessaire, ni plus ni moins
- **Noms explicites** - les noms doivent refleter le role exact dans CE projet
- **Specialisation** - mieux vaut plusieurs agents specialises qu'un agent generique
- **Contexte** - chaque fichier genere doit etre specifique au projet, pas generique

---

## ETAPE 3: Proposer et confirmer

Presente ta proposition:

```
## Configuration proposee pour {projet}

### Agents ({nombre})

| Agent | Role | Model |
|-------|------|-------|
| {nom-que-tu-as-choisi} | {role specifique} | {opus/sonnet/haiku} |
| ... | ... | ... |

### Commandes ({nombre})

| Commande | Description |
|----------|-------------|
| /{nom} | {ce que ca fait} |
| ... | ... |

### Skills ({nombre})

| Skill | Contenu |
|-------|---------|
| {nom}/ | {ce que ca contient} |
| ... | ... |

### Rules

- {liste des fichiers de regles}

---

Output: forged/{date}-{slug}/.claude/

Cette configuration te convient? Tu veux ajouter/modifier quelque chose?
```

Attends la validation ou les modifications demandees.

---

## ETAPE 4: Generer les fichiers

### Structure

```
forged/{YYYY-MM-DD}-{slug}/
└── .claude/
    ├── CLAUDE.md
    ├── agents/
    │   └── {tes-agents}.md
    ├── commands/
    │   └── {tes-commandes}.md
    ├── skills/
    │   └── {tes-skills}/
    │       └── SKILL.md
    └── rules/
        └── {tes-rules}.md
```

### Format des agents

```markdown
---
name: {nom-descriptif}
description: {DESCRIPTION RICHE de 50-100 mots qui explique precisement quand appeler cet agent, ce qu'il fait, et dans quel contexte. Cette description est CRITIQUE pour le routing automatique.}
model: {opus|sonnet|haiku}
tools:
  - {liste des outils necessaires}
---

# {Nom de l'Agent}

{Introduction: qui est cet agent, quel est son role dans ce projet specifique}

## Contexte

{Informations specifiques au projet que l'agent doit connaitre}

## Quand m'utiliser

{Liste des situations ou cet agent est pertinent}

## Comment je travaille

{Workflow detaille, etape par etape}

## Mon output

{Format de sortie attendu, exemples si utile}
```

### Format des commandes

```markdown
# /{nom} - {description courte}

## Usage

- `/{nom}` - {usage de base}
- `/{nom} {args}` - {variantes}

## Ce que ca fait

{Description detaillee}

## Workflow

1. {etape 1}
2. {etape 2}
...

## Output

{Ce que l'utilisateur voit}
```

### Format des skills

```markdown
---
name: {nom}
description: {description pour le chargement automatique}
---

# {Nom du Skill}

{Introduction}

## Patterns

{Patterns specifiques au projet, avec exemples de code si pertinent}

## Do's and Don'ts

### Do
- {bonne pratique}

### Don't
- {anti-pattern}

## Reference rapide

{Cheatsheet, commandes, snippets utiles}
```

### Model routing

- **opus**: Pour les decisions importantes, l'architecture, la securite, les reviews critiques
- **sonnet**: Pour la plupart des taches - execution, analyse, generation
- **haiku**: Pour les taches simples, rapides, repetitives

---

## ETAPE 5: Finaliser

Affiche:
- Liste des fichiers generes
- Commande pour copier dans le projet
- Apercu des commandes disponibles
- Conseils pour demarrer

---

## EXEMPLES (pour illustrer le niveau de qualite, PAS pour copier)

### Exemple 1: Projet SaaS TypeScript

Pour un SaaS de gestion de projets en Next.js + Supabase + Stripe:

**Agents possibles** (inventes pour ce contexte):
- `project-guardian` - veille sur l'architecture et la coherence du code
- `data-sentinel` - expert Supabase, RLS, queries optimisees
- `payment-watcher` - tout ce qui touche Stripe, webhooks, subscriptions
- `ui-crafter` - composants React, styling, UX
- `test-pilot` - tests, coverage, CI
- `security-auditor` - vulnerabilites, auth, secrets
- `deploy-chief` - deployments, env vars, monitoring

**Commandes possibles**:
- `/check` - verification rapide du code modifie
- `/fix` - analyser et corriger un bug
- `/ship` - checklist pre-deploy complete
- `/perf` - analyse de performance

### Exemple 2: Projet de contenu/blog

Pour un blog avec beaucoup de contenu a gerer:

**Agents possibles**:
- `content-strategist` - planning editorial, idees, angles
- `draft-reviewer` - relecture, structure, clarte
- `seo-optimizer` - mots-cles, meta, structure
- `fact-checker` - verification des sources et donnees
- `image-curator` - selection et optimisation des visuels

**Commandes possibles**:
- `/outline {sujet}` - generer un plan d'article
- `/review` - relecture complete
- `/seo {url}` - audit SEO d'une page
- `/publish` - checklist pre-publication

### Exemple 3: Projet e-commerce (non-dev, gestion)

Pour quelqu'un qui gere un e-commerce sans coder:

**Agents possibles**:
- `inventory-analyst` - suivi stock, alertes, previsions
- `pricing-strategist` - analyse prix, concurrence, marges
- `customer-helper` - templates reponses, FAQ, support
- `promo-planner` - calendrier promos, idees campagnes

**Commandes possibles**:
- `/stock` - etat des stocks
- `/price-check {produit}` - analyse prix vs concurrence
- `/respond {type}` - generer une reponse client
- `/promo` - idees de promotions

---

## REGLES ABSOLUES

1. **INVENTE TOUT** - Ne copie pas les exemples. Cree des agents/commandes adaptes au projet specifique.

2. **NOMS SIGNIFICATIFS** - Les noms doivent avoir du sens dans le contexte du projet. Pas de noms generiques.

3. **DESCRIPTIONS RICHES** - 50-100 mots minimum pour les descriptions d'agents. C'est critique pour le routing.

4. **SPECIALISATION** - Plusieurs agents specialises > un agent generique. Chaque agent a un domaine precis.

5. **ADAPTE-TOI** - Projet dev? Projet creatif? Projet business? Adapte ton vocabulaire et tes propositions.

6. **QUALITE > QUANTITE** - Ne genere pas 20 agents si 5 suffisent. Ne genere pas 5 si 15 sont necessaires.

7. **CONTENU SPECIFIQUE** - Chaque fichier genere doit contenir des informations specifiques au projet, pas du texte generique.
