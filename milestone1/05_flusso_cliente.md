# ATLAS — Flusso Area Cliente (Mobile-first)

## Dashboard Cliente — Variante per tipo di servizio

```mermaid
flowchart TD
    LOGIN[Cliente fa login] --> TIPO{Tipo di servizio?}

    TIPO --> |Continuativo| DASH_C["🏠 DASHBOARD CONTINUATIVO
    ✅ Prossimo servizio
    ➕ Richiedi servizio extra
    🔔 Segnala assenza"]

    TIPO --> |Booking| DASH_B["🏠 DASHBOARD BOOKING
    🔁 Ripeti questo servizio
    📅 Prenota di nuovo
    📋 Le mie richieste"]

    TIPO --> |Misto| DASH_M["🏠 DASHBOARD MISTO
    Combinazione dei due
    Da definire senza affollamento"]

    DASH_C --> |Prossimo servizio| SERV[Modulo Servizi]
    DASH_C --> |Richiedi extra| NUOVI[Modulo Nuovi]
    DASH_C --> |Segnala assenza| SEG[Modulo Servizi → Segnalazioni]

    DASH_B --> |Ripeti / Prenota| STOR[Storico richieste]
    DASH_B --> |Le mie richieste| STATO[Stato nuove richieste]
```

---

## Flusso Nuova Richiesta Cliente

```mermaid
sequenceDiagram
    participant C as Cliente
    participant LP as Landing / Modulo Nuovi
    participant IR as Admin: Inbound Requests
    participant LT as Admin: Lead Triage
    participant A as Admin

    C->>LP: Compila modulo richiesta (2 step)
    Note over LP: Step 1: dati personali / contatti<br/>Step 2: tipo servizio + categorie
    LP->>IR: Richiesta inviata
    IR->>A: Notifica nuova richiesta
    A->>LT: Trasferisce in Lead Triage
    A->>LT: Classifica: Booking o Continuativo?

    alt Booking
        LT->>LT: Passa in Pre-assegnazione
        LT->>C: Aggiorna stato → "In valutazione"
    else Continuativo
        LT->>A: Gestione manuale
        LT->>C: Aggiorna stato → "In valutazione"
    end

    A->>C: Stato finale → "Accettata"
    C->>C: Servizio appare in Dashboard e Servizi
```

---

## Modulo Servizi Cliente

```mermaid
flowchart TD
    SERV["📋 SERVIZI ATTIVI
    Lista servizi in corso"]

    CAL["📅 CALENDARIO
    Vista temporale dei servizi"]

    SEG["🔔 SEGNALAZIONI"]

    SERV --> |Clic servizio| DET[Dettaglio servizio]
    CAL --> |Clic evento| DET
    SEG --> SEG1["Segnala assenza
    → Admin: Controllo"]
```

---

## Modulo Nuovi — Stati richiesta visibili al cliente

```mermaid
stateDiagram-v2
    [*] --> InAttesa : Richiesta inviata
    InAttesa --> InValutazione : Admin trasferisce in Lead Triage
    InValutazione --> Accettata : Admin approva e assegna
    Accettata --> [*] : Appare in Servizi Attivi

    note right of InAttesa
        Cliente vede: "In attesa"
    end note
    note right of InValutazione
        Cliente vede: "In valutazione"
    end note
    note right of Accettata
        Cliente vede: "Accettata"
    end note
```

---

## Modulo Supporto

```mermaid
flowchart LR
    SUPP["📞 SUPPORTO"] --> WA["💬 WhatsApp API
    Contatto diretto e rapido"]
    SUPP --> ALTRI["📧 Altri contatti
    Email / Telefono"]
    WA --> |Visibile sempre anche in Dashboard| DASH
```
