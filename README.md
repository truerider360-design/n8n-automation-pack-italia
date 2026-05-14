# 🇮🇹 n8n Automation Pack Italia

> 5 workflow n8n pronti all'uso per PMI italiane. Importi il `.json`, configuri le credenziali, automatizzi.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![n8n](https://img.shields.io/badge/n8n-1.x-EA4B71)](https://n8n.io)
[![Status](https://img.shields.io/badge/status-WIP-orange)](#)

---

## 🎯 Cosa trovi qui dentro

Cinque automazioni pensate per problemi reali di una PMI italiana — non template generici tradotti, ma flussi che integrano AI (Claude) per ridurre il lavoro umano dove pesa di più: triage lead, sintesi informazioni, prima bozza di comunicazioni, onboarding clienti, risposta a recensioni.

## 📦 I 5 Workflow

| # | Workflow | Cosa fa | Stato |
|---|----------|---------|-------|
| 01 | [Lead Qualification](workflows/01-lead-qualification/) | Form sito → AI classifica → email + CRM | 🚧 In corso |
| 02 | [Newsletter Aggregator](workflows/02-newsletter-aggregator/) | RSS multipli → AI riassume → email | ⏳ Pianificato |
| 03 | [Slack Daily Digest](workflows/03-slack-daily-digest/) | Multi-feed → AI digest → Slack | ⏳ Pianificato |
| 04 | [Onboarding Clienti](workflows/04-onboarding-clienti/) | Form → email + Drive + Taskade (MCP) | ⏳ Pianificato |
| 05 | [Risposta Recensioni](workflows/05-risposta-recensioni-google/) | Recensione GMB → bozza AI → approvazione | ⏳ Pianificato |

## 🚀 Come usare

1. Leggi [prerequisites.md](docs/prerequisites.md) per i requisiti tecnici
2. Configura le credenziali seguendo [credential-setup.md](docs/credential-setup.md)
3. Apri n8n → **Import from File** → seleziona il `workflow.json` del workflow desiderato
4. Configura le credenziali sui nodi e attiva il workflow

## 🛠️ Stack tecnico

- **n8n** 1.x (self-hosted o n8n.cloud)
- **Claude API** (anthropic-claude-sonnet-4) per AI
- **Google Workspace**, **Slack**, **Airtable/Sheets**, **SendGrid** come destinazioni

## 📜 Licenza

MIT — vedi [LICENSE](LICENSE). Sentiti libero di forkare, modificare, usare in produzione.

## 🤝 Author

Costruito da Francesco — [GitHub](https://github.com/truerider360-design)

---

*Repository v1.0 in arrivo: domenica 24 maggio 2026*
