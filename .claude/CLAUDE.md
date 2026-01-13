# AgentForge

Generateur de configurations Claude Code.

## Commande principale

`/forge-init` - Lance le processus de generation

## Comment ca marche

1. Tu lances `/forge-init`
2. Je te pose des questions sur ton projet
3. Je genere une config complete dans `forged/{date}-{slug}/.claude/`
4. Tu copies ce dossier dans ton projet

## Structure des outputs

```
forged/
├── 2025-01-13-mon-saas/
│   └── .claude/
│       ├── CLAUDE.md
│       ├── agents/
│       ├── commands/
│       └── rules/
├── 2025-01-14-cli-tool/
│   └── .claude/
│       └── ...
```

## Regles de generation

1. **Contenu intelligent** - Chaque fichier est genere specifiquement pour le projet, pas des templates copie-colle
2. **Model routing** - Opus pour les decisions critiques, Sonnet pour l'execution, Haiku pour le trivial
3. **Descriptions riches** - Les agents ont des descriptions detaillees pour le routing automatique
4. **Minimalisme** - Ne genere que ce qui est necessaire, pas de bloat
