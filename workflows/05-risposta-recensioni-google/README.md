# 05 — Risposta Recensioni Google

> Nuova recensione Google My Business → Claude genera bozza risposta → notifica owner per approvazione

⏳ **Pianificato** — sviluppo previsto mar 19/05/2026.

## Il problema

Rispondere a ogni recensione Google è importante per SEO locale e percezione brand, ma richiede tempo e attenzione (specialmente per recensioni negative dove la prima risposta conta tantissimo).

## Come funziona

```
Trigger: nuova recensione GMB (polling)
   ↓
Claude genera bozza risposta:
   ├─ Positive → ringraziamento personalizzato
   └─ Negative → empatia + offerta di risoluzione offline
   ↓
Notifica Slack/email all'owner con bozza + link approvazione
   ↓
(L'owner approva manualmente con un click — il workflow NON pubblica automaticamente le risposte alle negative)
```

> ⚠️ **Design choice**: il workflow non pubblica automaticamente, richiede approvazione umana. Sulle recensioni un errore di tono fa più danno del tempo risparmiato.

_Documentazione completa al rilascio._
