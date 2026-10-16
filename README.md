# IDV Interface Manager

Applicazione web in un unico file (`IDV_Interface_Manager.html`) per disegnare e gestire architetture di sistema, interfacce, interconnessioni e requisiti.

Il modello ha cinque livelli: gruppi funzionali, componenti, porte, interfacce logiche e cavi fisici. Include anche requisiti, allegati, dashboard di completezza, lavagna con instradamento ortogonale e progetti multipli.

Non richiede installazione né server: basta aprire il file in un browser recente (Chrome, Edge, Firefox).

## Codice e dati sono separati

| Cosa | Dove si trova | Come è versionato |
|------|---------------|-------------------|
| **Codice dell'applicazione** | `IDV_Interface_Manager.html` (questo repository) | Git: ogni rilascio è un commit; le versioni sono in `CHANGELOG.md` |
| **Dati dei progetti** | Archivio del browser (IndexedDB) di ciascun computer, separato dal file HTML | Versioni interne del progetto, storico delle modifiche, esportazioni JSON, backup completi e, se collegati, repository GitHub dei progetti |

Sostituire o aggiornare il file HTML **non tocca i dati**, purché l'applicazione venga aperta nello stesso browser e dallo stesso indirizzo (stesso percorso del file o stesso sito).

## Versioni e migrazione dei dati

- `APP.version` è la versione dell'applicazione, per esempio `3.0`.
- `APP.schema` è la versione del **formato dei dati**, per esempio `3`.

Ogni progetto, versione, esportazione e backup registra il formato con cui è stato salvato.

**Progetto in un formato precedente.** Quando viene aperto, l'applicazione:

1. conserva una copia identica dei dati originali come versione del progetto ("Copia automatica prima dell'aggiornamento del formato dati");
2. converte i dati al formato corrente (`normalizeData`);
3. registra l'operazione nello storico delle modifiche.

**Progetto in un formato più recente.** Una copia più vecchia dell'applicazione **non apre** il progetto, per non perdere informazioni: bisogna aggiornare il file HTML.

Ogni modifica al formato dei dati deve:

1. incrementare `APP.schema`;
2. aggiungere in `normalizeData` la conversione dal formato precedente (vedi il blocco *Migrazione dei dati salvati con versioni precedenti del formato*);
3. essere descritta in `CHANGELOG.md`.

## Procedura consigliata per aggiornare l'applicazione

1. Nell'applicazione in uso, apri **Progetti → Backup completo** (oppure invia i progetti a GitHub).
2. Sostituisci `IDV_Interface_Manager.html` con la nuova versione, nello stesso percorso o sullo stesso sito.
3. Riapri l'applicazione: i progetti vengono aggiornati automaticamente all'apertura.
4. In caso di problemi:
   - **Progetti → Versioni**: ripristina la copia precedente alla migrazione;
   - **Ripristina backup**: ripristina l'intero archivio.

Per il lavoro in team conviene pubblicare l'applicazione a un indirizzo fisso, ad esempio un sito interno o GitHub Pages di questo repository.

## Progetti, cartelle, backup e GitHub

- **Progetti e cartelle.** Progetti indipendenti, organizzati in cartelle e sottocartelle, con cestino. Il salvataggio è automatico a ogni modifica.
- **Versioni.** Le versioni sono:
  - automatiche: ogni 20 minuti di lavoro e prima di importazioni, ripristini e migrazioni;
  - manuali: ad esempio le baseline.

  Ogni versione si può confrontare con lo stato attuale e ripristinare.
- **Storico delle modifiche.** Registro persistente di ogni operazione, con data, utente e descrizione. È esportabile in CSV.
- **Esporta / Importa JSON.** File completo e autosufficiente: dati, allegati in base64, versioni e storico.
- **Backup completo.** Un unico file con tutti i progetti, le cartelle, le versioni e gli allegati. "Ripristina backup" chiede cosa fare dei progetti già presenti.
- **GitHub.** Ogni progetto può essere collegato a un proprio repository, oppure a una cartella di un repository condiviso. Struttura nel repository:

  ```
  <cartella>/project.json        dati del progetto, storico, indice degli allegati
  <cartella>/attachments/...     file allegati
  <cartella>/README.md           riepilogo
  ```

  Funzioni disponibili:
  - "Invia" crea un commit;
  - "Aggiorna da GitHub" e "Cronologia" recuperano qualsiasi revisione;
  - "Apri da GitHub" permette a un collega di aprire il progetto.

  Se il progetto è stato modificato da altri dopo l'ultimo invio, l'applicazione avvisa prima di inviare.

  Il token di accesso resta solo nel browser e non viene mai scritto nei file. È consigliato un token *fine-grained* con permesso *Contents: read and write* limitato ai repository dei dati.

## Test

Le verifiche automatiche, in Playwright, coprono:

- lavagna, instradamento e punti di instradamento;
- filtri, allegati e progetti;
- importazione ed esportazione, backup e migrazione dei dati;
- sincronizzazione GitHub, su un server simulato.

Sono state eseguite durante lo sviluppo su Chromium.
