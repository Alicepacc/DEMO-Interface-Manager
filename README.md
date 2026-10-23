# IDV Interface Manager

Applicazione web in un unico file (`IDV_Interface_Manager.html`) per disegnare e gestire architetture di sistema, interfacce, interconnessioni e requisiti.

Il modello ha cinque livelli: gruppi funzionali, componenti, connettori (funzione, tipologia, direzione e pinout), interfacce logiche fra due componenti (Interfaccia Livello 1 e Livello 2, ID automatico `L1.L2:A.B`) e cavi fisici (ID automatico W-001…, anche ramificati, connettore → connettore). Include anche requisiti, allegati, campi personalizzati, dashboard di completezza, lavagna con instradamento ortogonale e progetti multipli.

Non richiede installazione né server: basta aprire il file in un browser recente (Chrome, Edge, Firefox). Per salvare i progetti in una cartella condivisa (OneDrive, Teams/SharePoint, cartella di rete) serve Microsoft Edge o Google Chrome.

## Codice e dati sono separati

| Cosa | Dove si trova | Come è versionato |
|------|---------------|-------------------|
| **Codice dell'applicazione** | `IDV_Interface_Manager.html` (questo repository) | Git: ogni rilascio è un commit con il tag `rev-X.YY`; le versioni sono in `CHANGELOG.md` |
| **Dati dei progetti** | A scelta, in **Progetti → Posizione dei progetti**: una **cartella di lavoro condivisa** (file `.idvproj` su OneDrive/Teams) oppure l'**archivio del browser** (IndexedDB) di ciascun computer. In entrambi i casi sono separati dal file HTML | Versioni del progetto, storico delle modifiche, esportazioni JSON, backup completi e, se collegati, repository GitHub dei progetti |

Sostituire o aggiornare il file HTML **non tocca i dati**. Con l'archivio del browser, l'applicazione va riaperta nello stesso browser e dallo stesso indirizzo (stesso percorso del file o stesso sito).

## Versioni e migrazione dei dati

- `APP.version` è il rilascio dell'applicazione, "Rev X.YY", per esempio `2.00`:
  - **Major** (1.15 → 2.00) per cambiamenti sostanziali, come un nuovo formato dei dati;
  - **Minor** (1.15 → 1.16) per correzioni e miglioramenti.

  La numerazione è ripartita da Rev 1.00 dopo il rilascio 3.3.
- `APP.schema` è la versione del **formato dei dati**, per esempio `7`.

Ogni progetto, versione, esportazione e backup registra il formato con cui è stato salvato.

**Progetto in un formato precedente.** Quando viene aperto, l'applicazione:

1. conserva una copia identica dei dati originali come versione del progetto ("Copia automatica prima dell'aggiornamento del formato dati");
2. converte i dati al formato corrente (`normalizeData`);
3. registra l'operazione nello storico delle modifiche;
4. dal formato 7: se il progetto usa livelli di interfaccia o funzioni che non corrispondono ai nuovi elenchi, chiede quali valori assegnare (finestra "Assegna i nuovi livelli e le funzioni").

**Progetto in un formato più recente.** Una copia più vecchia dell'applicazione **non apre** il progetto, per non perdere informazioni: bisogna aggiornare il file HTML.

Ogni modifica al formato dei dati deve:

1. incrementare `APP.schema`;
2. aggiungere in `normalizeData` la conversione dal formato precedente (vedi il blocco *Migrazione dei dati salvati con versioni precedenti del formato*);
3. essere descritta in `CHANGELOG.md`.

## Procedura consigliata per aggiornare l'applicazione

1. Nell'applicazione in uso, apri **Progetti → Backup completo** (oppure invia i progetti a GitHub).
2. Sostituisci `IDV_Interface_Manager.html` con la nuova versione, nello stesso percorso o sullo stesso sito (con la cartella condivisa: il file nella cartella del team).
3. Riapri l'applicazione: i progetti vengono aggiornati automaticamente all'apertura.
4. In caso di problemi:
   - **Progetti → Versioni**: ripristina la copia precedente alla migrazione;
   - **Ripristina backup**: ripristina l'intero archivio.

Per il lavoro in team il modo più semplice è tenere il file HTML nella cartella condivisa insieme ai progetti. In alternativa si può pubblicare l'applicazione a un indirizzo fisso, ad esempio un sito interno o GitHub Pages di questo repository.

## Cartella di lavoro condivisa (OneDrive / Teams)

Pensata per ambienti in cui non si può installare software: i progetti sono normali file in una cartella sincronizzata, e la sincronizzazione tra computer la fa OneDrive. L'applicazione usa la File System Access API del browser (Edge o Chrome).

