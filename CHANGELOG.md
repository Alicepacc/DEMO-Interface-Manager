# Registro delle versioni

Ogni rilascio dell'applicazione indica il formato dei dati (`schema`) che produce. I progetti salvati con un formato precedente vengono convertiti automaticamente all'apertura. Prima della conversione viene conservata una copia identica dei dati originali come versione del progetto.

**Numerazione dei rilasci: "Rev X.YY".** Da Rev 1.00 la numerazione riparte:
- rilascio **Major** (es. 1.15 → 2.00): cambiamenti sostanziali, come un nuovo formato dei dati;
- rilascio **Minor** (es. 1.15 → 1.16): correzioni e miglioramenti.

Ogni rilascio ha in Git il tag `rev-X.YY`. I rilasci precedenti (da 1.0 a 3.3) sono elencati più sotto con la loro numerazione originale.

## Rev 3.00 — formato dati 8

**Pinout condiviso fra connettore del componente e connettore del cavo**
- Il pinout è uno solo per il connettore del componente e per il connettore del cavo collegato.
- Nella scheda del cavo ogni estremo mostra il pinout del connettore scelto: compare già compilato appena si sceglie il connettore e si può modificare da lì. Le modifiche valgono anche nella scheda del componente, e viceversa.
- Nuove colonne "Pinout A" e "Pinout B" nella tabella Cavi e "Pinout" nella tabella Componenti; sono nascoste all'inizio e si attivano con Colonne ▾.

**Tabelle**
- Le colonne si spostano trascinando l'intestazione con il tasto sinistro del mouse. Vicino ai bordi la tabella scorre da sola; "Ordine predefinito" ripristina l'ordine iniziale.
- **Colonne da altre viste**: in Colonne ▾ si sceglie un oggetto collegato alla riga e uno dei suoi campi.
  - I campi disponibili sono le colonne delle altre tabelle e i campi dei connettori.
  - Esempi: nei Cavi "Connettore componente A → Tipologia" diventa la colonna "Tipologia connettore componente A"; nelle Interfacce "Componente A → Fornitore"; nei Cavi "Interfacce → Livello 1".
  - Con più oggetti collegati i valori sono separati da virgola. L'intestazione è modificabile.
- Le colonne aggiunte entrano nella ricerca, nell'ordinamento e nel CSV. Nel CSV delle interfacce, che ha un formato fisso, vanno in fondo.
- Scelta, ordine e colonne aggiunte restano salvati nel browser di ciascun utente.

**Esportazione PDF / SVG**
- Il pulsante "Esporta PDF / SVG" apre una finestra in cui si scelgono:
  - il formato: **PDF vettoriale**, generato dall'applicazione senza librerie esterne (funziona anche offline), oppure SVG;
  - il foglio: A4, A3, A2, A1, A0 orizzontale o verticale, oppure grande quanto il disegno;
  - il **bordo con i riferimenti di zona**: lettere A, B, C… sui lati e numeri 1, 2, 3… in alto e in basso, con campi di circa 50 mm, senza I e O.
- **Cartiglio modificabile**: intestazione e voci Titolo, Programma, N. documento, Revisione, Autore, Verificato, Approvato e Data.
  - Si possono aggiungere altre voci; Titolo, Programma, Autore e Data lasciati vuoti si compilano da soli.
  - Facoltativamente si aggiungono vista, contenuto e filtro dello schema.
  - Le impostazioni del foglio e del cartiglio sono salvate nel progetto.
- Le immagini dei componenti sono incluse nel file; testi e linee restano vettoriali.

**Lavagna**
- **Immagine del componente**: nella scheda del componente, "Sulla lavagna" sceglie fra rettangolo schematico e una delle immagini allegate. L'immagine compare nel blocco fra l'intestazione e i connettori, e i collegamenti restano agganciati ai connettori.
- **Testi per intero**: l'etichetta e la tipologia dei connettori non vengono più troncate (prima, ad esempio, "AUDI" al posto di "AUDIO"); il blocco si allarga quanto serve.
- Nuove opzioni nel **menu Filtro → Mostra nella vista cavi**, ricordate e incluse nell'esportazione:
  - **Tipologia dei connettori**: la tipologia del connettore del componente è scritta fuori dal blocco, sopra il cavo collegato;
  - **PN dei cavi**: PN fornitore e PN IDV accanto all'ID di ogni cavo.
- **Rami delle interfacce**: nella vista interfacce il tratto finale di un'interfaccia si trascina in alto o in basso lungo il lato del componente. La posizione resta salvata; dal clic destro si torna agli "Agganci automatici ai componenti".

