# ATLAS — Flusso Acquisition (Admin)

## Percorso completo: dalla richiesta esterna al servizio attivo

```mermaid
flowchart TD
    LP[🌐 Landing Page] --> |Richiesta cliente| IR
    LP --> |Candidatura personale| IR
    LP --> |Richiesta veloce no-login| IR

    IR["📥 INBOUND REQUESTS (IR)
    Lista di tutte le richieste esterne
    Separazione visiva: Cliente vs Personale"]

    IR --> |Candidatura personale approvata| CONV_P[✅ Convertito in Personale
    Aggiunto al pool personale]

    IR --> |Richiesta cliente trasferita| LT

    IR --> |Elimina| DEL1[🗑️ Eliminata]

    LT["🔍 LEAD TRIAGE
    Smistamento richieste clienti
    Valutazione tipo di servizio"]

    LT --> |Servizio SEMPLICE - Booking| PA
    LT --> |Servizio COMPLESSO - Continuativo| LT_MAN[⚙️ Gestione manuale
    Rimane in Lead Triage
    Operazione diretta Admin]

    PA["📋 PRE-ASSEGNAZIONE
    Lista booking disponibili
    Visibile al personale per candidatura
    
    Stati:
    🆕 Nuova
    ✅ Accettata
    ❌ Rifiutata"]

    PA --> |Personale si candida| PA_WAIT[⏳ In attesa approvazione Admin]
    PA_WAIT --> |Admin approva| CONV
    PA_WAIT --> |Admin rifiuta| PA

    CONV["📦 CONVERSIONE storica
    Archivio richieste diventate servizi
    Solo quelle convertite
    Escluse: eliminate e non rilevanti"]

    CONV --> |Genera| SA[🟢 SERVIZIO ATTIVO
    Entra in Operatività]

    LT_MAN --> |Se si conclude| CONV
```

---

## Dettaglio stati richiesta in Pre-assegnazione

```mermaid
stateDiagram-v2
    [*] --> Nuova : Trasferita da Lead Triage
    Nuova --> InValutazione : Personale si candida
    InValutazione --> Accettata : Admin approva
    InValutazione --> Rifiutata : Admin rifiuta
    Accettata --> Confermata : Personale riconferma
    Confermata --> [*] : Passa in Conversione → Servizio Attivo
    Rifiutata --> Nuova : Torna disponibile
```

---

## Chi vede cosa in Acquisition

| Sotto-modulo | Visibile a | Azioni disponibili |
|---|---|---|
| Inbound Requests | Solo Admin | Apri dettaglio, aggiungi nota, converti in personale, trasferisci in Lead Triage, elimina |
| Lead Triage | Solo Admin | Classifica servizio, filtra, apri dettaglio |
| Pre-assegnazione | Admin + Personale (lista booking) | Admin: approva/rifiuta — Personale: si candida |
| Conversione | Solo Admin | Consulta storico |
