# 05 — Risposta Recensioni Google

> Polling giornaliero Google My Business → Claude genera bozze risposte personalizzate → Email all'owner con copia-incolla pronto

## Come funziona

```
Schedule Trigger (09:00 ogni giorno)
   ↓
Google Business Profile API → lista recensioni
   ↓
Filtra solo quelle senza risposta (max 5)
   ↓
IF nessuna nuova → stop
   ↓
Claude genera risposta per ogni recensione:
   ├─ ⭐⭐⭐⭐⭐ (4-5 stelle) → ringraziamento personalizzato
   └─ ⭐⭐⭐ (1-3 stelle) → empatia + invito a risolvere offline
   ↓
Email HTML all'owner con bozze pronte al copia-incolla
```

> **Design scelta**: il workflow NON pubblica automaticamente. Ricevi la bozza, la revisioni e la pubblichi tu su Google Business Profile. Sulle recensioni negative la revisione umana è fondamentale.

---

## Setup

### 1. Credenziale Google Business Profile (OAuth2)

Questo è il passaggio più delicato. L'API Google My Business richiede OAuth2 con scope `https://www.googleapis.com/auth/business.manage`.

**Passaggi:**
1. Vai su [Google Cloud Console](https://console.cloud.google.com)
2. Crea un progetto (o usa quello già esistente per Google Sheets)
3. Abilita le API: `My Business Account Management API` + `My Business Reviews API`
4. Vai su **APIs & Services → Credentials → Create Credentials → OAuth 2.0 Client ID**
5. Tipo: **Web application**
6. Authorized redirect URI: `https://n8n.srv1196637.hstgr.cloud/rest/oauth2-credential/callback`
7. Salva Client ID e Client Secret

**In n8n:**
1. **Settings → Credentials → New → OAuth2 API**
2. Nome: `Google Business OAuth2`
3. Grant Type: `Authorization Code`
4. Authorization URL: `https://accounts.google.com/o/oauth2/auth`
5. Access Token URL: `https://oauth2.googleapis.com/token`
6. Client ID / Secret: dai passaggi precedenti
7. Scope: `https://www.googleapis.com/auth/business.manage`
8. Clicca **Connect** e autorizza con l'account Google associato a Google My Business

### 2. Trova Account ID e Location ID

Dopo aver connesso la credenziale, esegui questa chiamata API per trovare i tuoi ID:

**Account ID** — nel nodo `GMB — Lista Recensioni`, cambia temporaneamente l'URL in:
```
https://mybusinessaccountmanagement.googleapis.com/v1/accounts
```
Esegui il nodo — la risposta conterrà il tuo `name` nel formato `accounts/123456789`. Quello è il tuo Account ID.

**Location ID** — usa l'URL:
```
https://mybusinessbusinessinformation.googleapis.com/v1/accounts/YOUR_ACCOUNT_ID/locations
```
La risposta contiene i tuoi `name` nel formato `locations/987654321`.

### 3. Configura il nodo GMB

Nel nodo **GMB — Lista Recensioni**, imposta l'URL finale:
```
https://mybusiness.googleapis.com/v4/accounts/YOUR_ACCOUNT_ID/locations/YOUR_LOCATION_ID/reviews
```
Sostituisci `YOUR_ACCOUNT_ID` e `YOUR_LOCATION_ID` con i valori trovati al passo precedente.

### 4. Credenziale Anthropic

Usa la stessa credenziale **Header Auth** già configurata nei workflow precedenti:
- **Name**: `x-api-key`
- **Value**: la tua API key Anthropic

### 5. Credenziale SMTP

Usa la stessa credenziale SMTP già configurata nei workflow precedenti.

### 6. Configura email

Nel nodo **Email Notifica Owner**:
- **From Email**: il tuo indirizzo mittente
- **To Email**: la tua email dove ricevere le notifiche

---

## Test manuale

Poiché il workflow dipende dall'API GMB, per testarlo puoi:

1. Importa il workflow in n8n
2. Configura tutte le credenziali e gli ID
3. Apri il workflow, clicca su **Test Workflow**
4. Il nodo GMB tenterà la chiamata API reale

**Oppure testa con dati simulati:**
Sostituisci temporaneamente il nodo `GMB — Lista Recensioni` con un nodo **Set** che restituisce dati fittizi:

```json
{
  "reviews": [
    {
      "name": "accounts/123/locations/456/reviews/r1",
      "reviewer": { "displayName": "Mario Rossi" },
      "starRating": "FIVE",
      "comment": "Ottimo servizio, personale gentilissimo!",
      "createTime": "2026-05-15T10:00:00Z",
      "reviewReply": null
    },
    {
      "name": "accounts/123/locations/456/reviews/r2",
      "reviewer": { "displayName": "Anna Bianchi" },
      "starRating": "TWO",
      "comment": "Tempi di attesa troppo lunghi, delusa.",
      "createTime": "2026-05-14T15:00:00Z",
      "reviewReply": null
    }
  ]
}
```

> ⚠️ Nota: il campo `starRating` nell'API GMB è una stringa (`"FIVE"`, `"FOUR"`, `"THREE"`, etc.). Il nodo `Filtra Senza Risposta` usa già questa struttura. Se noti che il conteggio stelle non appare correttamente nell'email, aggiorna il nodo `Genera Email HTML` per mappare le stringhe ai numeri.

---

## Email di output — esempio

```
Oggetto: 📋 2 nuova/e recensione/i Google da rispondere — venerdì 15 maggio 2026

🟢 Recensione Positiva — ⭐⭐⭐⭐⭐ — Mario Rossi
  Commento: "Ottimo servizio, personale gentilissimo!"
  Bozza: "Grazie mille Mario per le tue splendide parole! Siamo felici..."

🔴 Recensione Negativa — ⭐⭐ — Anna Bianchi
  Commento: "Tempi di attesa troppo lunghi, delusa."
  Bozza: "Cara Anna, ci dispiace molto per la tua esperienza..."
```

---

## Personalizzazione

| Cosa cambiare | Dove |
|---|---|
| Tono/stile delle risposte | Nodo `Prepara Prompt Claude` → modifica il prompt |
| Numero massimo di recensioni per run | Nodo `Filtra Senza Risposta` → `.slice(0, 5)` |
| Orario polling | Nodo `Ogni Giorno 09:00` → modifica la cron expression |
| Soglia recensioni negative | Nodo `Genera Email HTML` → `votoNum <= 3` |

---

## Note sulla Google Business Profile API

L'API richiede che il tuo account Google abbia accesso verificato alla location su Google My Business. Se la tua location non è ancora verificata su Google, completa prima il processo di verifica su [business.google.com](https://business.google.com).

L'accesso all'API potrebbe richiedere approvazione da parte di Google se l'utilizzo supera determinati limiti. Per uso interno a una singola PMI, generalmente non ci sono problemi.
