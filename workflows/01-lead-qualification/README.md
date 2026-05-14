# 01 — Lead Qualification

> Form sito → Claude classifica il lead → email personalizzata + record Google Sheets

✅ **Workflow completo** — importa `workflow.json` e segui il setup qui sotto.

## Il problema

Le PMI ricevono lead dal form del sito ma non hanno tempo di:
- Distinguere lead caldi da timewaster
- Rispondere velocemente (rispondere entro 5 minuti triplica la conversion)
- Tracciare tutto in modo strutturato

## Come funziona

```
Webhook (form sito)
   ↓
Prepara Prompt  →  Claude API (classifica: hot / warm / cold + score 0-100)
   ↓
Parse Risposta
   ↓
Google Sheets (salva il lead con tutti i dati + classificazione)
   ↓
Router (IF)
  ├─ hot / warm  → Email personalizzata con tempi di risposta
  └─ cold        → Email di cortesia generica
```

## Criteri di classificazione Claude

| Classe | Score | Quando |
|--------|-------|--------|
| hot | 70–100 | Interesse esplicito, budget/urgenza chiari, azienda riconoscibile |
| warm | 40–69 | Interesse generico ma pertinente, settore rilevante |
| cold | 0–39 | Richiesta vaga, studenti, concorrenti, spam, fuori target |

## Setup

### 1. Importa il workflow

In n8n: **Workflows → Add workflow → Import from File** → seleziona `workflow.json`.

### 2. Configura le credenziali

Dopo l'import, n8n mostrerà i nodi con credenziali mancanti (icona rossa).

**Nodo `Claude API` — credenziale `Anthropic API Key`:**
1. Vai su [console.anthropic.com](https://console.anthropic.com) → API Keys → Create Key
2. In n8n: **Credentials → New → Header Auth**
   - Name: `x-api-key`
   - Value: `sk-ant-api03-...`
3. Assegna questa credential al nodo `Claude API`

**Nodo `Google Sheets` — credenziale `Google Sheets OAuth2`:**
1. In n8n: **Credentials → New → Google Sheets OAuth2 API**
2. Segui il flusso OAuth (richiede Google Cloud project con Sheets API abilitata)
3. Apri il nodo `Google Sheets`, incolla l'ID del tuo foglio nel campo `Document ID`
   - L'ID è la stringa lunga nell'URL: `docs.google.com/spreadsheets/d/`**`QUESTO_ID`**`/edit`

**Nodi `Email Calda` e `Email Cortesia` — credenziale `SMTP`:**
1. In n8n: **Credentials → New → SMTP**
2. Compila host, porta, utente e password del tuo provider (Gmail, Aruba, ecc.)
3. Cambia `tuamail@tuaazienda.it` nel campo `From Email` di entrambi i nodi
4. Personalizza firma e testi nei campi `Subject` e `Message`

### 3. Prepara il Google Sheet

Crea un foglio con questi nomi di colonna esatti nella riga 1 (il workflow usa `autoMapInputData`):

```
data_ricezione | nome | email | azienda | telefono | messaggio | classificazione | score | reasoning | priorita_risposta | descrizione_priorita
```

### 4. Collega il form del sito

Dopo aver attivato il workflow, copia l'URL del webhook da n8n (**Webhook → Copy URL**) e usalo come `action` del form HTML:

```html
<form method="POST" action="https://tuo-n8n.com/webhook/lead-qualification">
  <input name="nome"     type="text"  required />
  <input name="email"    type="email" required />
  <input name="azienda"  type="text" />
  <input name="telefono" type="tel" />
  <textarea name="messaggio" required></textarea>
  <button type="submit">Invia</button>
</form>
```

> I nomi dei campi (`nome`, `email`, `azienda`, `telefono`, `messaggio`) devono corrispondere esattamente.

### 5. Attiva il workflow

Toggle **Inactive → Active** in alto a destra. Il webhook è ora live.

## Test

Testa il webhook con curl prima di collegarlo al form:

```bash
curl -X POST https://tuo-n8n.com/webhook/lead-qualification \
  -H "Content-Type: application/json" \
  -d '{
    "nome": "Marco Rossi",
    "email": "marco@azienda-esempio.it",
    "azienda": "Azienda Esempio Srl",
    "telefono": "+39 02 1234567",
    "messaggio": "Buongiorno, siamo una PMI di 30 dipendenti e stiamo cercando una soluzione per automatizzare la gestione dei preventivi. Avremmo bisogno di partire entro giugno. Budget disponibile circa 5k. È possibile fissare una call questa settimana?"
  }'
```

Risultato atteso: classificazione `hot`, score ≥ 70, email personalizzata inviata, riga aggiunta al foglio.

**Test cold lead:**
```bash
curl -X POST https://tuo-n8n.com/webhook/lead-qualification \
  -H "Content-Type: application/json" \
  -d '{
    "nome": "Luca",
    "email": "luca@gmail.com",
    "azienda": "",
    "telefono": "",
    "messaggio": "Ciao, sto facendo una ricerca per la mia tesi e avrei qualche domanda"
  }'
```

Risultato atteso: classificazione `cold`, score ≤ 39, email di cortesia inviata.

## Personalizzazione

| Cosa cambiare | Dove |
|---|---|
| Modello Claude (es. claude-opus-4-7) | Nodo `Prepara Prompt`, campo `model` nel codice |
| Criteri di classificazione | Nodo `Prepara Prompt`, array `lines` |
| Template email hot/warm | Nodo `Email Calda`, campo `Message` |
| Template email cold | Nodo `Email Cortesia`, campo `Message` |
| Soglia hot/warm (default: ≠ cold) | Nodo `Router`, condizione IF |

## Costi stimati

- Claude Sonnet 4.5: ~€0.008–0.015 per qualificazione (≈500 token input + 150 output)
- Google Sheets: gratuito
- SMTP: dipende dal provider (Gmail free tier: 500 email/giorno)
