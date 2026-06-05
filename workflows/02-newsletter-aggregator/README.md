# 02 — Newsletter Aggregator

> 3 feed RSS (Marketing & AI) → filtro 7 giorni → Claude seleziona top 5 → digest HTML via email

✅ **Workflow completo** — importa `workflow.json` e segui il setup.

## Il problema

Curarsi una newsletter settimanale richiede ore: leggere le fonti, scegliere i pezzi, scrivere riassunti, formattare. Questo workflow automatizza il 90% — rimane solo leggere il digest che ti arriva in email ogni lunedì mattina.

## Come funziona

```
Schedule Trigger (ogni lunedì 09:00)
   ↓ [parallelo]
RSS Ninja Marketing IT  ──┐
RSS HubSpot Marketing   ──┤→ Merge Feeds
RSS VentureBeat AI      ──┘
   ↓
Filtra Articoli (ultimi 7 giorni, max 20 articoli)
   ↓
Prepara Prompt (costruisce il body per Claude)
   ↓
Claude API (seleziona top 5, riscrive titoli, riassume in italiano)
   ↓
Genera Newsletter (costruisce HTML email professionale)
   ↓
Invia Newsletter (SMTP → tua email)
```

## Feed RSS inclusi

| Feed | URL | Tema |
|------|-----|------|
| Ninja Marketing IT | https://www.ninja.it/feed/ | Marketing digitale italiano |
| HubSpot Marketing Blog | https://blog.hubspot.com/marketing/rss.xml | Marketing internazionale |
| VentureBeat AI | https://venturebeat.com/category/ai/feed/ | AI applicata al business |

> Puoi aggiungere/cambiare feed: clona uno dei nodi RSS e cambia l'URL. Ricorda di collegarlo al nodo Merge Feeds.

## Setup

### 1. Importa il workflow

n8n → **Workflows → + → Import from File** → seleziona `workflow.json`

### 2. Configura le credenziali

**Nodo `Claude API` — usa la stessa credenziale del Workflow 01**
Se hai già configurato "Anthropic API Key" nel workflow precedente, assegnala direttamente.

**Nodi `Invia Newsletter` — usa la stessa credenziale SMTP del Workflow 01**
- Apri il nodo `Invia Newsletter`
- Cambia `tuamail@tuaazienda.it` sia in `From Email` che in `To Email` con la tua email reale

### 3. Configura il trigger

Il workflow gira ogni **lunedì alle 09:00** (cron: `0 9 * * 1`).
Per cambiare orario/frequenza, apri il nodo `Schedule Trigger` e modifica l'espressione cron.

### 4. Attiva il workflow

Toggle **Inactive → Active**. Il prossimo lunedì alle 09:00 riceverai il primo digest.

## Test manuale

Per testare senza aspettare lunedì:
1. Apri il workflow in n8n
2. Clicca **Execute workflow** (pulsante in basso)
3. Controlla la tua email dopo circa 30-60 secondi

## Personalizzazione

| Cosa cambiare | Dove |
|---|---|
| Aggiungere un feed RSS | Aggiungi un nodo RSS Feed Read + collegalo al Merge Feeds |
| Finestra temporale (default: 7 giorni) | Nodo `Filtra Articoli`, riga `sevenDaysAgo.setDate(...)` |
| Numero articoli nel digest (default: top 5) | Nodo `Prepara Prompt`, modifica il numero nel prompt |
| Tema della newsletter | Nodo `Prepara Prompt`, modifica "Marketing e AI" nel prompt |
| Stile HTML della email | Nodo `Genera Newsletter`, modifica il codice HTML |
| Destinatario | Nodo `Invia Newsletter`, campo `To Email` |
| Orario/giorno invio | Nodo `Schedule Trigger`, campo `expression` |

## Output di esempio

Claude genera un JSON strutturato con:
- `titolo_newsletter`: titolo editoriale per la settimana
- `intro`: 2-3 righe introduttive
- `articoli[]`: 5 articoli con titolo riscritto in italiano, riassunto 3-4 frasi, tag tematico
- `chiusura`: firma informale

L'email finale è HTML responsive, visualizzabile su mobile e desktop.

## Costi stimati

- Claude Sonnet 4.6: ~€0.03–0.06 per esecuzione (prompt lungo ~3000 token + output ~1500 token)
- 4 esecuzioni/mese = ~€0.15–0.25/mese
- RSS feed: gratuiti, nessuna credenziale richiesta
- SMTP: dipende dal provider (Gmail: 500 email/giorno gratis)
