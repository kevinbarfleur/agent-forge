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

---

## ETAPE 2: Questions selon le mode

### MODE EXPRESS (3 questions)

**Q1: Type de projet**
```
1. SaaS / Web App (frontend + backend)
2. CLI Tool
3. Library / Package
4. API / Backend only
5. Mobile App
```

**Q2: Stack principale**
```
1. TypeScript / Node.js
2. Python
3. Go
4. Rust
5. Autre
```

**Q3: Nom du projet**

### MODE LIGHT (8 questions)

Questions Express + Q4-Q8: Framework, DB, ORM, Tests, Solo/Equipe

### MODE DEEP (20+ questions)

Questions Light + Q9-Q20: Integrations, Deploy, CI/CD, Git workflow, Review level, Docs, Conventions, Vertical, Contraintes, Marketing

---

## ETAPE 3: Selection des composants

Selon les reponses, selectionne dans le CATALOGUE ci-dessous ce qui doit etre genere.

**REGLE**: Pour un SaaS avec paiements/auth, genere MINIMUM 8-12 agents, 10-15 commandes, et 3-5 skills.

---

## CATALOGUE DES AGENTS

### Core (TOUJOURS generer)

| Agent | Role | Model | Quand |
|-------|------|-------|-------|
| `project-architect` | Decisions d'architecture, structure du projet, refactoring majeur | opus | TOUJOURS |
| `senior-reviewer` | Code review, qualite, best practices | opus | TOUJOURS |
| `test-runner` | Execute tests, analyse echecs, suggere fixes | sonnet | Si tests demandes |

### Dev Quotidien (TOUJOURS pour SaaS/Web)

| Agent | Role | Model | Quand |
|-------|------|-------|-------|
| `bug-hunter` | Analyse bugs, trouve la cause, propose fix | sonnet | TOUJOURS |
| `refactor-expert` | Refactoring propre, garde la retro-compatibilite | sonnet | TOUJOURS |
| `perf-analyzer` | Analyse performance, identifie bottlenecks | sonnet | TOUJOURS |

### Frontend (si applicable)

| Agent | Role | Model | Quand |
|-------|------|-------|-------|
| `frontend-expert` | Patterns framework (Next/Nuxt/Svelte), composants, state | sonnet | Si frontend |
| `ui-stylist` | CSS, styling, responsive, animations | sonnet | Si frontend |
| `a11y-checker` | Accessibilite, ARIA, contraste, navigation clavier | haiku | Si frontend |

### Backend / DB (si applicable)

| Agent | Role | Model | Quand |
|-------|------|-------|-------|
| `db-expert` | Queries, indexes, migrations, performance DB | sonnet | Si DB |
| `api-designer` | Design API REST/GraphQL, versioning, documentation | sonnet | Si API |

### Integrations (selon reponses)

| Agent | Role | Model | Quand |
|-------|------|-------|-------|
| `supabase-expert` | RLS, Auth, Realtime, Edge Functions, migrations | sonnet | Si Supabase |
| `prisma-expert` | Schema, migrations, queries optimisees | sonnet | Si Prisma |
| `payment-expert` | Stripe/Lemon, webhooks, subscriptions, checkout | sonnet | Si paiements |
| `auth-expert` | Auth flows, sessions, tokens, OAuth, securite auth | sonnet | Si auth complexe |
| `email-expert` | Templates, deliverabilite, transactional vs marketing | haiku | Si email |
| `storage-expert` | Upload, CDN, optimisation images, presigned URLs | haiku | Si storage |

### Securite / Conformite (selon reponses)

| Agent | Role | Model | Quand |
|-------|------|-------|-------|
| `security-expert` | Vulnerabilites, audit, OWASP, secrets management | opus | Si auth/paiements/sensible |
| `rgpd-expert` | Conformite RGPD, consentement, data retention, DPO | sonnet | Si RGPD |
| `pci-expert` | Conformite PCI-DSS pour paiements | sonnet | Si PCI |

### Marketing / Launch (si demande)

| Agent | Role | Model | Quand |
|-------|------|-------|-------|
| `landing-optimizer` | Copywriting, CTA, conversion, hero section | sonnet | Si marketing |
| `seo-expert` | Meta tags, structured data, sitemap, performance | sonnet | Si marketing |
| `launch-strategist` | Planning launch, ProductHunt, Twitter, outreach | sonnet | Si marketing |

### Documentation

