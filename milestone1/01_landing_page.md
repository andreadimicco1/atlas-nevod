# Landing Page

## Moduli

| Sezione | Spazio | Descrizione |
|---|---|---|
| Login | In alto | Accesso per utenti registrati |
| Clienti | 60% | Richiesta nuovo servizio in 2 step |
| Personale | 30% | Candidatura spontanea |
| Richiesta veloce | 10% | Contatto rapido senza login (es. partner) |

> La landing e' uguale per tutti — la distinzione admin / personale / cliente avviene solo dopo il login.

---

## Flusso 1 — Panoramica Landing Page

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

    RC --> FC[Form Cliente\n2 step]
    FC --> |Invia| IR[Admin — Inbound Requests]

    RP --> FP[Form Personale\nda definire]
    FP --> |Invia| IR

    RV --> |Nome, telefono, nota| IR
```

---

## Flusso 2 — Form Cliente

Il form e' diviso in 2 step. I campi del secondo step variano in base al tipo di servizio scelto nel primo.

```mermaid
flowchart TD
    FORM[FORM\nNome e cognome\nEmail — Telefono\n]

    FORM --> TIPO{Tipo di servizio}

    TIPO --> |Ass. a ore\nBadante notturna\nEconomia domestica| BK[Fascia oraria\nDurata se richiesta\nSelezione data]
    TIPO --> |Badante 24h\nAltro| ALT[Note aggiuntive\nIndirizzo]

    BK --> FINE[Note opzionali\nIndirizzo]
    FINE --> LT[Lead Triage]

    ALT --> GM[Gestione manuale Admin\nContinuativo valutato da Admin]
```

---

## Flusso 3 — Selezione fascia oraria

Dove richiesto dal tipo di servizio, il campo orario non e' un testo libero ma una selezione a livelli.

```mermaid
flowchart TD
    ORA{Fascia oraria}

    ORA --> M[Mattina]
    ORA --> P[Pomeriggio]
    ORA --> SN[Sera / Notte]
    ORA --> |Personalizzato| CUSTOM[Campo testo libero\nes. 14:30 oppure dalle 9 alle 11]
```
