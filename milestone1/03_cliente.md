# Area Cliente

## Moduli

| Modulo | Ruolo |
|---|---|
| Dashboard | Scorciatoie intelligenti — varia in base al tipo di servizio |
| Servizi | Lista e calendario dei servizi attivi |
| Nuovi | Richiesta nuovo servizio e stato delle richieste |
| Profilo | Dati personali, contratto e finanze |
| Supporto | Contatto rapido via WhatsApp e altri canali |

---

## Flusso 1 — Appuntamenti e Modifiche

```mermaid
flowchart TD
    DASH[Dashboard]

    DASH --> CAL[Calendario\nVista servizi attivi]
    DASH --> SA[Servizi\nLista servizi attivi]

    CAL --> |Clicca appuntamento| DET[Dettaglio appuntamento\nData, orario, operatore, indirizzo]
    SA --> |Clicca servizio| DET

    DET --> |Richiedi modifica orario| EV[Admin — Eventi Operativi\nAdmin approva o rifiuta]
    DET --> |Segnala assenza| ANN[Appuntamento annullato\nNotifica al personale assegnato]

    EV --> |Esito| NOT[Notifica al cliente]
```

---

## Flusso 2 — Nuova Richiesta

```mermaid
flowchart TD
    DASH[Dashboard]

    DASH --> |Richiedi servizio extra\nPrenota di nuovo| NUOVI[Nuovi\nModulo richiesta]

    NUOVI --> |Step 1| S1[Dati personali e contatti]
    S1 --> |Step 2| S2[Tipo servizio e dettagli]
    S2 --> |Invia| IR[Admin — Inbound Requests]

    IR --> STATO{Stato richiesta\nvisibile al cliente}
    STATO --> |In attesa| W[In attesa]
    STATO --> |In valutazione| V[In valutazione]
    STATO --> |Accettata| A[Accettata]

    A --> SA[Appare in Servizi attivi]
```
