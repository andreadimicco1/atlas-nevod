# Area Admin

## Moduli

| Modulo | Ruolo |
|---|---|
| Dashboard | KPI, alert e trend — lettura rapida dei dati |
| Acquisition | Tutto cio' che entra dall'esterno |
| Clienti | Registro operativo clienti |
| Personale | Registro operativo personale |
| Operativita' | Motore interno — coordina i servizi attivi |
| Finanza | Costi, entrate e buste paga |
| Network | Lista partner e relazioni |

---

## Flusso 1 — Acquisition

```mermaid
flowchart TD
    IR[Inbound Requests\nTutte le richieste esterne]

    IR --> |Candidatura personale approvata| PERS[Aggiunto al personale]
    IR --> |Richiesta cliente| LT[Lead Triage\nValutazione tipo servizio]
    IR --> |Non rilevante| DEL[Eliminata]

    LT --> |Booking — servizio semplice| PA[Pre-assegnazione\nVisibile al personale]
    LT --> |Continuativo — servizio complesso| MAN[Gestione manuale Admin]

    PA --> |Personale si candida\nAdmin approva| CONV[Conversione storica]
    MAN --> |Concluso| CONV

    CONV --> SA[Servizio Attivo]
```

---

## Flusso 2 — Operativita'

```mermaid
flowchart TD
    SA[Servizi Attivi\nFonte ufficiale del sistema]

    SA <--> CAL[Calendario\nVista temporale]
    SA --> CTRL[Controllo\nAlert e anomalie]

    CTRL --> |Servizi scoperti\nConflitti\nScadenze| A[Admin interviene]

    EV[Eventi Operativi\nTutto cio' che cambia]

    PERS[Personale] --> |Segnala assenza\nRichiede modifica\nSegnala problema| EV
    CLI[Cliente] --> |Segnala assenza\nRichiede modifica| EV

    EV --> |Admin approva| SA
    EV --> |Assenza personale| OPP[Nuova opportunita'\nper altro personale]
```
