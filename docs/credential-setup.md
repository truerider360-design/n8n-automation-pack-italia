# Configurazione credenziali

Guida step-by-step per configurare ogni credenziale richiesta dai workflow del pack.

> 💡 **Suggerimento**: configura solo le credenziali del workflow che vuoi usare. Non serve fare tutto in una volta.

## 1. Anthropic Claude API

Necessaria per tutti e 5 i workflow (è il cervello AI del pack).

1. Vai su https://console.anthropic.com/
2. Login o crea un account
3. Sezione **API Keys** → **Create Key**
4. Copia la key (formato `sk-ant-api03-...`)
5. In n8n: **Credentials** → **New** → cerca **Anthropic API** → incolla la key → Save

**Costo indicativo**: ~€0.01 per chiamata media con Claude Sonnet 4 (lead qualification tipica = ~500 token input + 200 output).

**Tip**: imposta un budget alert su Anthropic Console per evitare sorprese in caso di loop indesiderati.

## 2. SendGrid

Necessaria per Workflow #1, #2, #4.

_Sezione in arrivo durante lo sviluppo dei workflow._

## 3. Airtable / Google Sheets

Necessaria per Workflow #1 come CRM.

_Sezione in arrivo durante lo sviluppo del Workflow #1 (ven 15/05)._

## 4. Slack

Necessaria per Workflow #3 e per le notifiche del Workflow #5.

_Sezione in arrivo durante lo sviluppo del Workflow #3._

## 5. Google Drive

Necessaria per Workflow #4.

_Sezione in arrivo durante lo sviluppo del Workflow #4._

## 6. Taskade (via MCP)

Necessaria per Workflow #4 — viene usata via MCP server collegato a n8n.

_Sezione in arrivo durante lo sviluppo del Workflow #4 (lun 18/05)._

## 7. Google My Business

Necessaria per Workflow #5.

_Sezione in arrivo durante lo sviluppo del Workflow #5 (mar 19/05)._
