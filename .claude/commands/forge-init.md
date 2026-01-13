# /forge-init

Genere une configuration Claude Code complete pour un projet.

## IMPORTANT - Lis tout avant d'agir

Cette commande te guide pour generer une config `.claude/` adaptee au projet de l'utilisateur.
Le resultat sera sauvegarde dans `forged/{YYYY-MM-DD}-{slug}/.claude/`.

---

## ETAPE 1: Choix du mode

Demande a l'utilisateur quel mode il veut:

```
Quel mode de configuration?

1. Express (2 min) - 3 questions, config solide
2. Light (5 min) - 8 questions, plus de personnalisation
3. Deep (15 min) - 20+ questions, configuration complete
```

Utilise AskUserQuestion avec ces options.

---

## ETAPE 2: Questions selon le mode

### MODE EXPRESS (3 questions)

**Q1: Type de projet**
```
Quel type de projet?

1. SaaS / Web App (frontend + backend)
2. CLI Tool (ligne de commande)
3. Library / Package (npm, pip, crate...)
4. API / Backend only
5. Mobile App (React Native, Flutter...)
```

**Q2: Stack principale**
```
Stack principale?

1. TypeScript / Node.js
2. Python
3. Go
4. Rust
5. Autre (precise)
```

**Q3: Nom du projet**
```
Nom du projet? (sera utilise pour le slug)
Ex: mon-saas, cli-tool, awesome-lib
```

Passe ensuite a l'ETAPE 3.

---

### MODE LIGHT (8 questions)

Pose les 3 questions Express, puis:

**Q4: Framework (si applicable)**

Si SaaS/Web:
```
Framework frontend?
1. Next.js
2. Nuxt
3. SvelteKit
4. Remix
5. Autre / Pas de framework
```

Si API:
```
Framework backend?
1. Express / Fastify
2. NestJS
3. Django / FastAPI
4. Gin / Echo
5. Autre
```

**Q5: Base de donnees**
```
Base de donnees?
1. PostgreSQL
2. MySQL
3. MongoDB
4. SQLite
5. Pas de DB / Autre
```

**Q6: ORM / Query builder (si DB)**
```
ORM?
1. Prisma
2. Drizzle
3. TypeORM
4. SQLAlchemy
5. Pas d'ORM / Raw SQL
```

**Q7: Tests**
```
Niveau de tests souhaite?
1. Tests unitaires + integration (recommande)
2. Tests unitaires seulement
3. Pas de tests pour le MVP
```

**Q8: Solo ou equipe**
```
Tu travailles:
1. Solo
2. Petite equipe (2-5)
3. Equipe (5+)
```

Passe ensuite a l'ETAPE 3.

---

### MODE DEEP (20+ questions)

Pose les 8 questions Light, puis:

**Q9: Integrations tierces**
```
Integrations? (selection multiple)
[ ] Stripe / Paiements
[ ] Auth externe (Auth0, Clerk, Supabase Auth)
[ ] Email (SendGrid, Resend, Postmark)
[ ] Storage (S3, Cloudflare R2)
[ ] Analytics
[ ] Autre
```

**Q10: Deploiement**
```
Ou deploies-tu?
1. Vercel
2. Railway / Render
3. AWS / GCP / Azure
4. Self-hosted / VPS
5. Pas encore decide
```

**Q11: CI/CD**
```
CI/CD?
1. GitHub Actions
2. GitLab CI
3. Autre
4. Pas encore
```

**Q12: Workflow Git**
```
Workflow Git?
1. Trunk-based (push direct sur main)
2. Feature branches + PR
3. GitFlow
```

**Q13: Niveau de review**
```
Niveau de rigueur code review?
1. Strict (bloque si probleme)
2. Modere (suggestions)
3. Light (juste les erreurs critiques)
```

**Q14: Documentation**
```
Documentation requise?
1. JSDoc/docstrings obligatoires
2. README + docs principales
3. Minimal
```

**Q15: Conventions code**
```
Conventions specifiques?
(Ex: "pas de any en TS", "tout en anglais", "80 chars max")
Ou "Aucune" si pas de preference.
```

**Q16-20: Domaine metier (si SaaS)**

```
Vertical/Domaine?
1. E-commerce
2. Fintech
3. Healthtech
4. B2B SaaS generique
5. B2C App
6. Autre
```

```
Contraintes specifiques?
(Ex: "GDPR", "HIPAA", "PCI-DSS", "Aucune")
```

```
Besoins marketing/launch?
1. Oui, je veux des agents marketing
2. Non, juste le dev
```

Passe ensuite a l'ETAPE 3.

---

## ETAPE 3: Synthese et confirmation