**Preparazione, una volta per il team**

1. Crea una cartella in OneDrive o nei File di un canale Teams, ad esempio `IDV Progetti`, e copiaci `IDV_Interface_Manager.html`.
2. Ogni utente, dalla pagina web di Teams/SharePoint, usa "Aggiungi collegamento a I miei file" (o "Sincronizza"): la cartella compare in Esplora file, sotto OneDrive.

**Collegamento, una volta per computer**

1. Apri il file HTML dalla cartella sincronizzata con Edge o Chrome.
2. **Progetti → Posizione dei progetti → Cambia… → Usa una cartella condivisa…** e scegli la cartella `IDV Progetti`.
3. Se nel browser ci sono già progetti, l'applicazione propone di copiarli nella cartella.
4. Imposta il tuo nome in **Impostazioni ⚙**: compare nello storico e negli avvisi ai colleghi.

A ogni avvio il browser chiede di confermare l'accesso alla cartella ("Consenti accesso a «IDV Progetti»"); la cartella scelta viene ricordata.

**Struttura su disco**

```
IDV Progetti/
  IDV_Interface_Manager.html
  <cartella>/<sottocartella>/<Nome progetto>/
    progetto.idvproj             dati, storico delle modifiche e metadati (JSON)
    allegati/<id>-<nome file>    file allegati ai componenti
    versioni/indice.json         elenco delle versioni
    versioni/<data>_<id>.json    una versione del progetto
    .presenza/<dispositivo>.json chi ha il progetto aperto (aggiornato ogni 2 minuti)
```

Le cartelle e sottocartelle dei progetti sono cartelle reali. Rinominando un progetto si rinomina anche la sua sottocartella. Le preferenze personali e il token GitHub restano nel browser di ciascuno.

**Lavoro contemporaneo**

- **Presenza.** La finestra Progetti mostra "● aperto da …". Aprendo un progetto già aperto da un collega si riceve un avviso.
- **Aggiornamenti.** Quando un altro utente salva il progetto aperto, compare un avviso con il pulsante per ricaricarlo. Il controllo avviene ogni 15 secondi e quando si torna sulla finestra.
- **Conflitti.** Prima di ogni salvataggio l'applicazione verifica che il file non sia cambiato. Se è cambiato, il salvataggio si ferma e si sceglie tra: aprire la versione del collega, salvare le proprie modifiche come copia separata, sovrascrivere. Nulla viene scartato in silenzio.
- **Copie di conflitto di OneDrive** (`progetto-<NomePC>.idvproj`). Vengono segnalate nella finestra Progetti e si possono importare come progetto separato.

Regola pratica: un solo utente alla volta modifica un progetto; per lavorare in parallelo conviene dividere lo schema in più progetti.

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

- lavagna, instradamento e punti di instradamento, spostamento con mouse e frecce di blocchi, gruppi ed etichette;
- ID automatici di interfacce (`L1.L2:A.B`, lati in ordine alfabetico, suffissi -2…) e cavi (W-001…, numeri mai riusati), sigle dei livelli modificabili;
- connettori (tabella nella scheda del componente, funzione, tipologia, direzione, pinout), cavi da connettore a connettore con più interfacce, cavi ramificati e punto di diramazione, finestra "Nuovo cavo";
- collegamenti trascinati sulla lavagna da componente a componente e da connettore a connettore, con scorrimento automatico vicino ai bordi; miniature degli allegati;
- schede e menu a tendina modificabili ("−" per rimuovere una voce, "＋ Aggiungi…"), gestione dei valori in Impostazioni con rinomina propagata agli oggetti;
- colonne visibili per tabella, campi personalizzati (colonne, filtri, ricerca, ordinamento, CSV), revisione delle interfacce ed esportazione CSV delle interfacce;
- filtri, allegati e progetti;
- importazione ed esportazione, backup e migrazione dei dati (dal formato 6: porte nei connettori e finestra di assegnazione dei nuovi livelli e funzioni; cavi del formato 5 con il loro pinout);
- sincronizzazione GitHub, su un server simulato;
- cartella di lavoro condivisa: due computer simulati sulla stessa cartella (presenza, aggiornamenti, conflitti, copie di conflitto di OneDrive, rinomina dei progetti) e cartelle reali del browser (cartella ricordata, conferma dell'accesso all'avvio).

Sono state eseguite durante lo sviluppo su Chromium. La sincronizzazione reale di OneDrive non è stata provata: per il primo utilizzo conviene un progetto di prova.
