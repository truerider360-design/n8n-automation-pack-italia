# 04 — Onboarding Clienti

> Webhook firma contratto → Claude genera email → [Email SMTP + Cartella Drive + Progetto Taskade] in parallelo

✅ **Workflow completo** — importa `workflow.json` e segui il setup.

## Il problema

Ogni nuovo cliente richiede 15 minuti di click ripetitivi: email di benvenuto, cartella Drive con i template, apertura task nel PM tool. Questo workflow automatizza tutto in 10 secondi dal momento in cui ricevi il trigger.

## Come funziona

```
Webhook POST (form firma / Tally / Typeform / trigger manuale)
   ↓
Prepara Dati Cliente (normalizza campi + costruisce prompt Claude)
   ↓
Claude API (genera email di benvenuto personalizzata)
   ↓
Parse Email Claude (estrae oggetto + corpo HTML)
   ↓ [3 branch paralleli]
   ├─ Email Benvenuto (SMTP → cliente)
   ├─ Google Drive — Crea Cartella (nominata "Azienda — Onboarding 2026")
   └─ Taskade — Crea Progetto (con 7 task standard di onboarding)
```

## Task standard creati in Taskade

Il progetto viene creato con questa checklist predefinita:
- [ ] Invio questionario iniziale
- [ ] Kickoff call pianificato
- [ ] Accesso condiviso tools e credenziali
- [ ] Prima deliverable definita e approvata
- [ ] Check-in settimana 1
- [ ] Check-in settimana 2
- [ ] Review e chiusura onboarding

## Campi attesi dal Webhook

Il form/tool che invia il trigger deve passare questi campi in JSON:

```json
{
  "nome":     "Mario Rossi",
  "email":    "mario@azienda.it",
  "azienda":  "Azienda Srl",
  "servizio": "consulenza SEO",
  "data_inizio": "15/05/2026"
}
```

> I campi `azienda`, `servizio` e `data_inizio` sono opzionali — il workflow ha fallback per tutti.

## Setup

### 1. Importa il workflow

n8n → **Workflows → + → Import from File** → seleziona `workflow.json`

### 2. Credenziale Anthropic

Stessa dei workflow precedenti — assegna "Anthropic API Key" al nodo `Claude API`.

### 3. Credenziale SMTP

Stessa dei workflow precedenti — assegna al nodo `Email Benvenuto`.
Cambia `tuamail@tuaazienda.it` nel campo `From Email`.

### 4. Credenziale Google Drive OAuth2

Se non l'hai già configurata:
1. In n8n: **Credentials → New → Google Drive OAuth2 API**
2. Segui il flusso OAuth con il tuo account Google
3. Assegna la credenziale al nodo `Google Drive — Crea Cartella`

**Cartella di destinazione (opzionale):**
Per default crea le cartelle nel root di Drive. Per scegliere una cartella specifica:
1. Apri il nodo `Google Drive — Crea Cartella`
2. Campo `Folder` → seleziona la cartella padre desiderata

### 5. Credenziale Taskade API Key — unica nuova credenziale

1. Vai su [taskade.com](https://www.taskade.com) → **Settings → API**
2. Genera un **Personal API Token**
3. In n8n: **Credentials → New → Header Auth**
   - Name: `Authorization`
   - Value: `Bearer IL_TUO_TOKEN_TASKADE`
4. Assegna questa credenziale al nodo `Taskade — Crea Progetto`

**Configura il Folder ID Taskade:**
1. In Taskade, apri la cartella dove vuoi creare i progetti cliente
2. Copia l'ID dalla URL: `taskade.com/f/`**`QUESTO_ID`**
3. Nel nodo `Taskade — Crea Progetto`, sostituisci `YOUR_TASKADE_FOLDER_ID` nell'URL con il tuo ID

### 6. Attiva il workflow

Toggle **Inactive → Active**.

## Test

```bash
curl -X POST https://tuo-n8n.com/webhook/onboarding-cliente \
  -H "Content-Type: application/json" \
  -d '{
    "nome": "Giulia Ferrari",
    "email": "giulia@startup.it",
    "azienda": "Startup Innovativa Srl",
    "servizio": "automazione marketing",
    "data_inizio": "20/05/2026"
  }'
```

Risultato atteso entro 10 secondi:
- ✅ Email personalizzata ricevuta da `giulia@startup.it`
- ✅ Cartella `Startup Innovativa Srl — Onboarding 2026` creata in Drive
- ✅ Progetto `Onboarding — Startup Innovativa Srl` creato in Taskade con 7 task

## Personalizzazione

| Cosa cambiare | Dove |
|---|---|
| Task standard di onboarding | Nodo `Prepara Dati Cliente`, array `tasks` |
| Tono dell'email Claude | Nodo `Prepara Dati Cliente`, prompt nel campo `lines` |
| Cartella Drive di destinazione | Nodo `Google Drive — Crea Cartella`, campo `Folder` |
| Formato nome cartella Drive | Nodo `Prepara Dati Cliente`, riga `nome_cartella` |
| Aggiungere invio email interno (notifica a te) | Aggiungi un 4° nodo `emailSend` nel branch parallelo |

## Costi stimati

- Claude Sonnet 4.6: ~€0.01–0.02 per onboarding (prompt ~400 token + output ~600 token)
- Google Drive: gratuito
- Taskade: piano free include API access con limiti
- SMTP: dipende dal provider

## Download

**[→ workflow.json (raw)](https://raw.githubusercontent.com/truerider360-design/n8n-automation-pack-italia/main/workflows/04-onboarding-clienti/workflow.json)**
