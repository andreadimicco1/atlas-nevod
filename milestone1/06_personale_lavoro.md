# Personale — Il Mio Lavoro

## Moduli

| Modulo | Ruolo |
|---|---|
| Calendario | Vista giorno / settimana / mese dei servizi assegnati |
| Servizi Attivi | Lista completa dei servizi in corso |
| Segnalazioni | Comunicazioni verso Admin |

---

## Flusso

```mermaid
flowchart TD
    CAL[📅 Calendario\nVista giorno, settimana, mese]
    SA[📋 Servizi Attivi\nLista servizi in corso]

    CAL --> |Clicca evento| DET[Dettaglio servizio\nNome assistito, indirizzo, orari]
    DET --> SA

    SA --> |Bottone storico| CANC[📁 Servizi passati e cancellati]

    SEG[🔔 Segnalazioni]

    SEG --> |Segnala assenza| CTRL[Admin — Controllo\nAlert servizio scoperto]
    SEG --> |Richiedi modifica turno| EV[Admin — Eventi Operativi]
    SEG --> |Segnala problema cliente| EV

    CTRL --> |Se necessario| OPP[Nuova opportunità\nper altro personale]
```
