# Area Cliente

## Moduli

| Modulo | Ruolo |
|---|---|
| Dashboard | Scorciatoie intelligenti — cambia in base al tipo di servizio |
| Servizi | Lista e calendario dei servizi attivi |
| Nuovi | Richiesta nuovo servizio e stato delle richieste |
| Profilo | Dati personali, contratto, finanze |
| Supporto | Contatto rapido via WhatsApp e altri canali |

---

## Flusso

```mermaid
flowchart TD
    DASH[🏠 Dashboard]

    DASH --> |Servizio continuativo| C1[Prossimo servizio\nRichiedi servizio extra]
    DASH --> |Servizio booking| C2[Ripeti servizio\nPrenota di nuovo\nLe mie richieste]

    C1 --> SERV[📋 Servizi\nServizi attivi e calendario]
    C2 --> NUOVI[➕ Nuovi\nNuova richiesta]

    SERV --> |Segnalazione| SEG[Segnala assenza\nRichiedi modifica]
    SEG --> |Inviata a| EV[⚡ Admin — Eventi Operativi]

    NUOVI --> |Richiesta inviata| IR[📥 Admin — Inbound Requests]
    IR --> |Stato aggiornato| STATO[In attesa → In valutazione → Accettata]
    STATO --> |Confermata| SERV

    DASH --> SUPP[💬 Supporto\nWhatsApp sempre visibile]
```
