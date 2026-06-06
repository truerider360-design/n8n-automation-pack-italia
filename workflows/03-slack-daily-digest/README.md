# 03 — Slack Daily Digest

> 5 fonti (RSS + GitHub releases) → filtro 24h → Claude top 5 → post in #general

✅ **Workflow completo** — importa `workflow.json` e segui il setup.

## Il problema

Il team deve restare aggiornato su marketing, AI e tool tecnici senza aprire 5 feed ogni mattina. Un messaggio Slack alle 09:00, già filtrato e riassunto da Claude, fa il lavoro.

## Come funziona

```
Schedule Trigger (lun–ven 09:00)
   ↓ [5 branch paralleli]
RSS Ninja Marketing IT     ──┐
RSS HubSpot Marketing      ──┤
RSS VentureBeat AI         ──┼→ Merge Fonti
GitHub n8n Releases        ──┤
GitHub LangChain Releases  ──┘
   ↓
Filtra 24 Ore (fallback: ultimi disponibili se weekend/festivo)
   ↓
Prepara Prompt → Claude API (seleziona top 5, riassume in italiano)
   ↓
Formatta Messaggio Slack (emoji + link cliccabili)
   ↓
Post in #general
```

## Fonti incluse

| Fonte | Tipo | URL |
|-------|------|-----|
| Ninja Marketing IT | RSS | https://www.ninja.it/feed/ |
| HubSpot Marketing | RSS | https://blog.hubspot.com/marketing/rss.xml |
| VentureBeat AI | RSS | https://venturebeat.com/category/ai/feed/ |
| n8n Releases | GitHub Atom | https://github.com/n8n-io/n8n/releases.atom |
| LangChain Releases | GitHub Atom | https://github.com/langchain-ai/langchain/releases.atom |

## Setup

### 1. Importa il workflow

n8n → **Workflows → + → Import from File** → seleziona `workflow.json`

### 2. Credenziale Anthropic

Stessa del Workflow 01 e 02 — assegna "Anthropic API Key" al nodo `Claude API`.

### 3. Credenziale Slack (Bot Token) — unica nuova credenziale

1. Vai su [api.slack.com/apps](https://api.slack.com/apps) → **Create New App → From scratch**
2. Nome: `n8n Digest Bot` — seleziona il tuo workspace
3. Vai su **OAuth & Permissions → Scopes → Bot Token Scopes** → aggiungi:
   - `chat:write`
   - `chat:write.public`
4. Clicca **Install to Workspace** → autorizza
5. Copia il **Bot OAuth Token** (inizia con `xoxb-...`)
6. In n8n: **Credentials → New → Slack API**
   - Token type: `Bot`
   - Access Token: incolla il token `xoxb-...`
7. Assegna questa credenziale al nodo `Slack`

### 4. Canale di destinazione

Il workflow posta in `#general` per default.
Per cambiare canale: apri il nodo `Slack` → campo `Channel` → scrivi `#nome-canale`.

> Il bot deve essere nel canale per postarci. Invitalo con `/invite @n8n Digest Bot` in Slack.

### 5. Attiva il workflow

Toggle **Inactive → Active**. Il digest parte ogni lunedì–venerdì alle 09:00.

## Esempio di messaggio Slack generato

```
📰 *Daily Digest venerdì 15 maggio*

🤖 *Nuovo modello AI open-weight si avvicina ai modelli proprietari sul coding*
Un rilascio recente abbatte i costi di inferenza mantenendo qualità competitiva sui task di programmazione.
<https://venturebeat.com/...|Leggi →>

📦 *n8n v1.48 — nuovo nodo AI Agent*
La nuova versione introduce un nodo nativo per creare agenti AI multi-step senza codice.
<https://github.com/n8n-io/n8n/releases/...|Leggi →>

📊 *Come il marketing conversazionale aumenta la retention del 23%*
Uno studio HubSpot analizza l'impatto dei chatbot AI sulla fidelizzazione clienti B2B.
<https://blog.hubspot.com/...|Leggi →>

_Generato automaticamente · n8n + Claude_
```

## Personalizzazione

| Cosa cambiare | Dove |
|---|---|
| Aggiungere una fonte RSS | Nuovo nodo RSS Feed Read + collegalo a Merge Fonti |
| Cambiare repo GitHub monitorati | Modifica URL nei nodi `GitHub * Releases` |
| Canale Slack destinatario | Nodo `Slack`, campo `Channel` |
| Finestra temporale (default: 24h) | Nodo `Filtra 24 Ore`, riga `setHours(... - 24)` |
| Numero articoli nel digest (default: 5) | Nodo `Prepara Prompt`, modifica numero nel prompt |
| Orario invio (default: 09:00 lun-ven) | Nodo `Schedule Trigger`, campo `expression` |

## Costi stimati

- Claude Sonnet 4.6: ~€0.02–0.04 per esecuzione (prompt ~2000 token + output ~600 token)
- 5 giorni/settimana × 4 settimane = 20 esecuzioni/mese → ~€0.60–0.80/mese
- RSS + GitHub Atom: gratuiti, nessuna API key
- Slack API: gratuita per workspace standard

## Download

**[→ workflow.json (raw)](https://raw.githubusercontent.com/truerider360-design/n8n-automation-pack-italia/main/workflows/03-slack-daily-digest/workflow.json)**
