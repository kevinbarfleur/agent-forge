# AgentForge

Generateur de configurations Claude Code.

## Comment ca marche

1. Lance `/forge-init` dans ce repo
2. Reponds aux questions sur ton projet
3. Une config est generee dans `forged/{date}-{slug}/.claude/`
4. Copie ce dossier dans ton projet

## Usage

```bash
# Ouvre Claude Code dans ce repo
cd agent-forge
claude

# Lance la generation
/forge-init
```

## Modes

| Mode | Questions | Duree |
|------|-----------|-------|
| **Express** | 3 | 2 min |
| **Light** | 8 | 5 min |
| **Deep** | 20+ | 15 min |

## Output

```
forged/
├── 2025-01-13-mon-saas/
│   └── .claude/
│       ├── CLAUDE.md
│       ├── agents/
│       │   ├── senior-reviewer.md
│       │   └── test-runner.md
│       ├── commands/
│       │   ├── review.md
│       │   └── test.md
│       └── rules/
│           └── philosophy.md
├── 2025-01-14-cli-tool/
│   └── .claude/
│       └── ...
```

## Utiliser une config generee

```bash
# Copie dans ton projet
cp -r forged/2025-01-13-mon-saas/.claude/ /chemin/vers/ton/projet/

# Lance Claude Code dans ton projet
cd /chemin/vers/ton/projet
claude

# Tes commandes sont disponibles
/review
/test
```

## Ce qui est genere

Les fichiers ne sont PAS des templates copie-colle. Claude genere du contenu **specifique** a ton projet:

- **Agents** avec des checklists adaptees a ta stack
- **Commandes** qui connaissent tes outils
- **Rules** basees sur tes conventions

## License

MIT - Kevin Barfleur