**Componenti e gruppi funzionali**
- Il campo "Funzione" del connettore diventa **Etichetta**, completamente libera (es. AUDIO, RS-422 CTRL, 28 VDC IN). L'elenco delle funzioni resta per la "Funzione cavo".
- I connettori si riordinano **trascinando la maniglia ⠿** della riga, oppure con ↑ / ↓ da tastiera; le frecce ▲▼ sono state tolte.
- Nella scheda del gruppo, un componente compilato nei campi "Nuovo componente" ma non aggiunto viene **aggiunto premendo direttamente "Salva"**. Se i suoi dati non sono validi il salvataggio si ferma con un avviso.
- **Copia di componenti esistenti** in un gruppo, anche durante la creazione del gruppo (es. Radio RED): la copia ha un nuovo ID modificabile (RAD → RAD-2) e gli stessi dati, connettori, pinout e allegati. L'originale resta nel suo gruppo; interfacce e cavi non vengono copiati.

**Sigle**
- La sigla predefinita di Elettrica di potenza passa da PWR a **ELP**, per non confonderla con quella del Livello 2 Power (PWR). Gli ID diventano, ad esempio, `ELP.PWR:PDU.VCU`.

**Migrazione dal formato 7**
- La funzione dei connettori diventa la loro etichetta, senza modifiche al valore.
- Nei progetti in cui Elettrica di potenza ha ancora la sigla PWR, la sigla diventa ELP e gli ID delle interfacce si aggiornano. Una sigla già personalizzata non cambia.
- Il foglio di esportazione parte da A3 orizzontale con bordo e con le voci predefinite del cartiglio.

## Rev 2.00 — formato dati 7

**Interfacce**
- Rimossi dalla scheda dell'interfaccia: Nome, Protocollo / standard, Porta A, Porta B e "Scambia A/B". Un'interfaccia collega direttamente il componente A e il componente B.
- **Lato A e lato B seguono sempre l'ordine alfabetico** degli ID dei componenti (es. GPS è il lato A e VCU il lato B), anche quando un componente viene rinominato.
- "Categoria" e "Sottotipo" diventano **Interfaccia Livello 1** e **Interfaccia Livello 2**. Valori iniziali:
  - Meccanica: Statica, Dinamica;
  - Fluidica: Aria, Acqua, Olio, Gas combustibile, Combustibile;
  - Segnale: Dati analogici, Dati discreti, Comunicazioni, Sincronizzazione, Service;
  - Elettrica di potenza: Power.
- **ID automatico** nella forma `L1.L2:A.B`, composto dalle sigle dei livelli e dagli ID dei componenti A e B, per esempio `SEG.COM:GPS.VCU`. Se due interfacce hanno gli stessi livelli e gli stessi componenti, la seconda riceve il suffisso `-2`, la terza `-3` e così via.
  - L'ID non si modifica a mano. Si aggiorna da solo quando cambiano i livelli, le loro sigle o gli ID dei componenti, e resta stabile negli altri casi.
  - Le sigle iniziali sono MEC (STA, DIN), FLU (ARIA, H2O, OLIO, GAS, COMB), SEG (ANA, DIS, COM, SYNC, SRV) e PWR (PWR). Si cambiano in **Impostazioni → Livelli di interfaccia** e, per un nuovo valore, nella finestra che lo crea dal menu.
  - Le sigle non possono contenere spazi, "." o ":". Gli ID dei componenti non possono contenere "." o ":".
- Il riquadro "Percorso sulla lavagna" è stato tolto dalle schede di interfacce e cavi; il suo contenuto è nella Guida ("Percorso sulla lavagna: automatico o manuale").

**Cavi**
- **ID automatico progressivo** W-001, W-002…, assegnato al salvataggio. I numeri dei cavi eliminati non vengono riusati.
- "Tipo cavo" diventa **Funzione cavo**, con i valori Ethernet, Seriale, CAN, USB, RF, Alimentazione: lo stesso elenco della funzione dei connettori, modificabile da **Impostazioni → Valori dei campi → Funzioni**.
- Su ogni estremo il connettore del cavo ha un solo campo, **Tipo connettore cavo**; l'ID del connettore lato cavo è stato rimosso.
- Dal menu del connettore di un estremo si può creare un nuovo connettore del componente ("Nuovo connettore…").

**Componenti e connettori**
- Rimossi dal componente: Dominio e Owner. L'Owner resta su gruppi, interfacce e requisiti.
- Le **porte non esistono più**: ogni componente ha soltanto i suoi **connettori**, in una tabella con ID, **Funzione**, **Tipologia**, **Direzione** e **Pinout** (pin e segnale). L'ordine (▲▼) è quello dei connettori sulla lavagna.
- Le immagini allegate mostrano subito una **miniatura**; un clic la ingrandisce. Gli altri file mantengono il pulsante "Anteprima".
- Nella finestra del gruppo funzionale i nuovi componenti si creano con i loro connettori iniziali (ID e tipologia).
- I requisiti si collegano a interfacce, cavi, componenti e connettori.

