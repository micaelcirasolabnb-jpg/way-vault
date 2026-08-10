---
type: learning
date: 2026-08-10
tags: [git, hooks, reliability]
---

# L'hook di sync non deve mai bloccarsi

## Problema originale
`vault-auto-pull.sh` usava `git pull --ff-only ... || true`. Se il ramo locale e quello remoto divergevano, il pull falliva **in silenzio** — nessun errore visibile, ma i file remoti non arrivavano mai sul Mac. Così sono spariti per un po' 4 progetti che esistevano solo su GitHub.

## Fix
```bash
git pull --no-rebase --no-edit origin main >/dev/null 2>&1 || git merge --abort >/dev/null 2>&1 || true
```
Se il merge automatico fallisce, si annulla da solo (`merge --abort`) invece di lasciare il repo in uno stato sporco — e l'hook non blocca mai l'avvio della sessione.

## Estensione
Lo stesso hook ora assorbe anche i rami `origin/claude/*` dentro `main` in automatico. Vedi [[cloud-session-branch-behavior]].

Decisione collegata: [[ADR-001-cloud-sessions-vs-remote-control]]
