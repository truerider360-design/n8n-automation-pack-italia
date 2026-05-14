# Prerequisites

Requisiti tecnici per usare i workflow di questo pack.

## n8n

- **Versione**: 1.x o superiore
- **Hosting**: self-hosted (consigliato per privacy dei dati cliente) oppure n8n.cloud
- **Risorse minime**: 1 vCPU, 1GB RAM, 10GB disco
- **Nodi base usati**: Webhook, HTTP Request, Code, IF/Switch, Cron
- **Nodi servizio**: Anthropic, Google Drive, Slack, RSS, Airtable, Send Email

## Account e API keys

Per i 5 workflow del pack ti servono account/credenziali sui servizi seguenti (solo quelli del workflow che intendi usare):

| Servizio | Workflow | Tipo credenziale | Costo |
|----------|----------|------------------|-------|
| Anthropic Claude API | 01, 02, 03, 04, 05 | API key | Pay-as-you-go (~€0.01/qualificazione lead) |
| SendGrid (o SMTP) | 01, 02, 04 | API key | Free tier 100 email/giorno |
| Airtable (o Google Sheets) | 01 | Personal access token | Free fino 1000 record/base |
| RSS feeds | 02, 03 | Nessuna | Gratis |
| Slack | 03 | Bot OAuth | Gratis |
| GitHub API (releases feed) | 03 | Personal access token (read-only) | Gratis |
| Google Drive | 04 | OAuth2 | Gratis (15GB) |
| Taskade (via MCP) | 04 | OAuth | Free tier con limiti |
| Google My Business API | 05 | OAuth2 | Gratis |

## Skill richieste

- Familiarità base con n8n (importare workflow, configurare credenziali, attivare)
- Capacità di leggere un `curl` per testare i webhook
- **Nessun codice richiesto** (è utile saper leggere un JS leggero per il nodo Code dove presente)

---

Vedi [credential-setup.md](credential-setup.md) per le istruzioni passo-passo di configurazione di ogni credenziale.
