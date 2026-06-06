# Configurazione credenziali

Guida step-by-step per configurare ogni credenziale richiesta dai workflow del pack.

> 💡 **Suggerimento**: configura solo le credenziali del workflow che vuoi usare. Non serve fare tutto in una volta.

## Mappa credenziali → workflow

| Credenziale | Workflow | Tipo |
|---|---|---|
| Anthropic Claude API | 01 · 02 · 03 · 04 · 05 | Header Auth |
| SMTP (email) | 01 · 02 · 04 · 05 | SMTP |
| Google Sheets | 01 | OAuth2 |
| Slack | 03 | Bot Token |
| Google Drive | 04 | OAuth2 |
| Taskade | 04 | Header Auth (Bearer) |
| Google Business Profile | 05 | OAuth2 |

---

## 1. Anthropic Claude API

Necessaria per tutti e 5 i workflow (è il cervello AI del pack).

1. Vai su https://console.anthropic.com/ → login o crea un account
2. Sezione **API Keys** → **Create Key**
3. Copia la key (formato `sk-ant-api03-...`)
4. In n8n: **Credentials → New → Header Auth**
   - **Name**: `x-api-key`
   - **Value**: la tua key `sk-ant-api03-...`
5. Assegna questa credenziale al nodo `Claude API` di ogni workflow

> I workflow usano il modello `claude-sonnet-4-6`. Per cambiarlo, modifica il campo `model` nel nodo `Prepara Prompt`.

**Costo indicativo**: ~€0.01 per chiamata media con Claude Sonnet 4.6 (~500 token input + 200 output).

**Tip**: imposta un budget alert nella Console Anthropic per evitare sorprese in caso di loop indesiderati.

## 2. SMTP (email)

Necessaria per Workflow #1, #2, #4, #5. Funziona con qualsiasi provider SMTP (Gmail, Aruba, Register.it, ecc.) — non serve SendGrid.

1. In n8n: **Credentials → New → SMTP**
2. Compila:
   - **Host**: es. `smtp.gmail.com`, `smtps.aruba.it`
   - **Port**: `465` (SSL) oppure `587` (TLS)
   - **User** / **Password**: le credenziali della tua casella
3. Nei nodi email di ogni workflow (`Email Calda`, `Email Cortesia`, `Invia Newsletter`, `Email Benvenuto`, `Email Notifica Owner`) sostituisci `tuamail@tuaazienda.it` nel campo `From Email` con il tuo indirizzo reale.

> Gmail: usa una **App Password** (richiede 2FA attiva), non la password normale. Free tier: ~500 email/giorno.

## 3. Google Sheets (OAuth2)

Necessaria per Workflow #1 — fa da CRM dei lead.

1. Su [Google Cloud Console](https://console.cloud.google.com) crea/usa un progetto e abilita la **Google Sheets API**
2. In n8n: **Credentials → New → Google Sheets OAuth2 API**
3. Completa il flusso OAuth con il tuo account Google
4. Apri il nodo `Google Sheets` del Workflow 01 e incolla l'**ID del foglio** nel campo `Document ID`
   - L'ID è la stringa lunga nell'URL: `docs.google.com/spreadsheets/d/`**`QUESTO_ID`**`/edit`
5. Prepara il foglio con queste intestazioni esatte nella riga 1:
   `data_ricezione | nome | email | azienda | telefono | messaggio | classificazione | score | reasoning | priorita_risposta | descrizione_priorita`

## 4. Slack (Bot Token)

Necessaria per Workflow #3.

1. Vai su [api.slack.com/apps](https://api.slack.com/apps) → **Create New App → From scratch**
2. Nome: `n8n Digest Bot` → seleziona il tuo workspace
3. **OAuth & Permissions → Bot Token Scopes** → aggiungi `chat:write` e `chat:write.public`
4. **Install to Workspace** → autorizza
5. Copia il **Bot OAuth Token** (inizia con `xoxb-...`)
6. In n8n: **Credentials → New → Slack API** → Token type `Bot` → incolla il token
7. Assegna la credenziale al nodo `Slack`. Invita il bot nel canale di destinazione: `/invite @n8n Digest Bot`

## 5. Google Drive (OAuth2)

Necessaria per Workflow #4.

1. Su Google Cloud Console abilita la **Google Drive API** (puoi riusare il progetto di Google Sheets)
2. In n8n: **Credentials → New → Google Drive OAuth2 API** → completa il flusso OAuth
3. Assegna la credenziale al nodo `Google Drive — Crea Cartella`
4. (Opzionale) imposta una cartella padre nel campo `Folder` del nodo

## 6. Taskade (API token)

Necessaria per Workflow #4. Si usa un Personal API Token via Header Auth — **non** un MCP server.

1. Vai su [taskade.com](https://www.taskade.com) → **Settings → API** → genera un **Personal API Token**
2. In n8n: **Credentials → New → Header Auth**
   - **Name**: `Authorization`
   - **Value**: `Bearer IL_TUO_TOKEN_TASKADE`
3. Assegna la credenziale al nodo `Taskade — Crea Progetto`
4. Imposta il **Folder ID**: in Taskade apri la cartella di destinazione, copia l'ID dalla URL `taskade.com/f/`**`QUESTO_ID`** e sostituisci `YOUR_TASKADE_FOLDER_ID` nell'URL del nodo

## 7. Google Business Profile (OAuth2)

Necessaria per Workflow #5. È il passaggio più delicato — richiede OAuth2 con scope `business.manage`.

1. Su [Google Cloud Console](https://console.cloud.google.com) abilita **My Business Account Management API** + **My Business Reviews API**
2. **Credentials → Create Credentials → OAuth 2.0 Client ID** → tipo **Web application**
3. Authorized redirect URI: `https://<IL-TUO-N8N>/rest/oauth2-credential/callback` (sostituisci con l'URL della tua istanza n8n)
4. In n8n: **Credentials → New → OAuth2 API**
   - Grant Type: `Authorization Code`
   - Authorization URL: `https://accounts.google.com/o/oauth2/auth`
   - Access Token URL: `https://oauth2.googleapis.com/token`
   - Client ID / Secret: dai passaggi precedenti
   - Scope: `https://www.googleapis.com/auth/business.manage`
   - Clicca **Connect** e autorizza con l'account collegato a Google Business Profile
5. Trova **Account ID** e **Location ID** e impostali nell'URL del nodo `GMB — Lista Recensioni`

> La location deve essere verificata su Google Business Profile. Per i dettagli su come ricavare Account/Location ID e per i dati di test, vedi `workflows/05-risposta-recensioni-google/README.md`.
