# ATLAS — Flusso Operatività (Admin)

## Il motore interno: gestione di tutto ciò che è già nel sistema

```mermaid
flowchart TD
    SA["🟢 SERVIZI ATTIVI
    Fonte ufficiale e assoluta
    Lista di tutti i servizi in essere
    Filtri intelligenti
    Ogni modifica deve essere approvata"]

    CAL["📅 CALENDARIO
    Visualizzazione temporale
    Scorrimento sinistra/destra
    Rappresentazione visiva dei servizi"]

    EV["⚡ EVENTI OPERATIVI
    Lista di tutto ciò che cambia o segnala
    
    Origini:
    - Segnalazioni personale
    - Segnalazioni cliente
    - Richieste di modifica turno
    - Nuovi eventi creati da Admin"]

    CTRL["🔔 CONTROLLO
    Alert e anomalie
    
    Tipi di alert:
    - Servizi scoperti (senza operatore)
    - Booking non assegnati
    - Conflitti calendario
    - Scadenze contratti"]

    SA <--> CAL
    EV --> |Approvato → aggiorna| SA
    CTRL --> |Alert su| SA
    CTRL --> |Alert su| CAL

    PERS_SEG["👤 Segnalazione Personale
    (da area Personale)"] --> EV
    CLI_SEG["👥 Segnalazione Cliente
    (da area Cliente)"] --> EV
    ASSENZA["🚫 Segnalazione Assenza
    (da area Personale)"] --> CTRL
```

---

## Stati degli Eventi Operativi

```mermaid
stateDiagram-v2
    [*] --> Nuovo : Creato da Admin o ricevuto da Personale/Cliente
    Nuovo --> InElaborazione : Admin lo prende in carico
    InElaborazione --> InAttesaRisposta : Richiede risposta esterna
    InAttesaRisposta --> ProntoDaApprovare : Risposta ricevuta
    InElaborazione --> ProntoDaApprovare : Risolto internamente
    ProntoDaApprovare --> Chiuso : Approvato → aggiorna Servizi Attivi
    Chiuso --> [*] : Archiviato
```

---

## Flusso segnalazione Personale → Admin

```mermaid
sequenceDiagram
    participant P as Personale
    participant SYS as Sistema
    participant A as Admin

    P->>SYS: Segnala assenza (giorni + nota opzionale)
    SYS->>A: Alert in CONTROLLO
    A->>SYS: Vede servizio scoperto
    SYS->>SYS: Genera opportunità per altro personale
    SYS->>P: Notifica ad altri collaboratori (Pre-assegnazione)

    P->>SYS: Richiede modifica turno (servizio + nota)
    SYS->>A: Evento in EVENTI OPERATIVI
    A->>SYS: Accetta o rifiuta modifica
    SYS->>P: Notifica esito

    P->>SYS: Segnala problema cliente (servizio + commento)
    SYS->>A: Evento in EVENTI OPERATIVI
    A->>SYS: Decide come gestire
```

---

## Regola fondamentale — Servizi Attivi come fonte ufficiale

```
SERVIZI ATTIVI = Verità assoluta del sistema in quel momento

Nessuna modifica diretta ai Servizi Attivi senza passare per:
  └── EVENTI OPERATIVI → approvazione Admin → aggiornamento SA
```
