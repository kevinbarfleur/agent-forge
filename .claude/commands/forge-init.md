# /forge-init

Generates a custom Claude Code configuration for the user's project.

---

## YOUR ROLE

You are a **blacksmith** who creates custom tools. You don't pick from a catalog - you **invent** agents, commands, and skills tailored to the project.

Every configuration you generate is **unique**. The names, roles, number of agents - everything depends on the context and user's needs.

---

## STEP 1: Assess the context

### If you've already discussed the project (prior brainstorming)

Use everything you learned during the conversation. No need to re-ask questions.

Just verify you have the essential info:
- Project type
- Stack/tools (if relevant)
- Daily workflows
- Problems to solve

If something's missing, only ask what's missing.

### If it's a direct launch (no prior discussion)

Ask questions to understand:

1. **What type of project?** (let the user describe freely)
2. **What tools/tech?** (if applicable)
3. **What are the daily workflows?**
4. **What problems do you want Claude to solve?**
5. **Solo or team?**
6. **Any specific constraints?**

Adapt your questions to the context. If it's a dev project, ask about the stack. If it's something else, ask relevant questions.

---

## STEP 2: Design the configuration

After understanding the project, **think** about what the user needs.

### Questions to ask yourself:

**For agents:**
- What repetitive tasks does the user do?
- What experts would be useful for this project?
- What specific problems need specialized attention?
- What level of detail/specialization is needed?

**For commands:**
- What actions will the user do daily?
- What shortcuts would save them time?
- What complex tasks can be simplified?

**For skills:**
- What contextual knowledge would be useful?
- What patterns/references does the user need at hand?

### Principles:

- **No minimum, no maximum** - generate what's necessary, no more no less
- **Explicit names** - names must reflect the exact role in THIS project
- **Specialization** - better to have multiple specialized agents than one generic agent
- **Context** - every generated file must be project-specific, not generic

---

## STEP 3: Propose and confirm

Present your proposal:

```
## Proposed configuration for {project}

### Agents ({count})

| Agent | Role | Model |
|-------|------|-------|
| {name-you-chose} | {specific role} | {opus/sonnet/haiku} |
| ... | ... | ... |

### Commands ({count})

| Command | Description |
|---------|-------------|
| /{name} | {what it does} |
| ... | ... |

### Skills ({count})

| Skill | Content |
|-------|---------|
| {name}/ | {what it contains} |
| ... | ... |

### Rules

- {list of rule files}

---

Output: forged/{date}-{slug}/.claude/

Does this configuration work for you? Want to add/modify anything?
```

Wait for validation or requested changes.

---

## STEP 4: Generate the files

### Structure

```
forged/{YYYY-MM-DD}-{slug}/
└── .claude/
    ├── CLAUDE.md
    ├── agents/
    │   └── {your-agents}.md
    ├── commands/
    │   └── {your-commands}.md
    ├── skills/
    │   └── {your-skills}/
    │       └── SKILL.md
    └── rules/
        └── {your-rules}.md
```

### Agent format

```markdown
---
name: {descriptive-name}
description: {RICH DESCRIPTION of 50-100 words that explains precisely when to call this agent, what it does, and in what context. This description is CRITICAL for automatic routing.}
model: {opus|sonnet|haiku}
tools:
  - {list of necessary tools}
---

# {Agent Name}

{Introduction: who is this agent, what's their role in this specific project}

## Context

{Project-specific information the agent needs to know}

## When to use me

{List of situations where this agent is relevant}

## How I work

{Detailed workflow, step by step}

## My output

{Expected output format, examples if useful}
```

### Command format

```markdown
# /{name} - {short description}

## Usage

- `/{name}` - {basic usage}
- `/{name} {args}` - {variants}

## What it does

{Detailed description}

## Workflow

1. {step 1}
2. {step 2}
...

## Output

{What the user sees}
```

### Skill format

```markdown
---
name: {name}
description: {description for automatic loading}
---

# {Skill Name}

{Introduction}

## Patterns

{Project-specific patterns, with code examples if relevant}

## Do's and Don'ts

### Do
- {best practice}

### Don't
- {anti-pattern}

## Quick reference

{Cheatsheet, commands, useful snippets}
```

### Model routing

- **opus**: For important decisions, architecture, security, critical reviews
- **sonnet**: For most tasks - execution, analysis, generation
- **haiku**: For simple, fast, repetitive tasks

---

## STEP 5: Finalize

Display:
- List of generated files
- Command to copy to the project
- Overview of available commands
- Tips for getting started

---

## EXAMPLES (to illustrate quality level, NOT to copy)

### Example 1: TypeScript SaaS Project

For a project management SaaS in Next.js + Supabase + Stripe:

**Possible agents** (invented for this context):
- `project-guardian` - watches over architecture and code coherence
- `data-sentinel` - Supabase expert, RLS, optimized queries
- `payment-watcher` - everything Stripe, webhooks, subscriptions
- `ui-crafter` - React components, styling, UX
- `test-pilot` - tests, coverage, CI
- `security-auditor` - vulnerabilities, auth, secrets
- `deploy-chief` - deployments, env vars, monitoring

**Possible commands**:
- `/check` - quick verification of modified code
- `/fix` - analyze and fix a bug
- `/ship` - complete pre-deploy checklist
- `/perf` - performance analysis

### Example 2: Content/Blog Project

For a blog with lots of content to manage:

**Possible agents**:
- `content-strategist` - editorial planning, ideas, angles
- `draft-reviewer` - proofreading, structure, clarity
- `seo-optimizer` - keywords, meta, structure
- `fact-checker` - source and data verification
- `image-curator` - visual selection and optimization

**Possible commands**:
- `/outline {topic}` - generate an article outline
- `/review` - complete proofreading
- `/seo {url}` - SEO audit of a page
- `/publish` - pre-publication checklist

### Example 3: E-commerce Project (non-dev, management)

For someone managing an e-commerce without coding:

**Possible agents**:
- `inventory-analyst` - stock tracking, alerts, forecasts
- `pricing-strategist` - price analysis, competition, margins
- `customer-helper` - response templates, FAQ, support
- `promo-planner` - promo calendar, campaign ideas

**Possible commands**:
- `/stock` - inventory status
- `/price-check {product}` - price analysis vs competition
- `/respond {type}` - generate a customer response
- `/promo` - promotion ideas

---

## ABSOLUTE RULES

1. **INVENT EVERYTHING** - Don't copy examples. Create agents/commands tailored to the specific project.

2. **MEANINGFUL NAMES** - Names must make sense in the project's context. No generic names.

3. **RICH DESCRIPTIONS** - 50-100 words minimum for agent descriptions. Critical for routing.

4. **SPECIALIZATION** - Multiple specialized agents > one generic agent. Each agent has a precise domain.

5. **ADAPT** - Dev project? Creative project? Business project? Adapt your vocabulary and proposals.

6. **QUALITY > QUANTITY** - Don't generate 20 agents if 5 are enough. Don't generate 5 if 15 are necessary.

7. **SPECIFIC CONTENT** - Every generated file must contain project-specific information, not generic text.
