# Personale — Nuove Richieste e Opportunità

## Moduli

| Modulo | Ruolo |
|---|---|
| Nuove richieste | Lista opportunità disponibili a cui candidarsi |
| Richieste in valutazione | Candidature inviate — monitoraggio stato |
| Storico | Archivio candidature accettate e rifiutate |

---

## Flusso

```mermaid
flowchart TD
    NR[📋 Nuove Richieste\nOpportunità disponibili]

    NR --> |Si candida| RIV[⏳ Richieste in Valutazione\nIn attesa di risposta Admin]
    RIV --> |Annulla candidatura| NR

    RIV --> |Admin rifiuta| STOR[📁 Storico Rifiutate\nNon torna in Nuove Richieste]
    RIV --> |Admin accetta| RICONF[✅ Riconferma obbligatoria\nIl personale deve confermare]

    RICONF --> |Confermato| MLV[💼 Il Mio Lavoro\nServizio assegnato]
    RICONF --> |Non confermato| STOR2[📁 Storico Accettate]
```
