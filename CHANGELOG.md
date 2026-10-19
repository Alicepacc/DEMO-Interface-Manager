# Registro delle versioni

Ogni versione dell'applicazione indica il formato dei dati (`schema`) che produce. I progetti salvati con un formato precedente vengono convertiti automaticamente all'apertura. Prima della conversione viene conservata una copia identica dei dati originali come versione del progetto.

## 3.1 — formato dati 3

**Cartella di lavoro condivisa (OneDrive / Teams)**
- Nuova posizione dei progetti, in alternativa all'archivio del browser: una cartella sincronizzata (OneDrive, Teams/SharePoint, cartella di rete). Si sceglie da Progetti → Posizione dei progetti. Richiede Edge o Chrome; nessuna installazione.
- Ogni progetto è una sottocartella con:
  - `progetto.idvproj`;
  - la cartella `allegati`;
  - la cartella `versioni`.
- Le cartelle dei progetti sono cartelle reali.
- Copia dei progetti esistenti dal browser alla cartella.
- La cartella scelta viene ricordata; a ogni avvio il browser chiede di confermare l'accesso.
- Presenza: "● aperto da …" nella finestra Progetti e avviso se si apre un progetto già aperto da un collega.
- Avviso quando un collega salva il progetto aperto, con ricarica.
- Rilevamento dei conflitti prima di ogni salvataggio, con scelta tra:
  - la versione del collega;
  - una copia con le proprie modifiche;
  - la sovrascrittura.
- Rilevamento delle copie di conflitto create da OneDrive e importazione come progetto separato.
- Nuova sezione della Guida sul lavoro in team con la cartella condivisa.

Il formato dei dati non cambia (formato 3). I file `progetto.idvproj` usano lo stesso formato dei file di progetto esportati (`IDV-Interface-Manager-Project`).

## 3.0 — formato dati 3

**Lavagna**
- Percorsi manuali con punti di instradamento:
  - spostamento di tratti e punti;
  - aggiunta con doppio clic;
  - eliminazione con doppio clic o Canc;
  - menu contestuale.
- I percorsi manuali restano tali quando si spostano i blocchi collegati.
- Ogni modifica si annulla con Annulla/Ripeti.
- Auto-Rerouting con scelta se mantenere i percorsi manuali.
- Ripristinati i pulsanti di zoom − / +.
- Filtro per categoria e sottotipo di interfaccia, anche dalla legenda, con opzione per nascondere i componenti non coinvolti. L'esportazione SVG rispetta il filtro e lo riporta nel cartiglio.

**Categorie e componenti**
- Nuove categorie predefinite:
  - Software;
  - Rete/IP;
  - RF;
  - Fibra ottica.
- Nuovi tipi di porta: Optical e Software.
- Allegati dei componenti (immagini, PDF, Word, Excel, altri file) con anteprima e conteggio sulla lavagna e in tabella.

**Progetti e dati**
- Cartelle e sottocartelle dei progetti.
- Storico persistente delle modifiche.
- Confronto tra versioni.
- Esporta/Importa JSON completo (dati, allegati, versioni, storico).
- Backup completo e ripristino.
- Collegamento dei progetti a repository GitHub: invio come commit, aggiornamento, cronologia, apertura da GitHub e avviso di modifiche concorrenti.
- Archivio del browser alla versione 2, con un archivio separato per gli allegati.

**Migrazione dal formato 2**
- Aggiunte le nuove categorie e i nuovi tipi di porta.
- Aggiunto l'elenco allegati ai componenti.

## 2.0 — formato dati 2

**Progetti**
- Progetti multipli con salvataggio automatico.
- Versioni, cestino e file di progetto.

**Interfacce e requisiti**
- Interfacce classificate per categoria, sottotipo e protocollo.
- Requisiti con titolo e flag "Condivisibile con il fornitore".
- Esportazione Excel per il fornitore.

**Lavagna e componenti**
- Creazione di componenti dal gruppo funzionale.
- Lato fisso delle porte sul diagramma.
- Guida integrata.

## 1.1 — formato dati 1

- Lavagna in stile schema topologico.
- Instradamento ortogonale automatico.
- Auto-Rerouting.
- Annulla/Ripeti dei percorsi.

## 1.0 — formato dati 1

- Prima versione: gruppi, componenti, porte, interfacce, cavi, requisiti e dashboard.
- Salvataggio nel browser.
