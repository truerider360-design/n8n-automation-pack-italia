# Prerequisites

Requisiti tecnici per usare i workflow di questo pack.

## n8n

- **Versione**: 1.x o superiore
- **Hosting**: self-hosted (consigliato per privacy dei dati cliente) oppure n8n.cloud
- **Risorse minime**: 1 vCPU, 1GB RAM, 10GB disco
- **Nodi base usati**: Webhook, HTTP Request, Code, IF/Switch, Cron
- **Nodi servizio**: Anthropic, Google Sheets, Google Drive, Slack, RSS, Taskade, Send Email

## Account e API keys

Per i 5 workflow del pack ti servono account/credenziali sui servizi seguenti (solo quelli del workflow che intendi usare):

| Servizio | Workflow | Tipo credenziale | Costo |
|----------|----------|------------------|-------|
| Anthropic Claude API | 01, 02, 03, 04, 05 | API key (Header Auth) | Pay-as-you-go (~€0.01/qualificazione lead) |
| SMTP (qualsiasi provider) | 01, 02, 04, 05 | Host/porta/utente/password | Free tier provider (Gmail ~500 email/giorno) |
| Google Sheets | 01 | OAuth2 | Gratis |
| RSS feeds | 02, 03 | Nessuna | Gratis |
| Slack | 03 | Bot OAuth Token | Gratis |
| GitHub Releases (Atom feed) | 03 | Nessuna | Gratis |
| Google Drive | 04 | OAuth2 | Gratis (15GB) |
| Taskade | 04 | API token (Header Auth) | Free tier con limiti |
| Google My Business | 05 | OAuth2 | Gratis |

## Skill richieste

- Familiarità base con n8n (importare workflow, configurare credenziali, attivare)
- Capacità di leggere un `curl` per testare i webhook
- **Nessun codice richiesto** (è utile saper leggere un JS leggero per il nodo Code dove presente)

---

Vedi [credential-setup.md](credential-setup.md) per le istruzioni passo-passo di configurazione di ogni credenziale.
