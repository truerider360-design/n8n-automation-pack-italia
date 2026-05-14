# 03 — Slack Daily Digest

> Multi-feed (RSS, GitHub, Reddit) → Claude digest → post in canale Slack

⏳ **Pianificato** — sviluppo previsto dom 17/05/2026.

## Il problema

Il tuo team ha bisogno di rimanere aggiornato su tante fonti (blog del settore, repo GitHub seguiti, subreddit) senza che ognuno debba aprirle ogni mattina. Un digest unico, sintetico, postato in Slack alle 09:00 fa il lavoro.

## Come funziona

```
Cron giornaliero (09:00)
   ↓
Fetch RSS + GitHub releases + Reddit top posts
   ↓
Claude: deduplica + sintetizza in 1 messaggio Slack
   ↓
Post in canale Slack (Block Kit formatting)
```

_Documentazione completa al rilascio._
