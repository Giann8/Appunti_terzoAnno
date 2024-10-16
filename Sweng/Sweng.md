# Ingegneria del software

Il processo di produzione di un software si basa sulla comunicazione e sull’essere rigorosi, inoltre va a considerare diversi aspetti.

## Studio di fattibilità

Abbiamo varie scelte progettuali basate sullo studio degli scenari e le scelte architetturali. Lo studio di Fattibilità serve per capire anche la stima dei costi, dei tempi di sviluppo e delle risorse necessarie oltre che dei benefici delle diverse soluzioni. Possiamo farlo noi ma spesso, per non togliere persone dallo sviluppo del software, si assume uno specialista, l’output è un documento in linguaggio naturale.

## Analisi e specifica (raccolta e studio) dei requisiti

In un momento dobbiamo parlare con i clienti e capire il dominio applicativo in cui dobbiamo lavorare. Definiamo con **stakeholders** coloro che sono interessati allo sviluppo e al funzionamento dei processi. All’utente interessa solo il funzionamento, non il progetto o l’implementazione (non il **come**). Gli output possibili sono:

- documento di specifica: documento contrattuale approvato dal committente, è la base per il lavoro di design e verifica, i programmatori però preferiscono documenti più formali.
- Manuale utente.
- Piano dei test di sistema, che certificano la correttezza del software.

Non è importante scrivere ma capire.

## Progettazione

Devo scegliere l’architettura di sistema da avere come riferimento, scomporre in moduli e oggetto e identificare possibili pattern. Otteniamo così un documento di specifica del progetto.

## Programmazione e test di unità

Svolgo un testing isolato, devo quindi prima andare a creare dei test basati sul problema dato, da questi partirò scrivendo il codice che mi permetterà di risolvere il problema dato. I test saranno quindi totalmente isolati dal codice effettivo che voglio scrivere e direttamente basati sul problema, non interessa

I moduli vengono testati indipendentemente e possono essere divisi in:

- Moduli stub (fittizi)
- Moduli driver (guida)

L’output che otterremo saranno moduli sviluppati in modo separato, singolarmente verificati e con interfaccia concordata.

Successivamente avverrà l’**Integrazione** ovvero l’unione dei vari componenti, i moduli di testing vengono sostituiti ano a mano con i moduli reali.

Ho due approcci:

- Top-down:parto definendo un modulo reale che definisce l’interfaccia utente, mi illude di avere un programma completo (al di sotto sono invece presenti dei moduli fittizi).
- Bottom-up: parto da cose vere guidate dai moduli driver e fittizi, questi ovviamente non saranno visti dall’utente.

con entrambi si arriverà comunque ad ottenere un programma funzionante.

## Manutenzione

- correttiva: ho degli errori e li vado a risolvere correggendo il codice.
- Adattiva: adatto il codice a nuove leggi o specifiche.
- Perfettiva: software sufficientemente corretto ma miglioro performance, o comunque la qualità in generale del programma (refactoring) cambio quindi il codice senza modificarne la funzionalità.

### Attività finali

- Documentazione
    - Può essere un’attività trasversale
    - spesso nella pratica è un’attività a posteriori
- Verifica e controllo qualità
    - quality assurance
- Gestione del processo
    - gestione incentivi, responsabilità ed eccezioni
- Gestione configurazioni
    - relazioni inter-progettuali

### Approccio ingegneristico

1. Target: ci si prefigge un obiettivo da raggiungere
2. Metric: si definisce una metrica correlata al raggiungimento del target (non deve essere scelta a posteriori)
3. Method, process, tool: si definisce un metodo, strumento o processo che possa condurci al nostro target
4. Measurements: si confrontano le metriche stabilite nel caso di adozione o meno della tecnica sotto valutazione, valutando se sono state utili e quanto ci hanno avvicinato all’obiettivo, in base ai risultati ottenuto avremo:
    - risultati soddisfacenti ( un miglioramento della metrica) - andiamo ad accettare come buoni i metodi e processi proposti;
    - risultati insoddisfacenti (il peggioramento della metrica) -  si verificano peggioramenti o forti effetti collaterali, bisogna quindi modificare qualcosa come target o la metrica in caso ci si rendesse conto di non aver ben definito l’obiettivo, di solito bisogna però rivedere i processi e i metodi usati.

**Cosa si intende con target?** gli obiettivi da raggiungere possono essere:

1. la risoluzione dei problemi nello sviluppo del software;
2. l’assicurazione di una qualche qualità che il software dovrà avere.

### Modelli

