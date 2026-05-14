# 02 — Newsletter Aggregator

> RSS multipli → Claude riassume → email HTML settimanale

⏳ **Pianificato** — sviluppo previsto sab 16/05/2026.

## Il problema

Curare una newsletter settimanale richiede ore: leggere le fonti, scegliere i pezzi rilevanti, scrivere riassunti, formattare. Automatizzando il 90% del lavoro, resta solo il review finale.

## Come funziona

```
Cron (settimanale, lunedì 09:00)
   ↓
Leggi N feed RSS (parallelo)
   ↓
Filtra ultime 7 giorni
   ↓
Claude: riassume + sceglie top 5
   ↓
Genera HTML newsletter
   ↓
Invia via SendGrid
```

_Documentazione completa al rilascio._
