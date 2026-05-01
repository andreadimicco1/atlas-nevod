# Admin — Acquisition

## Moduli

| Modulo | Ruolo |
|---|---|
| Inbound Requests | Raccoglie tutto ciò che arriva dall'esterno |
| Lead Triage | Valuta e smista le richieste clienti |
| Pre-assegnazione | Gestisce i booking — visibile anche al personale |
| Conversione | Archivio storico delle richieste diventate servizi |

---

## Flusso

```mermaid
flowchart TD
    IR[📥 Inbound Requests\nTutte le richieste esterne]

    IR --> |Candidatura personale approvata| PERS[✅ Aggiunto al personale]
    IR --> |Richiesta cliente| LT[🔍 Lead Triage\nValutazione tipo servizio]
    IR --> |Non rilevante| DEL[🗑️ Eliminata]

    LT --> |Booking\nServizio semplice| PA[📋 Pre-assegnazione\nVisibile al personale]
    LT --> |Continuativo\nServizio complesso| MAN[⚙️ Gestione manuale Admin]

    PA --> |Personale si candida\nAdmin approva| CONV[📦 Conversione storica]
    MAN --> |Concluso| CONV

    CONV --> SA[🟢 Servizio Attivo]
```
