# Area Personale

## Moduli

| Modulo | Ruolo |
|---|---|
| Dashboard | Scorciatoie: prossimo servizio, richieste in attesa, segnala assenza |
| Opportunita' | Nuove richieste disponibili e gestione candidature |
| Il mio lavoro | Calendario, servizi assegnati e segnalazioni |
| Profilo | Dati personali, finanze e documenti |

---

## Flusso 1 — Nuove Richieste e Opportunita'

```mermaid
flowchart TD
    NR[Nuove Richieste\nOpportunita' disponibili]

    NR --> |Si candida| RIV[Richieste in Valutazione\nIn attesa risposta Admin]
    RIV --> |Annulla candidatura| NR

    RIV --> |Admin rifiuta| STOR_R[Storico Rifiutate\nNon torna in Nuove Richieste]
    RIV --> |Admin accetta| RICONF[Riconferma obbligatoria\nIl personale deve confermare]

    RICONF --> |Confermato| MLV[Il Mio Lavoro\nServizio assegnato]
    RICONF --> |Non confermato| STOR_A[Storico Accettate]
```

---

## Flusso 2 — Il Mio Lavoro

```mermaid
flowchart TD
    CAL[Calendario\nVista giorno, settimana, mese]
    SA[Servizi Attivi\nLista servizi in corso]

    CAL --> |Clicca evento| DET[Dettaglio servizio\nNome assistito, indirizzo, orari]
    DET --> SA
    SA --> |Bottone storico| CANC[Servizi passati e cancellati]

    SEG[Segnalazioni]

    SEG --> |Segnala assenza| CTRL[Admin — Controllo\nAlert servizio scoperto]
    SEG --> |Richiedi modifica turno| EV[Admin — Eventi Operativi]
    SEG --> |Segnala problema cliente| EV

    CTRL --> |Se necessario| OPP[Nuova opportunita'\nper altro personale]
```