- Modelli sequenziali
    - **Modello a cascata(lo usiamo solo come paragone negativo da non usare):** Creato come una sorta di catena di montaggio, questo modello forza una progressione lineare, impedendo di tornare indietro a uno step precedente. La maggior parte dei processi che utilizzano questo modello presentano almeno le seguenti fasi **`(separazione dei compiti)`**:“Requisiti”,”Progetto”,”Codifica”,”testing”,”Prodotto”. (Ad ogni step può essere assegnata una persona diversa in base alle sue capacità) Ogni step produce un “semilavorato” che viene poi consegnato allo step successivo. è **`Document based`** fa uso cioè di un documento per il trasferimento delle informazioni che viene creato ad ogni terminazione di fase, ciò permette a chi ha finito di lavorare nella sua fase di poter procedere ad altri lavori non essendo più necessario. La linearità inoltre permette di **`pianificare i tempi`** stimando la durata di ogni fase, questa stima è però, come la linearità, a senso unico: non possiamo ridurre il tempo speso e dovremo assorbire eventuali ritardi. Le principali criticità sono:
        - `Fase di manutenzione assente`: essendo a senso unico non possiamo tornare indietro, nonostante siamo a conoscenza che ogni software è destinato ad evolversi e cambiare; gli unici aggiornamenti possibili sono piccole patch che però disallineano solamente la documentazione precedente, è comunque la fase in cui ricadono la maggior parte dei costi di sviluppo.
        - `Rigidità`: Stima dei costi e valutazione dei rischi vengono fatti all’inizio e non quando ho capito bene il problema, resto così rigido congelando i sotto-prodotti e perdendo la flessibilità richiesta.
        - `Monoliticità`: poiché la pianificazione è orientata ad un singolo rilascio, ciò però ci porta ad un aumento dei costi e a sforare i tempi di consegna. (contraddice quindi la realizzazione di un software modificabile ed evolubile, inoltre la manutenzione viene fatta solo sul codice)
        
        ![Screenshot 2024-10-15 alle 10.33.04.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/c49c1dd1-1782-40bf-81c2-2394e02f982f/Screenshot_2024-10-15_alle_10.33.04.png)
        
    - **Modello a V (dente di pesce cane):** una delle varianti del modello a cascata, introduce una più estesa fase di testing. Nonostante sia sempre un modello sequenziale presenta dei nuovi legami tra le fasi di sviluppo corrispondenti alle attività di verifica e convalida. Va ad accentuare il rapporto con il cliente, coinvolto con la richiesta di feedback per ciascun sottoprodotto generato. Le nuove attività introdotte sono definite quindi come:
        - `verifica`: va a controllare la correttezza rispetto alla descrizione formale delle specifiche;
        - `convalidazione`: controlla, attraverso un feedback continuo, la compatibilità con le esigenze del cliente.
        
        ![Screenshot 2024-10-15 alle 10.36.22.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/43851789-7dab-404d-bcc4-44b6b38a3837/Screenshot_2024-10-15_alle_10.36.22.png)
        
- **Modelli iterativi**: ottenuto sapendo che la sequenzialità stringente delle fasi rappresenta un grosso limite, si pensa di far ripetere alcune fasi più di una volta con dei cicli fino all’ottenimento di un prodotto worth.
    - **Modello a cascata con singola retroazione:** Come il modello a cascata ma presenta una fase di testing e permette agli sviluppatori di poter ritornare al passo precedente, arrivati però al prodotto non possiamo tornare indietro per la manutenzione e l’introduzione stessa di un’iterazione renderebbe molto difficile la pianificazione del lavoro e il monitoraggio dell’avanzamento. Un’altra criticità è la possibilità di avere un problema non nel punto precedente ma direttamente all’inizio (**Condiviso da molti modelli iterativi**)
        
        ![Screenshot 2024-10-15 alle 10.42.04.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/e5fd0f8d-657f-4bd5-b862-b7983aba0761/Screenshot_2024-10-15_alle_10.42.04.png)
        
- **Modello prototipale:**  Si divide in pubblico e privato, lo creo per parlare con il cliente, per far vedere al cliente il funzionamento (grezzo) del software, permette di ridurre significativamente i requisiti e errori di design soprattutto riguardanti l’interfaccia utente:
    - Il `modello pubblico` viene mostrato al cliente, comporta dei rischi nella futura gestione del codice poiché può portare il cliente a richiedere nuove funzioni, ci permette di far compiere scelte all’utente; `non sto consegnando il progetto ma lo sto mostrando`;
    - Il `modello privato`, detto “spike”, è utile per testare nuove tecnologie o linguaggi e programmare soluzioni per i problemi più difficili, permettendo di comprenderlo meglio (”do it twice”) (per la legge di Bohem la prototipizzazione riduce notevolmente gli errori dei requisiti e di design, soprattutto nelle interfacce utente)