**Lavagna**
- Vista interfacce: i collegamenti vanno **da componente a componente**. Si crea un'interfaccia trascinando dalla maniglia sul lato di un blocco fino a un altro blocco.
- Vista cavi: si trascina da un connettore a un altro, oppure sulla sua riga nel blocco. La finestra "Nuovo cavo" propone la funzione comune ai due connettori.
- Durante il trascinamento di un collegamento, avvicinandosi al bordo **la lavagna scorre da sola**: non serve più ridurre lo zoom per raggiungere un blocco lontano.
- Le etichette mostrano **solo l'ID**, sia delle interfacce sia dei cavi.
- Nei blocchi le righe dei connettori riportano ID, tipologia, funzione e direzione. L'intestazione non mostra più dominio e owner.
- Il pulsante "Porte" della barra diventa "Connettori".

**Tabelle, CSV e Dashboard**
- Tabella Interfacce: Livello 1, Livello 2, Comp. A e Comp. B; filtro per Livello 1. Tabella Cavi: Funzione cavo (anche come filtro) e Tipo connettore cavo A/B. Tabella Componenti: numero ed elenco dei connettori.
- CSV delle interfacce: le colonne sono ID Interfaccia, Rev Interfaccia, Interfaccia Livello 1, Gruppo di derivazione A, Componente A, Connettore A, Gruppo di derivazione B, Componente B, Connettore B, ID Cavo, Funzione Cavo, PN Fornitore Cavo, PN IDV Cavo, Stato, Interfaccia Livello 2, Note / Descrizione dello Scambio. I connettori sono quelli degli estremi del cavo.
- Dashboard: nuovi controlli "Interfacce con livelli non previsti", "Funzioni non previste" e "Componenti senza connettori"; i controlli delle porte sono sostituiti da quelli dei connettori.

**Migrazione dal formato 6 (e precedenti)**
- Le porte confluiscono nei connettori:
  - la funzione del connettore viene dal tipo delle sue porte (Power/Ground → Alimentazione, Serial → Seriale, Ethernet, RF, Optical → Ethernet);
  - la direzione è quella comune alle porte, Bidirectional se sono diverse;
  - con più porte nello stesso connettore, il nome della porta viene aggiunto al segnale nel pinout.
- Porte senza connettore:
  - le porte elettriche e di dati diventano connettori, con i pin che avevano;
  - le porte meccaniche, fluidiche e software sono eliminate, mentre le interfacce restano fra i componenti.
- Cavi, interfacce e requisiti che puntavano a una porta passano al connettore che l'ha assorbita, oppure al componente.
- Nome e protocollo delle interfacce sono conservati nella descrizione ("Nome — descrizione", "Protocollo / standard: …").
- Gli ID diventano automatici:
  - interfacce `L1.L2:A.B`;
  - cavi W-001, W-002… nell'ordine dei loro ID precedenti.
- I vecchi livelli e i vecchi tipi di cavo che non corrispondono ai nuovi elenchi restano invariati finché l'utente non sceglie i valori da assegnare:
  - all'apertura del progetto convertito compare la finestra **"Assegna i nuovi livelli e le funzioni"**, con proposte precompilate (es. Elettrica / Alimentazione → Elettrica di potenza / Power; Twisted Pair → Seriale);
  - con "Decidi dopo" la Dashboard continua a segnalarli e la finestra si riapre dalla Dashboard o da Impostazioni → Livelli di interfaccia;
  - l'assegnazione aggiorna gli ID e si annulla con un solo passo.
- Dominio e owner dei componenti e l'ID del connettore lato cavo non sono più usati; restano nella copia del progetto salvata prima della migrazione.

## Rev 1.00 — formato dati 6

**Connettori**
- Nuovo livello del modello: il connettore fisico è il contenitore delle porte funzionali (Componente └ Connettore ├ Porta 1 … Porta N). Esempi: "J1 – MIL-DTL-38999" con le porte A, B, C, D; "MISC – 20ZD-35SN" con le porte RS232, GPIO e PPS.
- Ogni connettore ha ID, **Tipo connettore** (testo libero) e **pinout**: pin, segnale e porta a cui appartiene. Il pinout appartiene solo al connettore lato componente.
- L'ID della porta è univoco nel suo connettore (J1.A e J2.A possono coesistere). Riferimento completo: COMPONENTE:CONNETTORE.PORTA (es. VCU:J2.CTRL); una porta senza connettore resta COMPONENTE:PORTA.
- Porte senza connettore ammesse (servizi software, punti di fissaggio, raccordi).