Affiche un resume de ce qui va etre genere:

```markdown
## Configuration a generer

**Projet**: {nom}
**Type**: {type}
**Stack**: {stack} + {framework} + {db} + {orm}
**Mode**: {solo/equipe}

### Agents a generer

| Agent | Role | Model |
|-------|------|-------|
| senior-reviewer | Code review, architecture | opus |
| test-runner | Execute les tests | sonnet |
| {autres selon contexte} | ... | ... |

### Commandes a generer

| Commande | Description |
|----------|-------------|
| /review | Lance une code review |
| /test | Lance les tests |
| {autres selon contexte} | ... |

### Rules a generer
- philosophy.md (principes du projet)
- {stack}.md (conventions specifiques)

---

Output: forged/{date}-{slug}/.claude/

Generer? [O/n]
```

Attends la confirmation avant de continuer.

---

## ETAPE 4: Generation

### 4.1 Creer la structure

```bash
forged/{YYYY-MM-DD}-{slug}/
└── .claude/
    ├── CLAUDE.md
    ├── agents/
    ├── commands/
    └── rules/
```

Utilise le format de date: `2025-01-13`
Slug: lowercase, tirets, pas d'espaces (ex: `mon-super-saas`)

### 4.2 Generer CLAUDE.md

Genere un CLAUDE.md SPECIFIQUE au projet. Exemple pour un SaaS Next.js + Prisma:

```markdown
# {Nom du Projet}

{Description en 1-2 phrases basee sur le contexte}

## Stack

- **Frontend**: Next.js 14 (App Router)
- **Backend**: Server Actions + API Routes
- **Database**: PostgreSQL + Prisma
- **Deploy**: Vercel

## Commandes

| Commande | Description |
|----------|-------------|
| /review | Code review avec focus archi et perf |
| /test | Lance les tests (unit + integration) |
| /deploy | Checklist pre-deploy |

## Agents

| Agent | Role | Quand l'utiliser |
|-------|------|------------------|
| senior-reviewer | Review code et architecture | Avant merge, refactoring |
| test-runner | Tests et coverage | Apres changements |

## Conventions

{Conventions specifiques si mentionnees, sinon des defaults sensibles}

- TypeScript strict, pas de `any`
- Server Components par defaut, Client Components explicites
- Prisma: toujours `select` les champs necessaires

## Structure projet

```
src/
├── app/           # Next.js App Router
├── components/    # UI components
├── lib/           # Utilities, helpers
├── server/        # Server-only code
└── prisma/        # Schema et migrations
```
```

### 4.3 Generer les Agents

Pour chaque agent, genere un fichier SPECIFIQUE. Pas de template generique.

**Exemple: `agents/senior-reviewer.md` pour un projet Next.js + Prisma + Stripe**

```markdown
---
name: senior-reviewer
description: Review le code Next.js avec focus sur App Router patterns, Server Components vs Client Components, queries Prisma optimisees, et securite des webhooks Stripe. Appeler avant les merges importants ou pour du refactoring.
model: opus
tools:
  - Read
  - Grep
  - Glob
---

# Senior Reviewer

Tu es le code reviewer senior pour ce projet SaaS.

## Contexte technique

- **Next.js 14**: App Router, Server Components, Server Actions
- **Prisma**: PostgreSQL, besoin d'optimiser les queries
- **Stripe**: Webhooks, subscriptions

## Checklist de review

### Architecture Next.js
- [ ] Server Components utilises par defaut?
- [ ] "use client" seulement quand necessaire?
- [ ] Server Actions pour les mutations (pas d'API routes inutiles)?
- [ ] Metadata et generateMetadata pour le SEO?

### Performance Prisma
- [ ] Pas de `findMany` sans `take` limit?
- [ ] `select` explicite (pas de select *)?
- [ ] Relations chargees avec `include` seulement si necessaire?
- [ ] Pas de N+1 queries?

### Securite Stripe
- [ ] Webhook signature verifiee?
- [ ] Idempotency keys pour les operations critiques?
- [ ] Pas de prix/IDs hardcodes cote client?

### General
- [ ] Pas de `any` en TypeScript?
- [ ] Error handling present?
- [ ] Pas de secrets/credentials dans le code?

## Output

Quand tu fais une review:

1. Liste les fichiers analyses
2. Pour chaque probleme:
   - Fichier + ligne
   - Probleme
   - Suggestion de fix
3. Score global (OK / Minor issues / Bloquant)
4. Resume en 2-3 phrases
```

**Exemple: `agents/test-runner.md`**

