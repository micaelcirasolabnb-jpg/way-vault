---
name: cloud-sessions-push-to-branches
description: Sessioni cloud nuove committano su main; quelle riprese restano sul loro ramo claude/*
metadata: 
  node_type: memory
  type: project
  originSessionId: b327bab1-edfc-4385-a8a5-825c0bae23ec
  modified: 2026-08-10T18:09:42.213Z
---

Le sessioni cloud (claude.ai/code, usate dal telefono) committano **direttamente su `main`**
se sono sessioni nuove. Se invece si riprende una sessione che in passato si era creata un
ramo `claude/<nome>`, continua a committare lì.

Verificato il 2026-08-10 con due test end-to-end:
- sessione ripresa → commit `1e6fe43` sul ramo `claude/claude-macbook-connection-urlib6`
- sessione nuova → commit `77326d6` dritto su `main`

**Why:** l'utente lavora dal telefono col MacBook chiuso e non vuole gestire rami a mano.

**How to apply:** dire all'utente di **aprire una sessione nuova** per ogni lavoro diverso —
così finisce sempre su main. Non serve scrivere "committa su main" nel prompt.
Come rete di sicurezza, `~/.claude/hooks/vault-auto-pull.sh` (SessionStart) fa il merge
automatico di eventuali rami `origin/claude/*` dentro main, così il lavoro di una sessione
ripresa non resta orfano. Vedi [[vault-sync-hooks]].