- **Modelli incrementali:** Permette di affrontare e limitare i rischi di consegna, riducendo i fallimenti,  si parla di incrementale quando nelle iterazioni viene inclusa la consegna. è più appropriato parlare infatti di `Implementazione Iterativa`, che stressa la modularizzazione e l’identificazione di sottosistemi e nel quale si ripetono fasi di coding ed integrazione, e `Sviluppo incrementale`, che viene esteso a tutte le fasi.
    
    `Caratteristiche`: 
    
    - Complicato il lavoro di planning, stato del processo meno visibile e dobbiamo pianificare tutte le iterazioni
    - Si riconosce che bisogna rimettere mano a ciò che si è fatto
    - Cosa è una iterazione, quanto dura?
        - rischio di troppe iterazioni
        - rischio di overhead causato dalle troppe iterazioni
        - rischio di eccessivo overlapping
            - non abbiamo tempo di avere feedback dall’utente.
    
    - **Modello a fontana**: nel modello a fontana, in caso di problemi si riparte dal primo passaggio (ovvero la definizione dei requisiti)  senza però andare ad eliminare il lavoro svolto. Cerco infatti il punto più “indietro” che viene influenzato dal problema, così da poterlo correggere, in questo modello non congeliamo il prodotto in uso (che può provocare problemi) ma lo lascio lavorare permettendomi di arrivare ad una eventuale manutenzione o evoluzione dello stesso.
    - **modello a flipper**: è un processo non definito, può essere svolto qualunque passo, è un modello creato come critica ai modelli incrementali.
    
- **Modelli trasformazionali**: cercano di mantenere sotto controllo tutti i passi e i procedimenti in modo formale; partendo da specifiche spiegate in modo informale (dal cliente) otteniamo come risultato un prototipo che differisce per efficienza e completezza dal prodotto finale, inoltre tali passi devono essere dimostrabili formalmente come corretti. In caso il passo non fosse corretto, ovvero nel caso arrivassi ad un vicolo cieco, posso tornare un passo indietro scegliendo una nuova strada.
    - **MetaModello a spirale**: non è propriamente un modello bensì un framework in cui possono essere inquadrati altri modelli. è di tipo incrementale ed è guidato da un’analisi dei rischi, ovvero su cosa possiamo fare in caso di un certo rischio
        - **Variante Win-WIn**: questa variante prende in considerazione anche i rischi contrattuali che possono esserci con i clienti, problemi quindi di comunicazione che necessitano di contrattazioni e negoziazione. Entrambe le parti, quindi, vincono attraverso questa variante.
    - **Modello COTS (Component Off The Shelf)**: si parte dalla disponibilità interna o sul mercato di moduli preesistenti, non riusciremo a creare un progetto formato solo da moduli preesistenti ma ciò ci permette di di non dover partire perforza da zero. Dobbiamo però basarci su altre attività (vedi appunti corso).

- Modelli agili: (Ci si concentra sull’extreme programming)
    
    I requisiti diventano volatili, possiamo gestirlo, infatti il cliente può cambiare sempre idea
    
    - **Modello Lean Waste:** nata dalla lean manufactoring di Toyota. Si basa sulla riduzione di sprechi e di cose inutili.
    - **Modello Kanban:** basato su una lavagna con diverse colonne: “to-do”, “in progress”,” testing” e “done” nelle quali andiamo ad inserire le varie parti del progetto, in done metteremo ciò che è stato completato, che ha passato i test e che è stato valutato e accettato dal cliente. Per Kanban noi dobbiamo andare a minimizzare il “work in progress”.
    - **Scrum:** Approccio simile al win-win, il cliente può aggiungere o togliere delle richieste ma dopo una certa scadenza (due settimane) sposto ciò che è stato richiesto nella seconda colonna dove rimane congelata.
    - **Crystal:** Si basa sulla comunicazione osmotica la conoscenza cioè viene sparsa a tutto il team, ovvero viene condiviso ciò su cui si ha lavorato per evitare eventuali “blocchi” del lavoro causati da imprevisti verso uno o più elementi del gruppo.

## eXtreme Programming (XP)

Si basa sul TDD (test driven development), vado cioè a creare prima un test che possa verificare la correttezza dell’idea, dopo aver creato il test da cui partire evolveremo per baby-steps, ovvero tramite piccole porzioni, andando a testare questi e ad ottenere così un feedback istantaneo.

