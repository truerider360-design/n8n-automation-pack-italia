# Changelog

Tutte le modifiche rilevanti a questo progetto verranno documentate in questo file.

Il formato si basa su [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), e questo progetto segue il [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

_Nessuna modifica pendente._

---

## [1.0.0] - 2026-05-24

### Added
- **Workflow 01 — Lead Qualification**: Webhook → Claude classifica lead (hot/warm/cold) → Google Sheets → email segmentata
- **Workflow 02 — Newsletter Aggregator**: Schedule settimanale → 3 feed RSS → Claude seleziona top 5 → newsletter HTML via email
- **Workflow 03 — Slack Daily Digest**: Schedule giornaliero → 5 feed (RSS + GitHub releases) → Claude digest → messaggio Slack
- **Workflow 04 — Onboarding Clienti**: Webhook → Claude genera email benvenuto → Google Drive crea cartella → Taskade crea progetto
- **Workflow 05 — Risposta Recensioni Google**: Polling giornaliero Google My Business → Claude genera bozze risposte → email HTML all'owner
- README master con badge, tabella workflow e struttura repository
- README dettagliato per ogni workflow con setup, test e personalizzazione
- `docs/prerequisites.md` e `docs/credential-setup.md`
- Licenza MIT

### Stack
- n8n 1.x, Claude API (claude-sonnet-4-5), Google Sheets, Google Drive, Slack, SMTP, Google Business Profile API, Taskade API

---

## [0.1.0] - 2026-05-10

### Added
- Scaffolding iniziale del repository
- Placeholder README per ogni workflow (01-05)
