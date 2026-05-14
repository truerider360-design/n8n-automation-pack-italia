# 04 — Onboarding Clienti

> Webhook firma contratto → email benvenuto + cartella Drive + task Taskade (via MCP)

⏳ **Pianificato** — sviluppo previsto lun 18/05/2026.

## Il problema

Quando firmi un nuovo cliente devi: mandare email di benvenuto, creare cartella condivisa Drive con i template, aprire i task del progetto nel tuo PM tool. Sono 15 minuti di click ripetitivi a ogni firma.

## Come funziona

```
Webhook (es. da Tally, Typeform, Stripe)
   ↓
├─ Email benvenuto (SendGrid)
├─ Crea cartella in Google Drive + copia template
└─ Crea progetto Taskade con task standard (via MCP server) ★
```

★ Questo workflow è l'unico che **integra MCP Taskade** direttamente in n8n — usato come autopromozione tecnica nel post di lancio LinkedIn.

_Documentazione completa al rilascio._
