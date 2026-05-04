# Landing Page

## Moduli

| Sezione | Spazio | Descrizione |
|---|---|---|
| Login | In alto | Accesso per utenti registrati |
| Clienti | 60% | Richiesta nuovo servizio in 2 step |
| Personale | 30% | Candidatura spontanea |
| Richiesta veloce | 10% | Contatto rapido senza login (es. partner) |

> La landing e' uguale per tutti — distinzione admin / personale / cliente solo dopo login.

---

## Flusso

```mermaid
flowchart TD
    LP[Landing Page]

    LP --> LOGIN[Bottone LOGIN]
    LP --> RC[Sezione Clienti\nRichiesta servizio]
    LP --> RP[Sezione Personale\nCandidatura]
    LP --> RV[Richiesta veloce\nsenza login]

    LOGIN --> AUTH{Autenticazione}
    AUTH --> |Admin| ADMIN[Area Admin]
    AUTH --> |Personale| PERS[Area Personale]
    AUTH --> |Cliente| CLI[Area Cliente]

    RC --> |Compila form in 2 step| FC[Form Cliente\nvedi dettaglio in 05_form_cliente]
    FC --> |Invia| IR[Admin — Inbound Requests]

    RP --> |Compila form| FP[Form Personale\nvedi dettaglio in 06_form_personale]
    FP --> |Invia| IR

    RV --> |Nome + telefono + nota| IR
```