Mantra del TDD è (rosso, verde,refactoring):

- write a failing test
- make it pass
- refactor

Variabili in gioco:

- Portata: ovvero la quantità di funzionalità che si vogliono implementare;
- Tempo: ovvero il tempo che ho a disposizione per terminare il progetto;
- Qualità: ovvero la qualità del progetto che si deve ottenere;
- Costo: Le risorse finanziarie che si possono impegnare nel progetto;

Principi:

| XP | Ing SW “classica” |
| --- | --- |
| Feedback rapido | Separazione degli interessi |
| presumere la semplicità | Astrazione e modularità |
| Accettare il cambiamento | anticipazione del cambiamento |
| Modifica incrementale | generalità |
| Lavoro di qualità | incrementalità |

## Figure in gioco e responsabilità

Il manager/cliente ha la responsabilità di decidere portata, priorità tra funzioni e date dei rilasci mentre ha il diritto di sapere cosa può essere fatto, di vedere i progressi nel sistema e i cambiare idea.

Lo sviluppatore deve stimare i tempi per le singole funzionalità, le conseguenze delle scelte tecnologiche e una pianificazione dettagliata, ha il diritto di sapere cosa è necessario attraverso requisiti chiari, cambiare le stime dei tempi con esperienza, identificare e indicare le funzionalità pericolose ed infine produrre software di qualità

## Raggruppare per fasi

- Requirements:
    - Gli utenti fanno parte del team di sviluppo
    - Consegne incrementali e pianificazioni continue, non posso quindi raccogliere tutto insieme ma in modo continuo e incrementale
- Design:
    - metafora come visione unificante del progetto;
    - Refactoring, ripensare quindi a come cambiare il design
    - presume la semplicità
- **Code**:
    - *programmazione a coppie*;
    - *proprietà collettiva*;
    - *integrazione continua*;
    - *standard di codifica*.
- **Test**
    - *test di unità* continuo (da scriversi prima del codice);
    - *test funzionale* scritto dagli utenti nelle user stories

## Documentazione

La documentazione cartacea non è necessaria.

## Quando non possiamo usare xp?

In ambienti che impediscono l’uso di anche un solo approccio utilizzato,

- Barriere tecnologiche che impediscono di testare il sistema in condizioni reali e di avere feedback in modo rapido;
- Barriere di tipo manageriale o burocratico, quindi team troppo numerosi e la necessità di documentazioni per certificazioni basate su di essa.
- barriere di tipo fisico, ovvero che non permettono flessibilità nella formazione delle coppie di lavoro

## Mesi-uomo

Il rapporto tra numero di persone che lavorano e tempo si pensa essere proporzionale, ovvero all’aumento del numero di persone diminuisce il tempo che esse devono impiegare per programmare i loro pezzo di codice, ovviamente ciò è sbagliato a causa dell’**overhead** che va ad impedire una corretta comunicazione impattando la gestione dei ritardi.

## Strumenti di supporto

Vanno dalla comunicazione: quindi internet o forum, alla sincronizzazione del lavoro e versioning fino all’automazione della build e al bug tracking.

## Source Code Management (SCM): scenari

- Gestisce il luogo in cui vengono messi i progetti in fase di evoluzione, permettendo di andare a cercare e risolvere eventuali errori gravi, richiamando e mettendo in confronto versioni diverse

## Cosa tracciare?

Dobbiamo prima di tutto rispondere alle domande:

- Si traccia l’evoluzione anche di componenti fuori dal nostro controllo?
- Si archiviano i file che costituiscono il prodotto?

E la risposta è no, poiché risulta costoso sia in tempo che in spazio e risulta anche poco pratico.

### Meccanismo di base

ogni cambiamento è regolato da:

- check-out, ottenere una versione già presente
- check-in(commit), registrare nuova versione

La repo mantiene informazioni comprese date, etichette versioni e diramazioni, può salvare solo le differenze tra una versione e l’altra.

Quando è condiviso da un gruppo di lavoro nasce il problema di gestirne l’accesso concorrente:

- modello “pessimistico” (RCS): la gestione degli accessi agli artifact viene fatta in mutua esclusione, attivando un lock (la durata deve essere piccola) al check-out. (previene)
- Modello “ottimistico” (CVS): il sistema si disinteressa del problema, andando a fornire supporto per le attività di merge di change-set paralleli in conflitto (sistema), questo modello è parzialmente regolabile tramite branch, le varie diramazioni vengono unite (merge) andando a confrontare le differenze.

