---
type: learning
date: 2026-08-10
tags: [git, cloud-session]
---

# Le sessioni cloud: dove committano davvero

Verificato con due test end-to-end (progetti [[ecommerce]] e [[bnb]]):

- **Sessione nuova** dal telefono → committa **direttamente su `main`**.
- **Sessione ripresa** (che in passato si era già creata un ramo `claude/<nome>`) → continua a committare su quel ramo, non su `main`.

## Implicazione pratica
Per lavorare senza pensieri: **aprire una sessione nuova per ogni lavoro diverso**. Non serve scrivere "salva su main" nel prompt — non cambia il comportamento.

## Rete di sicurezza
Se una sessione ripresa lascia lavoro su un ramo separato, non resta orfano: vedi [[vault-sync-hook-never-blocks]] — l'hook lo assorbe da solo dentro `main` al prossimo avvio di una sessione su questo Mac.

Decisione collegata: [[ADR-001-cloud-sessions-vs-remote-control]]
