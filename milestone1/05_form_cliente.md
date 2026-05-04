# Form Cliente — Nuova Richiesta

Il form e' diviso in 2 step. I campi del secondo step variano in base al tipo di servizio selezionato nel primo.

---

## Flusso generale

```mermaid
flowchart TD
    S1[STEP 1\nDati personali e tipo servizio]

    S1 --> DATI[Nome e cognome\nEmail\nTelefono]
    DATI --> TIPO{Tipo di servizio}

    TIPO --> A[Assistenza domiciliare a ore]
    TIPO --> B[Badante notturna]
    TIPO --> C[Badante 24h]
    TIPO --> D[Economia domestica]
    TIPO --> E[Altro]

    A --> FREQ_A{Una volta sola\no continuativo?}
    B --> FREQ_B{Una volta sola\no continuativo?}
    C --> FREQ_C{Una volta sola\no continuativo?}
    D --> FREQ_D{Una volta sola\no continuativo?}
    E --> FREQ_E{Una volta sola\no continuativo?}

    FREQ_A --> S2[STEP 2\nDettagli intervento]
    FREQ_B --> S2
    FREQ_C --> S2
    FREQ_D --> S2
    FREQ_E --> S2

    S2 --> CAMPI[Campi adattativi\nvedi tabella sotto]
    CAMPI --> NOTE[Note aggiuntive opzionali]
    NOTE --> INVIA[Invia richiesta\nva in Admin — Inbound Requests]
```

---

## Campi adattativi Step 2 per tipo di servizio

| Tipo servizio | Orario inizio | Durata intervento | Data intervento | Data inizio | Note |
|---|---|---|---|---|---|
| Assistenza domiciliare a ore — una volta | Si | Si | Si | No | Opzionale |
| Assistenza domiciliare a ore — continuativo | Si | Si | No | Si | Opzionale |
| Badante notturna — una volta | Si | No | Si | No | Opzionale |
| Badante notturna — continuativo | Si | No | No | Si | Opzionale |
| Badante 24h — una volta | No | No | Si | No | Opzionale |
| Badante 24h — continuativo | No | No | No | Si | Opzionale |
| Economia domestica — una volta | Si | Si | Si | No | Opzionale |
| Economia domestica — continuativo | Si | Si | No | Si | Opzionale |
| Altro — una volta | Si | Si | Si | No | Opzionale |
| Altro — continuativo | Si | Si | No | Si | Opzionale |

> Logica: la durata non viene chiesta per badante notturna (si intende l'intera notte) e badante 24h (si intende l'intera giornata). L'orario non viene chiesto per badante 24h.
