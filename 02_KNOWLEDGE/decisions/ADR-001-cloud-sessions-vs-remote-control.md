---
type: decision
date: 2026-08-10
tags: [architecture, mobile, infrastructure]
---

# ADR-001 — Sessioni cloud invece di Remote Control

## Contesto
Obiettivo: mandare comandi dal telefono, da ovunque, e far iniziare a lavorare Claude — senza dover tenere il MacBook acceso, alimentato, o dover rovinare la batteria.

## Opzioni valutate
1. **Remote Control** — il telefono pilota una sessione che gira sul Mac. Richiede il Mac sempre acceso e sveglio. Con lo schermo chiuso e a batteria, macOS sospende comunque il sistema: non aggirabile.
2. **Sessioni cloud** (claude.ai/code) — girano sui server di Anthropic, non sul Mac. Il Mac può restare spento o chiuso.

## Decisione
Sessioni cloud. Il punto di contatto tra telefono e Mac non è una connessione diretta, ma **GitHub**: la sessione cloud legge/scrive nel vault, il Mac sincronizza al riavvio tramite `vault-auto-pull.sh` / `vault-auto-backup.sh`.

## Conseguenze
- Il Mac può essere chiuso in ogni momento senza interrompere nulla.
- Il lavoro dal telefono arriva su GitHub subito; arriva su questo Mac solo alla sessione successiva (non è live).
- Vedi [[cloud-session-branch-behavior]] per come le sessioni cloud committano.
- Vedi [[vault-sync-hook-never-blocks]] per come il Mac assorbe quel lavoro senza mai bloccarsi.
