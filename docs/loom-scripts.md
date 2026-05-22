# 🎬 Loom Scripts — n8n Automation Pack Italia

> Script di riferimento per i 5 video Loom (60-90s ciascuno) che accompagnano i workflow del pack.

## Struttura standard

Ogni script segue la stessa cadenza in 4 blocchi:

| Blocco | Durata | Scopo |
|---|---|---|
| **HOOK** | 5-8s | Domanda o promessa che ferma lo scroll |
| **PROBLEMA** | 10-15s | Chi soffre quel problema e perché brucia |
| **DEMO** | 40-50s | Cosa fa il workflow mentre si vede a schermo |
| **CTA** | 8-10s | Repo, link in commento, invito a sperimentare |

**Tono**: pragmatico B2B, no buzzword. Narratore "tu" — parla al titolare/operations di una PMI.

**Cadenza target**: ~150 parole/minuto a velocità conversazionale italiana → ~180 parole totali per script.

---

## Script 1 — Lead Qualification

**Durata stimata**: 80-85s
**Schermo principale**: Gmail inbox piena di "Nuovo contatto" → form di test → n8n workflow live → Google Sheet che si popola → inbox del lead con l'email personalizzata

> **[HOOK — 0:00-0:07]**
> *"Hai ricevuto trenta lead dal sito questa settimana. Quanti sono davvero pronti a comprare? Senza un sistema, te li leggi tutti uno per uno."*
>
> **[PROBLEMA — 0:07-0:20]**
> *"Per la maggior parte delle PMI italiane il contact form è una black box: arriva un'email, qualcuno la legge 'quando può', il lead caldo aspetta, l'occasione passa. E intanto rispondi anche ai curiosi con la stessa fatica del cliente reale."*
>
> **[DEMO — 0:20-1:10]**
> *"Workflow Lead Qualification in n8n. Il form invia il submit al webhook. Claude legge nome, azienda, messaggio, budget, telefono — e in un colpo solo ti restituisce: classificazione hot, warm o cold; uno score da zero a cento; il perché di quella valutazione; e una priorità di risposta. Il foglio Google si compila da solo. Se è hot o warm, parte un'email personalizzata col nome del lead — guarda — entro trenta secondi. Se è cold, riceve un cortese 'ti risponderemo' e finisce in fondo alla lista. Tutto loggato, niente perso. Tu il lunedì mattina apri Sheets, ordini per score, e attacchi solo quelli che valgono."*
>
> **[CTA — 1:10-1:20]**
> *"Workflow numero uno del pack 'n8n Automation Italia'. Cinque flussi pronti per la tua PMI, gratis e open source. Repo pubblico venerdì, link nel commento qui sotto."*

---

## Script 2 — Newsletter Aggregator

**Durata stimata**: 78-82s
**Schermo principale**: tre feed RSS aperti in tab → n8n workflow → inbox con email HTML responsive ricevuta

> **[HOOK — 0:00-0:08]**
> *"Newsletter settimanale di settore. Quante ore ti porta via, fra lettura, scelta dei pezzi, scrittura e impaginazione? E se il lunedì mattina arrivasse già pronta nella tua inbox?"*
>
> **[PROBLEMA — 0:08-0:20]**
> *"Per chi cura una newsletter — agenzia, consulente, brand — la routine è sempre la stessa: aprire dieci feed, leggere, selezionare, sintetizzare, formattare. Tre ore a settimana che si possono quasi azzerare."*
>
> **[DEMO — 0:20-1:10]**
> *"Workflow Newsletter Aggregator in n8n. Ogni lunedì alle nove, il trigger pesca articoli da tre feed RSS in parallelo — qui ho messo Ninja Marketing, HubSpot e VentureBeat AI, ma cambiarli si fa in trenta secondi. Filtra gli ultimi sette giorni, manda venti articoli a Claude, che seleziona i top cinque, riscrive i titoli in italiano e riassume ogni pezzo in tre o quattro frasi. Il workflow costruisce l'HTML responsive — guarda — e arriva nella tua inbox così. Costo: meno di trenta centesimi al mese, tutto compreso."*
>
> **[CTA — 1:10-1:20]**
> *"Workflow numero due del pack n8n Automation Italia. Cinque flussi pronti per la tua PMI, gratis e open source. Repo pubblico venerdì, link nel commento qui sotto."*

---

## Script 3 — Slack Daily Digest

**Durata stimata**: 78-82s
**Schermo principale**: 5 fonti aperte in tab → n8n workflow → messaggio Slack che compare in `#general`

> **[HOOK — 0:00-0:08]**
> *"Cinque fonti da controllare ogni mattina — marketing, AI, release dei tool che usi. Quante volte lo fai davvero? E se arrivasse tutto in un messaggio Slack alle nove?"*
>
> **[PROBLEMA — 0:08-0:20]**
> *"Nei team piccoli, restare aggiornati è una guerra persa: gli RSS si accumulano, le release passano sotto traccia, nessuno ha tempo di sintetizzare. Risultato: si parla delle novità in ritardo, oppure non se ne parla."*
>
> **[DEMO — 0:20-1:10]**
> *"Daily Digest in n8n. Dal lunedì al venerdì, alle nove in punto, il flusso pesca da cinque fonti — tre RSS marketing e AI, più le release di n8n e LangChain prese direttamente da GitHub. Claude legge le ultime ventiquattro ore, sceglie i top cinque, scrive due o tre righe di riassunto per ciascuno in italiano. Il workflow formatta il messaggio Slack con emoji, titoli grassetto, link cliccabili — guarda come compare in canale. Il team apre, scorre trenta secondi, è aggiornato. Costo: ottanta centesimi al mese."*
>
> **[CTA — 1:10-1:20]**
> *"Workflow numero tre del pack. Repo aperto venerdì, link nel commento."*