```markdown
---
name: test-runner
description: Execute les tests unitaires et d'integration, analyse les echecs, suggere des fixes. Appeler avec /test ou quand l'utilisateur mentionne tests, coverage, CI.
model: sonnet
tools:
  - Bash
  - Read
  - Grep
---

# Test Runner

Tu geres les tests pour ce projet.

## Commandes

```bash
# Tests unitaires
pnpm test

# Tests avec coverage
pnpm test:coverage

# Tests en watch mode
pnpm test:watch

# Un fichier specifique
pnpm test src/lib/utils.test.ts
```

## Workflow

1. **Lancer les tests** demandes
2. **Si echecs**:
   - Lire le fichier de test
   - Lire le fichier source
   - Identifier la cause
   - Proposer un fix
3. **Reporter** les resultats clairement

## Format de rapport

```
## Resultats des tests

Tests: X passed, Y failed, Z skipped
Coverage: XX%

### Echecs

**test/utils.test.ts > formatDate**
- Attendu: "2025-01-13"
- Recu: "13/01/2025"
- Cause probable: Format de date incorrect
- Fix suggere: Utiliser toISOString().split('T')[0]

### Coverage faible

- src/lib/auth.ts: 45% (manque tests pour refreshToken)
```
```

### 4.4 Generer les Commandes

**Exemple: `commands/review.md`**

```markdown
# /review - Code Review

## Usage

- `/review` - Review les fichiers modifies (git diff)
- `/review src/` - Review un dossier specifique
- `/review src/auth.ts` - Review un fichier

## Workflow

1. Identifier les fichiers a review
   - Si pas d'argument: `git diff --name-only HEAD~1`
   - Si argument: les fichiers/dossiers specifies

2. Deleguer a l'agent `senior-reviewer`

3. Afficher le rapport de review

## Output

Le rapport inclut:
- Fichiers analyses
- Problemes trouves (avec localisation)
- Suggestions de fix
- Score global
```

**Exemple: `commands/test.md`**

```markdown
# /test - Lancer les tests

## Usage

- `/test` - Lance tous les tests
- `/test --coverage` - Avec rapport de coverage
- `/test src/lib/` - Tests d'un dossier
- `/test --watch` - Mode watch

## Workflow

1. Deleguer a l'agent `test-runner`
2. Executer la commande appropriee
3. Analyser les resultats
4. Si echecs: proposer des fixes

## Output

- Nombre de tests passed/failed
- Coverage si demande
- Details des echecs avec suggestions
```

### 4.5 Generer les Rules

**Exemple: `rules/philosophy.md`**

```markdown
# Philosophie du projet

## Principes

1. **Ship fast** - MVP first, polish later
2. **Type safety** - TypeScript strict, pas de any
3. **Server-first** - Server Components par defaut

## Out of scope (pour le MVP)

- Tests E2E
- i18n
- Dark mode
- Analytics avances

## Conventions

- Commits en anglais
- Branches: feature/, fix/, chore/
- PR obligatoires pour main
```

---

## ETAPE 5: Finalisation

Apres avoir genere tous les fichiers, affiche:

```markdown
## Generation terminee!

**Output**: forged/{date}-{slug}/.claude/

### Fichiers generes

```
forged/{date}-{slug}/.claude/
├── CLAUDE.md
├── agents/
│   ├── senior-reviewer.md
│   └── test-runner.md
├── commands/
│   ├── review.md
│   └── test.md
└── rules/
    └── philosophy.md
```

### Pour utiliser cette config

```bash
# Copie dans ton projet
cp -r forged/{date}-{slug}/.claude/ /chemin/vers/ton/projet/

# Ou si tu es deja dans ton projet
cp -r /chemin/vers/agent-forge/forged/{date}-{slug}/.claude/ .
```

Puis relance Claude Code dans ton projet.

### Commandes disponibles

- `/review` - Code review
- `/test` - Lancer les tests

Besoin de modifications? Tu peux editer les fichiers directement ou relancer `/forge-init` pour une nouvelle config.
```

---

## REGLES IMPORTANTES

1. **Genere du contenu SPECIFIQUE** - Pas de placeholders `{nom}`, pas de templates generiques. Chaque fichier doit etre adapte au projet.

2. **Descriptions d'agents DETAILLEES** - La description YAML doit faire 50-100 mots pour que le routing automatique fonctionne bien.

3. **Model routing intelligent**:
   - `opus`: Decisions d'architecture, security review, refactoring majeur
   - `sonnet`: Tests, docs, taches standard
   - `haiku`: Formatting, questions simples

4. **Pas de bloat** - Ne genere que ce qui est necessaire. Un projet simple n'a pas besoin de 10 agents.

5. **Tools whitelisting** - Chaque agent a une liste explicite de tools, pas de "all".
