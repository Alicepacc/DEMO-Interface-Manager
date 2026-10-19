# Registro delle versioni

Ogni versione dell'applicazione indica il formato dei dati (`schema`) che produce. I progetti salvati con un formato precedente vengono convertiti automaticamente all'apertura. Prima della conversione viene conservata una copia identica dei dati originali come versione del progetto.

## 3.3 — formato dati 5

**Menu a tendina modificabili**
- Aprendo un menu delle schede compare l'elenco delle voci con:
  - il simbolo "−" accanto a ogni voce, per toglierla dall'elenco del progetto;
  - "＋ Aggiungi…" in fondo, per inserire un valore nuovo;
  - "⚙ Gestisci", che apre la gestione dell'elenco.
- Rimuovere una voce non modifica gli oggetti che la usano: la conservano e la mostrano come "non in elenco". Le categorie usate da interfacce non si rimuovono.
- Il menu si usa anche da tastiera (Invio apre, frecce, Invio sceglie, Esc chiude).
- Anche la direzione della porta è ora un elenco configurabile. Resta fisso solo il lato della porta sul diagramma.

**Impostazioni**
- Organizzate in schede: Generale, Valori dei campi, Categorie di interfaccia, Campi personalizzati.
- "Valori dei campi" gestisce tutti gli elenchi del progetto, compresi i sottotipi delle categorie e i campi personalizzati a elenco. Per ogni voce si può:
  - aggiungere;
  - rinominare (gli oggetti che la usano vengono aggiornati);
  - eliminare;
  - spostare.

  Per ogni voce è indicato quanti oggetti la usano.

**Tabelle**
- Pulsante "Colonne" in Gruppi, Componenti, Interfacce, Cavi e Requisiti per scegliere le colonne visibili. La scelta è salvata nel browser e vale nelle sessioni successive.
- Esporta CSV usa le colonne mostrate.
- Il CSV delle Interfacce ha colonne fisse: ID Interfaccia, Rev Interfaccia, Categoria, Gruppo di derivazione A, Componente A, Porta A, Gruppo di derivazione B, Componente B, Porta B, ID Cavo, Tipo Cavo, PN Fornitore Cavo, PN IDV Cavo, Stato, Sottotipo, Note / Descrizione dello Scambio. Seguono i campi personalizzati delle interfacce, con una riga per ogni cavo.

**Interfacce**
- Nuovo campo "Revisione (Rev)" con il pulsante "↑ Nuova revisione" (A → B, 01 → 02).
- Il cambio di revisione è registrato nello storico.
- La revisione compare nel titolo della scheda, nella tabella, sulla lavagna e nel CSV.

**Cavi**
- Torna il campo "Tipo cavo", come elenco configurabile (RF, Twisted Pair, Coassiale, Schermato, Fibra Ottica, Ethernet, Alimentazione, Altro).
- Nuovi campi "PN fornitore" e "PN IDV". "PN IDV" è il campo che prima si chiamava "Specifica / part number": i valori già inseriti compaiono lì.

**Campi personalizzati**
- Definibili in Impostazioni per gruppi, componenti, interfacce, cavi e requisiti.
- Tipi disponibili: testo, numero, elenco, data, casella.
- Compaiono:
  - nelle schede;
  - come colonne delle tabelle;
  - nella ricerca e nell'ordinamento;
  - nei filtri (elenco e casella);
  - nelle esportazioni CSV.

**Migrazione dal formato 4**
- Tipi di cavo: nuovo elenco predefinito più i tipi già usati dai cavi esistenti, che restano invariati.
- Aggiunto l'elenco configurabile delle direzioni delle porte.
- Revisione vuota per le interfacce esistenti.
- Nessun campo personalizzato.

## 3.2 — formato dati 4

**Lavagna**
- Etichette dei collegamenti (interfacce e cavi) spostabili con il mouse. Restano agganciate alla loro linea e la seguono quando si spostano i blocchi. Clic destro → "Ripristina posizione automatica dell'etichetta".
- Spostamento di precisione con le frecce della tastiera (Maiusc = passi da 10) per:
  - blocchi;
  - gruppi;
  - etichette (con la linea selezionata);
  - punti di instradamento (con il punto selezionato).

  Pressioni consecutive sullo stesso elemento si annullano con un solo Ctrl+Z.
- Trascinamento dei blocchi sulla griglia di 10; con Alt premuto lo spostamento è libero.
- Un clic su un blocco apre la scheda lasciando il cursore sulla lavagna, così le frecce spostano subito il blocco.

**Schede più semplici**
- Le coordinate X/Y non compaiono più nella scheda e nella tabella dei componenti: la posizione si cambia solo sulla lavagna. Salvare una scheda non riporta più indietro un blocco spostato mentre era aperta.
- L'etichetta della porta è facoltativa.
- Tolti dall'interfaccia tipo di cavo, lunghezza e schermatura (scheda, tabella, etichette e controlli). I valori già inseriti restano nei dati del progetto.

**Valori nuovi dai menu a tendina**
- Ogni menu delle schede termina con "＋ Aggiungi…", che aggiunge un valore all'elenco del progetto e lo seleziona. Vale per:
  - dominio e owner;
  - tipo di porta;
  - stato;
  - tipo, origine e metodo di verifica dei requisiti;
  - categoria e sottotipo dell'interfaccia.
- Nei menu di oggetti la voce crea l'oggetto: "＋ Nuovo componente…", "＋ Nuova porta…", "＋ Nuovo gruppo…".
- I valori nuovi scritti nei campi con suggerimenti (protocollo, connettori) vengono aggiunti ai suggerimenti al salvataggio.
- Stati e liste dei requisiti sono ora elenchi modificabili in Impostazioni.

**Cartella di lavoro condivisa**
- Rinominando un progetto si rinomina anche la sua sottocartella. Gli altri computer che hanno il progetto aperto lo ritrovano nella nuova posizione.

**Migrazione dal formato 3**
- Aggiunti gli elenchi configurabili degli stati di componenti, interfacce e cavi e degli stati, tipi, origini e metodi di verifica dei requisiti, con i valori usati finora.
- Aggiunta la posizione delle etichette spostate a mano (vuota per i progetti esistenti).

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