---

## Script 4 — Onboarding Clienti

**Durata stimata**: 82-88s
**Schermo principale**: form Tally → n8n workflow con 3 branch paralleli → email arrivata + cartella Drive creata + progetto Taskade aperto con 7 task

> **[HOOK — 0:00-0:08]**
> *"Nuovo cliente firma. Email di benvenuto, cartella Drive con i template, task aperti nel project manager. Quindici minuti di click ripetitivi. Ogni. Singola. Volta."*
>
> **[PROBLEMA — 0:08-0:22]**
> *"Per consulenti, agenzie, studi professionali, l'onboarding è la stessa sequenza ripetuta cento volte: si dimentica un passaggio, l'email parte tardi, la cartella non c'è. E il cliente si fa l'idea sbagliata già dal giorno zero."*
>
> **[DEMO — 0:22-1:15]**
> *"Workflow Onboarding Clienti in n8n. Il cliente firma il contratto, parte un webhook — può essere Tally, Typeform, qualsiasi form. Claude genera un'email di benvenuto personalizzata col nome dell'azienda e il servizio acquistato. Poi tre branch in parallelo: l'email parte via SMTP, la cartella Drive 'Azienda — Onboarding 2026' viene creata, e in Taskade, via MCP, si apre un progetto con sette task standard già pronti: questionario iniziale, kickoff, accessi, prima deliverable, check-in settimana uno, settimana due, chiusura. Dieci secondi e l'onboarding è partito. Tu rimani libero per parlare col cliente."*
>
> **[CTA — 1:15-1:25]**
> *"Workflow numero quattro del pack n8n Automation Italia. Repo aperto venerdì, link nel commento."*

---

## Script 5 — Risposta Recensioni Google

**Durata stimata**: 80-86s
**Schermo principale**: scheda Google Business Profile con recensioni in attesa → n8n workflow → email con bozze pronte al copia-incolla

> **[HOOK — 0:00-0:08]**
> *"Hai cinque recensioni Google da rispondere. Le positive le rimandi sempre, le negative ti rovinano il pomeriggio. E intanto passano i giorni."*
>
> **[PROBLEMA — 0:08-0:22]**
> *"Per ristoranti, studi, negozi, b&b, le risposte alle recensioni contano molto — sia per chi le legge, sia per l'algoritmo Google. Ma scriverle costa tempo, soprattutto sulle negative dove serve attenzione. E il backlog si accumula."*
>
> **[DEMO — 0:22-1:15]**
> *"Workflow Risposta Recensioni in n8n. Ogni mattina alle nove, polling sull'API Google Business Profile. Il flusso pesca le recensioni senza risposta, massimo cinque per giro. Per ognuna, Claude genera una bozza: se è quattro o cinque stelle, un ringraziamento personalizzato che cita un dettaglio del commento; se è una, due o tre stelle, una risposta empatica che invita a risolvere offline, senza difensiva. Le bozze arrivano in un'unica email — guarda — pronte per il copia-incolla. Il workflow non pubblica da solo: la revisione umana sulle negative è non negoziabile."*
>
> **[CTA — 1:15-1:25]**
> *"Workflow numero cinque del pack. Repo aperto venerdì, link nel commento."*

---

## Riepilogo set

| # | Workflow | Durata | Schermo principale |
|---|---|---|---|
| 1 | Lead Qualification | 80-85s | Webhook → Sheet che si popola → inbox |
| 2 | Newsletter Aggregator | 78-82s | Feed RSS → workflow → email HTML |
| 3 | Slack Daily Digest | 78-82s | 5 fonti → workflow → Slack #general |
| 4 | Onboarding Clienti | 82-88s | Form → 3 branch → email + Drive + Taskade |
| 5 | Risposta Recensioni Google | 80-86s | GMB → workflow → email con bozze |

**Totale parlato**: ~7 minuti di registrazioni nette.

## Calendario registrazione

| Data | Loom da girare |
|---|---|
| Sab 23/05 | W#1 + W#2 |
| Dom 24/05 | W#3 + W#4 |
| Lun 25/05 | W#5 + retake eventuali |

## Note per la registrazione

- **Prima di rec**: pulire dati di test inutili (es. riga 2 spazzatura nel Sheet Leads CRM v2 dell'execute accidentale).
- **Risoluzione consigliata**: 1080p, full screen Loom o area schermo dedicata.
- **Audio**: micro USB possibilmente, no microfono di laptop.
- **Comportamento Claude**: nel parlato dire "Claude" e basta, non specificare versione (i README hanno ancora "Sonnet 4.5" da aggiornare a 4.6 nella revisione di mer 27/05).
- **CTA finale**: ricordare di linkare il repo (a quel punto pubblico) nel primo commento del post LinkedIn di venerdì.