| Agent | Role | Model | Quand |
|-------|------|-------|-------|
| `docs-writer` | README, API docs, guides, changelog | sonnet | Si docs demandees |
| `comment-writer` | JSDoc, docstrings, comments inline | haiku | Si docs demandees |

---

## CATALOGUE DES COMMANDES

### Core (TOUJOURS)

| Commande | Description | Quand |
|----------|-------------|-------|
| `/review` | Code review complet | TOUJOURS |
| `/review {path}` | Review fichier/dossier specifique | TOUJOURS |

### Dev Quotidien (TOUJOURS pour SaaS/Web)

| Commande | Description | Quand |
|----------|-------------|-------|
| `/fix {description}` | Analyse et corrige un bug | TOUJOURS |
| `/hotfix` | Fix urgent, minimal, rapide | TOUJOURS |
| `/refactor {path}` | Refactoring d'un fichier/module | TOUJOURS |
| `/perf` | Analyse performance globale | TOUJOURS |
| `/perf {path}` | Analyse performance d'un fichier | TOUJOURS |

### UI/Styling (si frontend)

| Commande | Description | Quand |
|----------|-------------|-------|
| `/style {description}` | Fix probleme UI/CSS | Si frontend |
| `/responsive` | Verifie le responsive design | Si frontend |
| `/a11y` | Audit accessibilite | Si frontend |

### Tests

| Commande | Description | Quand |
|----------|-------------|-------|
| `/test` | Lance tous les tests | Si tests |
| `/test {path}` | Tests d'un fichier/dossier | Si tests |
| `/test --coverage` | Tests avec coverage | Si tests |
| `/test --watch` | Tests en watch mode | Si tests |

### DB

| Commande | Description | Quand |
|----------|-------------|-------|
| `/db-check` | Verifie schema, indexes, migrations | Si DB |
| `/migrate` | Cree une migration | Si DB |

### Deploy / Ops

| Commande | Description | Quand |
|----------|-------------|-------|
| `/deploy` | Checklist pre-deploy | TOUJOURS |
| `/deploy --dry` | Simule le deploy | TOUJOURS |
| `/env-check` | Verifie les env vars | TOUJOURS |

### Git / Workflow

| Commande | Description | Quand |
|----------|-------------|-------|
| `/commit` | Commit avec message genere | TOUJOURS |
| `/pr` | Cree une PR avec description | Si feature branches |
| `/changelog` | Genere changelog depuis commits | Si docs |

### Securite

| Commande | Description | Quand |
|----------|-------------|-------|
| `/security` | Audit securite complet | Si auth/paiements |
| `/secrets` | Verifie les secrets exposes | TOUJOURS |

### Documentation

| Commande | Description | Quand |
|----------|-------------|-------|
| `/docs` | Genere/update la documentation | Si docs |
| `/readme` | Update le README | Si docs |

### Marketing (si demande)

| Commande | Description | Quand |
|----------|-------------|-------|
| `/landing` | Optimise la landing page | Si marketing |
| `/seo` | Audit SEO | Si marketing |
| `/copy {section}` | Genere du copywriting | Si marketing |

### Integration specifiques

| Commande | Description | Quand |
|----------|-------------|-------|
| `/stripe` | Debug integration Stripe | Si Stripe |
| `/lemon` | Debug integration LemonSqueezy | Si LemonSqueezy |
| `/supabase` | Debug queries/RLS Supabase | Si Supabase |
| `/email-preview` | Preview des emails | Si email |

---

## CATALOGUE DES SKILLS

Les skills fournissent du contexte reutilisable que les agents peuvent charger.

### Framework Skills (selon stack)

| Skill | Contenu | Quand |
|-------|---------|-------|
| `nextjs/` | App Router, Server Components, Server Actions, Metadata | Si Next.js |
| `nuxt/` | Auto-imports, composables, server routes, Nitro | Si Nuxt |
| `sveltekit/` | Load functions, actions, hooks | Si SvelteKit |
| `vue/` | Composition API, reactivity, composables | Si Vue/Nuxt |
| `react/` | Hooks, patterns, state management | Si React/Next |

### Integration Skills (selon integrations)

| Skill | Contenu | Quand |
|-------|---------|-------|
| `supabase/` | Client setup, RLS policies, Auth patterns, Realtime | Si Supabase |
| `prisma/` | Schema patterns, migrations, query optimization | Si Prisma |
| `stripe/` | Checkout, webhooks, subscriptions, Customer Portal | Si Stripe |
| `lemonsqueezy/` | Checkout, webhooks, license keys, variants | Si LemonSqueezy |
| `resend/` | Templates, React Email, deliverability | Si Resend |

