# AgentForge

Generateur de configurations Claude Code sur mesure.

## Comment ca marche

1. Ouvre Claude Code dans ce repo
2. Parle de ton projet (brainstorming libre)
3. Quand tu es pret, lance `/forge-init`
4. Une config est generee dans `forged/{date}-{slug}/.claude/`
5. Copie ce dossier dans ton projet

## Usage

```bash
# Ouvre Claude Code dans ce repo
cd agent-forge
claude

# Parle de ton projet...
# "Je veux creer un SaaS de facturation pour freelances"
# "C'est du Next.js avec Supabase et Stripe"
# etc.

# Quand tu es pret
/forge-init
```

## Le flow

### 1. Brainstorming (par defaut)

Quand tu arrives, Claude engage la conversation. Pas de questionnaire robotique.

- Tu expliques ton projet
- Claude pose des questions, challenge tes idees
- Vous discutez librement

### 2. Generation (/forge-init)

Quand tu es pret, tu lances `/forge-init`. Claude genere une config complete basee sur tout l'echange.

## Output

```
forged/
├── 2025-01-13-mon-saas/
│   └── .claude/
│       ├── CLAUDE.md
│       ├── agents/
│       │   ├── payment-guardian.md
│       │   └── data-architect.md
│       ├── commands/
│       │   ├── deploy.md
│       │   └── fix.md
│       ├── skills/
│       │   └── stripe-patterns/
│       └── rules/
│           └── security.md
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
/deploy
/fix
```

## Ce qui est genere

Les fichiers ne sont PAS des templates. Claude invente tout specifiquement pour ton projet:

- **Agents** avec des roles adaptes a tes besoins
- **Commandes** pour tes workflows quotidiens
- **Skills** avec les patterns de ton projet
- **Rules** basees sur tes contraintes

## License

MIT - Kevin Barfleur
