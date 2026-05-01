# Admin — Operatività

## Moduli

| Modulo | Ruolo |
|---|---|
| Servizi Attivi | Fonte ufficiale — la verità del sistema in ogni momento |
| Calendario | Visualizzazione temporale dei servizi attivi |
| Eventi Operativi | Gestione di tutto ciò che cambia o viene segnalato |
| Controllo | Alert e anomalie operative |

---

## Flusso

```mermaid
flowchart TD
    SA[🟢 Servizi Attivi\nFonte ufficiale del sistema]

    SA <--> CAL[📅 Calendario\nVista temporale]
    SA --> CTRL[🔔 Controllo\nAlert e anomalie]

    CTRL --> |Servizi scoperti\nConflitti\nScadenze| A[Admin interviene]

    EV[⚡ Eventi Operativi\nTutto ciò che cambia]

    PERS[👤 Personale] --> |Segnala assenza\nRichiede modifica\nSegnala problema| EV
    CLI[👥 Cliente] --> |Segnala assenza\nRichiede modifica| EV

    EV --> |Admin approva| SA
    EV --> |Assenza personale| OPP[📋 Nuova opportunità\nper altro personale]
```