### Domain Skills (selon domaine)

| Skill | Contenu | Quand |
|-------|---------|-------|
| `auth/` | Auth patterns, sessions, tokens, refresh, OAuth | Si auth complexe |
| `payments/` | Payment flows, webhooks, refunds, invoices | Si paiements |
| `ecommerce/` | Cart, checkout, inventory, orders | Si e-commerce |

### Conformite Skills (selon contraintes)

| Skill | Contenu | Quand |
|-------|---------|-------|
| `rgpd/` | Consentement, cookies, data retention, droits utilisateurs | Si RGPD |
| `security/` | OWASP Top 10, headers, CSP, sanitization | Si securite critique |

---

## ETAPE 4: Synthese et confirmation

Affiche un resume COMPLET de ce qui va etre genere:

```markdown
## Configuration a generer

**Projet**: {nom}
**Type**: {type}
**Stack**: {stack complet}
**Integrations**: {liste}

### Agents ({nombre} agents)

| Agent | Role | Model |
|-------|------|-------|
| ... | ... | ... |

### Commandes ({nombre} commandes)

| Commande | Description |
|----------|-------------|
| ... | ... |

### Skills ({nombre} skills)

| Skill | Description |
|-------|-------------|
| ... | ... |

### Rules

- philosophy.md
- {autres rules}

---

Output: forged/{date}-{slug}/.claude/

Generer? [O/n]
```

---

## ETAPE 5: Generation

### Structure a generer

```
forged/{YYYY-MM-DD}-{slug}/
└── .claude/
    ├── CLAUDE.md
    ├── agents/
    │   ├── project-architect.md
    │   ├── senior-reviewer.md
    │   ├── bug-hunter.md
    │   ├── {frontend-expert}.md
    │   ├── {supabase-expert}.md
    │   ├── {payment-expert}.md
    │   ├── {security-expert}.md
    │   └── ...
    ├── commands/
    │   ├── review.md
    │   ├── fix.md
    │   ├── hotfix.md
    │   ├── refactor.md
    │   ├── test.md
    │   ├── deploy.md
    │   └── ...
    ├── skills/
    │   ├── nuxt/
    │   │   └── SKILL.md
    │   ├── supabase/
    │   │   └── SKILL.md
    │   └── ...
    └── rules/
        ├── philosophy.md
        └── ...
```

### Generation CLAUDE.md

Le CLAUDE.md doit:
- Lister TOUTES les commandes disponibles
- Lister TOUS les agents avec leur role
- Lister TOUTES les skills
- Expliquer la stack
- Definir les conventions

### Generation des Agents

Chaque agent DOIT avoir:
- **YAML frontmatter** avec name, description (50-100 mots), model, tools
- **Contexte technique** specifique au projet
- **Checklist** ou workflow detaille
- **Format de sortie** explicite

### Generation des Commandes

Chaque commande DOIT avoir:
- **Usage** avec variantes
- **Workflow** etape par etape
- **Agent(s)** a utiliser si applicable
- **Output** attendu

### Generation des Skills

Chaque skill DOIT avoir:
- **SKILL.md** avec frontmatter (name, description)
- **Patterns** et examples de code specifiques a l'integration
- **Do's and Don'ts**
- **Reference** rapide

---

## ETAPE 6: Finalisation

Affiche le resume final avec:
- Liste complete des fichiers generes
- Commande pour copier dans le projet
- Liste des commandes disponibles
- Conseils pour demarrer

---

## REGLES CRITIQUES

1. **GENERE BEAUCOUP** - Un SaaS complet = 8-12 agents, 10-15 commandes, 3-5 skills minimum

2. **CONTENU SPECIFIQUE** - Chaque fichier adapte au projet. Les checklists mentionnent les technos exactes.

3. **DESCRIPTIONS RICHES** - 50-100 mots pour que le routing automatique fonctionne

4. **MODEL ROUTING**:
   - `opus`: project-architect, senior-reviewer, security-expert
   - `sonnet`: La plupart des agents
   - `haiku`: a11y-checker, comment-writer, taches simples

5. **TOOLS EXPLICITES** - Chaque agent a sa liste de tools, pas "all"

6. **SKILLS UTILES** - Les skills contiennent des patterns concrets, pas de la doc generique