**Scheda del componente**
- Nuovi campi **PN fornitore** e **PN IDV**.
- Sezione "Connettori e porte": un riquadro per connettore (ID, tipo, porte, pinout) e uno per le porte senza connettore.
- Le porte si trascinano da un riquadro all'altro; "+ Connettore" e "+ Porta" in ogni riquadro; l'ordine (▲▼) definisce la posizione sulla lavagna.
- **Trasforma in connettore**: la porta J1 diventa il connettore J1 con dentro una porta che prende l'ID dall'etichetta; i pin che i cavi avevano su quella porta entrano nel pinout del connettore e i cavi passano al connettore.
- Controlli: ID dei connettori obbligatori e univoci, ID delle porte univoci nel connettore, pin ripetuti.
- Eliminando un connettore le porte restano (senza connettore); i cavi che vi arrivavano restano senza connettore del componente.
- Rimosso "Sposta in…".

**Cavi**
- Campi del cavo: ID, stato, interfacce logiche associate (**una o più**), tipo cavo, PN fornitore, PN IDV, estremi, requisiti, note.
- Ogni **estremo** (A, B, C…) indica il componente, il connettore del componente e il connettore del cavo su quel lato (ID e tipo, testo libero).
- **Cavi ramificati** (bifidi, trifidi…): "+ Estremo" aggiunge un ramo.
- "↺ Allinea estremi alle interfacce" ricava gli estremi dai connettori delle porte delle interfacce scelte.
- Rimossi dal cavo: funzione / descrizione e pinout (il pinout è del connettore del componente).
- Tabella Cavi: interfacce, componente, connettore del componente e connettore del cavo per gli estremi A e B, altri estremi, PN.
- Le interfacce restano punto–punto: un bus si modella come più interfacce sullo stesso cavo. Il CSV delle interfacce ha una riga per ogni cavo, anche quando un cavo porta più interfacce.

**Creazione dei cavi**
- Nella vista cavi si trascina da un connettore a un altro. La finestra "Nuovo cavo" propone le interfacce fra quei connettori e offre:
  - **Associa il cavo a un'interfaccia esistente** (anche più di una);
  - **Crea nuova interfaccia**, che apre la scheda dell'interfaccia con le porte dei due connettori.
- Nella scheda dell'interfaccia: "Associa a un cavo esistente…" accanto a "+ Cavo per questa interfaccia".
- ID proposto per il cavo: IF-CTRL-01 → CBL-CTRL-01 (o il primo numero libero).

**Lavagna**
- I blocchi mostrano i connettori come righe di intestazione (▣ ID, tipo, numero di pin) seguite dalle loro porte.
- Vista interfacce: linee da porta a porta. Vista cavi: linee da connettore a connettore, maniglie di collegamento sui connettori.
- I cavi ramificati sono disegnati a Y: un ramo dal punto di diramazione (●) a ogni estremo. Il punto si trascina con il mouse, si sposta con le frecce quando è selezionato e torna in posizione automatica dal menu del clic destro.
- La legenda (in basso a sinistra) e la descrizione dei comandi (in basso a destra) si riducono a un pulsante; la scelta resta memorizzata. Corretto il clic sulle categorie della legenda, che non aveva effetto.
- Menu delle porte raggruppati per connettore.

**Dashboard**
- Nuovi controlli: "Connettori collegati senza pinout", "Pin ripetuti nei connettori", "Interfacce non raggiunte dal loro cavo".
- Copertura: "Cavi con tutti i connettori indicati" e "Connettori cablati con pinout".

**Altro**
- La finestra che all'avvio chiede di consentire l'accesso alla cartella condivisa è più compatta: le scelte sono una sotto l'altra, dentro il riquadro.
- Il numero di rilascio ("Rev 1.00") compare nell'intestazione, nelle Impostazioni e nella Guida.
- Guida: nuove sezioni "Connettori, porte e pinout" e "Cavi: estremi, interfacce e cavi ramificati"; numerazione dei rilasci.

**Migrazione dal formato 5**
- Le porte esistenti restano senza connettore: si organizzano trascinandole nei connettori o con "Trasforma in connettore".
- Ogni cavo diventa un cavo a due estremi:
  - interfaccia → interfacce associate (una);
  - componente e porta A/B → estremi A/B, sulla porta (o sul suo connettore, se ne ha uno);
  - connettori A/B (testo) → tipo del connettore lato cavo.
- I pin del pinout dei cavi vengono conservati sulle porte del componente e diventano il pinout del connettore quando la porta entra in un connettore. Funzione / descrizione dei cavi resta nella copia del progetto salvata prima della migrazione.

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
