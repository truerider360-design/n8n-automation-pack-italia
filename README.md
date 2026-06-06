# 🇮🇹 n8n Automation Pack Italia

> 5 workflow n8n pronti all'uso per PMI italiane. Importi il `.json`, configuri le credenziali, automatizzi.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![n8n](https://img.shields.io/badge/n8n-1.x-EA4B71)](https://n8n.io)
[![Status](https://img.shields.io/badge/status-ready-brightgreen)](#)
[![Release](https://img.shields.io/badge/release-v1.0.0-blue)](https://github.com/truerider360-design/n8n-automation-pack-italia/releases)

---

## 🎯 Cosa trovi qui dentro

Cinque automazioni pensate per problemi reali di una PMI italiana — non template generici tradotti, ma flussi che integrano AI (Claude) per ridurre il lavoro umano dove pesa di più: triage lead, sintesi informazioni, prima bozza di comunicazioni, onboarding clienti, risposta a recensioni.

## 📦 I 5 Workflow

| # | Workflow | Cosa fa | Stato |
|---|----------|---------|-------|
| 01 | [Lead Qualification](workflows/01-lead-qualification/) | Form sito → AI classifica → email + Google Sheets | ✅ Pronto |
| 02 | [Newsletter Aggregator](workflows/02-newsletter-aggregator/) | RSS multipli → AI riassume → email settimanale | ✅ Pronto |
| 03 | [Slack Daily Digest](workflows/03-slack-daily-digest/) | Multi-feed + GitHub releases → AI digest → Slack | ✅ Pronto |
| 04 | [Onboarding Clienti](workflows/04-onboarding-clienti/) | Form → email benvenuto + Google Drive + Taskade | ✅ Pronto |
| 05 | [Risposta Recensioni Google](workflows/05-risposta-recensioni-google/) | Recensioni GMB → bozze AI → email owner | ✅ Pronto |

## 🚀 Come usare

1. Leggi [prerequisites.md](docs/prerequisites.md) per i requisiti tecnici
2. Configura le credenziali seguendo [credential-setup.md](docs/credential-setup.md)
3. Apri n8n → **Import from File** → seleziona il `workflow.json` del workflow desiderato
4. Configura le credenziali sui nodi e attiva il workflow

## 🛠️ Stack tecnico

- **n8n** 1.x (self-hosted o n8n.cloud)
- **Claude API** (`claude-sonnet-4-6`) per AI
- **Google Sheets / Google Drive** (OAuth2)
- **Slack** (Bot Token)
- **SMTP** per email
- **Google Business Profile API** per recensioni
- **Taskade API** per project management

## 📂 Struttura repository

```
workflows/
├── 01-lead-qualification/
│   ├── workflow.json
│   └── README.md
├── 02-newsletter-aggregator/
├── 03-slack-daily-digest/
├── 04-onboarding-clienti/
└── 05-risposta-recensioni-google/
docs/
├── prerequisites.md
└── credential-setup.md
```

## 📜 Licenza

MIT — vedi [LICENSE](LICENSE). Sentiti libero di forkare, modificare, usare in produzione.

## 🤝 Autore

Costruito da **RiderVision Studio** — studio di automazione AI con base a Roma.
[GitHub](https://github.com/truerider360-design) · truerider360@gmail.com

Hai bisogno di un'automazione su misura per la tua PMI? Scrivimi.

---

*v1.0.0 — rilasciato il 24 maggio 2026*