## SCM distribuito

I vantaggi di sfruttare i sistemi Software Configuration Management sono differenti:

- posso lavorare offline, facendo commit senza rete, posso poi aggiornare il repo appena avrò una connessione.
- Lavoro veloce, non rallentato dai tempi del commit grazie alla presenza di un repo locale.
- Supporta diversi modi di lavorare:
    - simil centralizzato: si considera un repository come riferimento
    - i peer che collaborano direttamente
    - gerarchico a più livelli

Quando un oggetto viene salvato, si calcola l’hash dello stesso oggetto che viene salvato insieme ad esso.

I tipi di oggetti possono essere:

- Blob, una massa informe di dati  (file compresso).
- Tree, blocco che indica una directory
- commit, contiene le meta informazioni di quel blob

posso usare git commit —amend per  sostituire l’ultimo commit effettuato, quello vecchio viene eliminato dal garbage collector.

Spesso facendo git merge possono verificarsi dei conflitti quando la stessa zona di codice (chunks) viene modificata da più utenti, o abbiamo dei merge con codici uguali o quando sono tutti e tre diversi.

git reset che parte dal local repo, aggiorna e sovrascrive gli index con quello che c’è nel commit più recente

## Branch

Creare dei branch è praticamente obbligatorio, quando cloniamo siamo già in presenza di due branch: Main e remote main.

La prima branch non vale come main effettivo, infatti il vero e proprio “main” sarà quello su cui verrà eseguito il primo commit; i branch si usano soprattutto in un workflow molto grande.

## Gitflow

Inizializzo con `git flow init`.

Differenzia i vari rami dando loro, in base alla diversa categoria, comandi differenti.

I rami principali sono `Master`e`Develop`, il primo contiene le versioni stabili, develop invece è il ramo di integrazione, nel quale il codice viene modificato prima del rilascio di una versione stabile.

Altri rami sono:

- `Feature` : un ramo non infinito, viene creato per ogni funzionalità nuova che voglio sviluppare, quando penso di aver terminato lo sviluppo di tale feature mi sposto nel ramo develop. La feature deve partire dall’ultima versione stabile che è partita dal develop. Non posso aprire feature con lo stesso nome.
    
    Il comando `git flow feature start <nome_feature>` corrisponde a:
    
    ```latex
    git checkout develop
    git branch <feature>
    git checkout <feature>
    ```
    
    Il comando `git flow feature finish <nome_feature>` corrisponde a:
    
    ```latex
    git checkout develop
    git merge --no-ff feat1 (--no-ff vuol dire "ti obbligo a fare il merge anche in caso di fast forward(avviene in mancanza di altri commit)")
    git branch -d feat1
    ```
    
- `Release`: Congelo le feature che dovranno esserci nella prossima release, quando faccio una release (beta) vado a riparare, chiedendo ai beta tester dei feedback.
    
    Avvio utilizzando `git flow release start ver`che corrisponde a
    
    ```latex
    git checkout -b ver develop
    ```
    
    mentre termino con `git flow release finish ver`:
    
    ```latex
    git checkout master
    git merge --no-ff release-ver
    git tag -a ver
    git checkout develop
    git merge --no-ff release-ver
    git branch -d release-ver
    ```
    
- `Hotfix`: creato in caso di problemi importanti (crash o grandi problemi di sicurezza).
    
    Si apre con `git flow hotfix start ver`:
    
    ```latex
    git checkout -b ver master
    ```
    
    si chiude con `git flow hotfix finish ver`:
    
    ```latex
    git checkout master
    git merge --no-ff ver
    git tag -a ver
    git checkout develop
    git merge --no-ff ver
    git branch -d ver
    ```
    
- `Support`: aperto quando devo fixare dei bug in una versione vecchia del software senza andare ad intaccare la nuova versione (ad esempio viene presentato un bug della versione 1.1 ma siamo già alla v2.0).
    

### Git request-pull

### Fork

Va a risolvere il problema delle autorizzazioni

## Gerrit

Progettato da google, è un sistema di review del codice sviluppato internamente a google utilizzato per la gestione di progetti open source troppo grandi come android.

### Verifier: Verifying a chance

Uno strumento o processo utilizzato in Gerrit per verificare che le modifiche proposte siano corrette e funzionino come dovrebbero.

### Approver

Successivamente alla verifica di una proposta di modifica questa deve essere anche approvata

### Build automation

Per proteggersi da checkin di una versione non funzionante possiamo automatizzare la ricompilazione e il testing

### Make
