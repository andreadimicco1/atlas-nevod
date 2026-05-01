# ATLAS — Schema Database (MVP)

## Tabelle principali e relazioni

```mermaid
erDiagram
    USERS {
        int id PK
        string email
        string password_hash
        string role "admin | personale | cliente"
        string nome
        string cognome
        string telefono
        bool attivo
        datetime created_at
    }

    CLIENTI {
        int id PK
        int user_id FK
        string indirizzo
        string tipo_servizio "continuativo | booking | misto"
        string note
        string stato_contratto
    }

    PERSONALE {
        int id PK
        int user_id FK
        string indirizzo
        bool attivo
        string note
        string stato_contratto
    }

    RICHIESTE_INGRESSO {
        int id PK
        string tipo "cliente | personale | veloce"
        string stato "ir | lead_triage | pre_assegnazione | conversione | eliminata"
        string nome
        string cognome
        string email
        string telefono
        string note
        datetime created_at
    }

    SERVIZI_ATTIVI {
        int id PK
        int cliente_id FK
        int personale_id FK
        string tipo "continuativo | booking"
        string stato "attivo | cancellato | sospeso"
        datetime data_inizio
        datetime data_fine
        string descrizione
        string indirizzo
        string fascia_oraria
        datetime created_at
    }

    EVENTI_OPERATIVI {
        int id PK
        int servizio_id FK
        int creato_da FK
        string tipo "segnalazione | modifica_turno | problema_cliente | assenza | nuovo"
        string stato "nuovo | in_elaborazione | in_attesa_risposta | pronto_da_approvare | chiuso"
        string descrizione
        string nota
        datetime created_at
    }

    OPPORTUNITA {
        int id PK
        int servizio_id FK
        string tipo "nuovo_servizio | copertura"
        string stato "aperta | chiusa"
        datetime created_at
    }

    CANDIDATURE {
        int id PK
        int opportunita_id FK
        int personale_id FK
        string stato "in_valutazione | accettata | rifiutata | annullata | confermata"
        datetime created_at
    }

    PARTNER {
        int id PK
        string nome
        string tipo
        string stato_relazione
        int clienti_portati
        string note
        string contatti
    }

    USERS ||--o| CLIENTI : "ha profilo"
    USERS ||--o| PERSONALE : "ha profilo"
    CLIENTI ||--o{ SERVIZI_ATTIVI : "riceve"
    PERSONALE ||--o{ SERVIZI_ATTIVI : "eroga"
    SERVIZI_ATTIVI ||--o{ EVENTI_OPERATIVI : "genera"
    SERVIZI_ATTIVI ||--o{ OPPORTUNITA : "apre"
    OPPORTUNITA ||--o{ CANDIDATURE : "riceve"
    PERSONALE ||--o{ CANDIDATURE : "invia"
```

---

## Note sullo schema

| Tabella | Note |
|---|---|
| `users` | Tabella centrale. Il campo `attivo` gestisce la revoca login (quando false → accesso bloccato immediatamente) |
| `richieste_ingresso` | Unico punto di ingresso per tutto ciò che viene dall'esterno. Lo `stato` traccia il percorso in Acquisition |
| `servizi_attivi` | Fonte ufficiale. Non si modifica direttamente: ogni cambio passa per `eventi_operativi` |
| `candidature` | Traccia l'intera vita di una candidatura personale a un'opportunità |
| `partner` | Semplice anagrafica partner con tracking clienti portati |
