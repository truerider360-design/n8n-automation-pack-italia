# 01 — Lead Qualification

> Form sito → Claude classifica il lead → email personalizzata + record CRM

🚧 **Work in progress** — deadline ven 15/05/2026.

## Il problema

Le PMI ricevono lead dal form del sito ma non hanno tempo di:
- Distinguere lead caldi da timewaster
- Rispondere velocemente (cruciale: rispondere entro 5 minuti triplica la conversion)
- Tracciare tutto in un CRM in modo strutturato

## Come funziona

```
Webhook (form sito)
   ↓
Claude API (qualifica: hot / warm / cold + score 0-100 + reasoning)
   ↓
Switch
  ├─ hot/warm  → Email personalizzata + record CRM (Airtable/Sheets)
  └─ cold      → Log + email generica di cortesia
```

## Setup

_Documentazione completa al rilascio del workflow.json (ven 15/05)._

## Test

_Sezione in arrivo: payload di test + risultati attesi._

## Screenshot

_In arrivo._
