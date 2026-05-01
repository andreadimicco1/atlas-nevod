# Landing Page

## Moduli

| Sezione | Spazio | Descrizione |
|---|---|---|
| Login | In alto | Accesso per utenti registrati |
| Clienti | 60% | Richiesta nuovo servizio (2 step) |
| Personale | 30% | Candidatura spontanea |
| Richiesta veloce | 10% | Contatto rapido senza login (es. partner) |

> La landing è uguale per tutti — il sistema non sa chi sei finché non fai login.

---

## Flusso

```mermaid
flowchart TD
    LP[🌐 Landing Page]

    LP --> LOGIN[Bottone LOGIN]
    LP --> RC[Sezione Clienti\n Richiesta servizio]
    LP --> RP[Sezione Personale\n Candidatura]
    LP --> RV[Richiesta veloce\n senza login]

    LOGIN --> AUTH{Autenticazione}
    AUTH --> |Admin| ADMIN[Area Admin]
    AUTH --> |Personale| PERS[Area Personale]
    AUTH --> |Cliente| CLI[Area Cliente]

    RC --> |Invia richiesta| IR[📥 Inbound Requests]
    RP --> |Invia candidatura| IR
    RV --> |Invia contatto| IR
```
