
# Reti di calcolatori



Requisiti rete:

- prestazioni
- affidabilità, attraverso TCP → pezzo di software più diffuso sul pianeta
- sicurezza
- indirizzamento, protocollo Ip
- instradamento (routing)

Le regole necessarie non sono necessariamente delegate alla rete, una parte sono della rete una parte mia.

messaggio: coda input —> router (viene analizzato) —> output

L’unica parte software è la popolazione ella tabella, il resto viene svolto via hardware.

Frammento in pacchetti (unità dati di dimensione massima fissata) l’unità dati dell’utente che viene poi riassemblata.

L' **Instradamento** è la capacità di un nodo di trovare la strada verso un altro nodo
L'affidabilità deve garantire:
- completezza, devono arrivare tutti i frame.
- ordine, i frammenti devono arrivare in ordine.
- non duplicità, non devo avere copie.


### Routing
 
Trovare la migliore strada per arrivare a destinazione in un certo istante di tempo

Tabella sulla quale si basa il processo di routing.

Una grande unità dati viene frammentata in tanti pacchetti quanti ne servono per poter far passare tutta l’unità senza incorrere in un overflow.

origine: frammento → destinazione assemblo
Tra frammento singolo e file si perde, per questo il tempo e la possibilità di arrivo dei pacchetti può variare.

## Commutazione

- Commutazione di un messaggio
- Commutazione di un pacchetto

Con commutazione si intende la scelta di un percorso per spedire un messaggio da un mittente ad un destinatario.

I dati da trasmettere vengono decorati con:

- un’intestazione iniziale (che identifica mittente e destinatario, header)
- una coda che funge da codice rilevatore di errore
- possibili altre informazioni tipo il protocollo usato

La commutazione si definisce con affidabilità ed efficienza:

- efficienza: basata soprattutto sul **Packet error rate $p_{er} = 1-(1-b_{er})^{n} = n•b_{er}$**

## Internet

tutte le reti del pianeta connesse ad internet sfruttano l’**IP** Internet Protocol.

Ogni rete appartenente all’internet usa tecniche diverse di instradamento e usa o può usare tecniche diverse per fare routing.

Le reti a virtual circuit (circuito virtuale) sono reti affidabili poiché mantengono il traffico su un unico percorso

La validazione di avvenuta ricezione avviene attraverso l’**ACK (acknowledgment)**
Grazie a questo posso anche decidere un tempo t utile.

**Jitter:** varianza sul ritardo in rete

Per calcolare la velocità del traffico su rete useremo:

$$ T = t_{x}+2t_{p} $$
Dove tx è il tempo di trasmissione, $t_{p}$ tempo di propagazione.
$$t_x = \frac{l}{ck} $$
Dove $l=lunghezza\space frame$ e $c=velocità\space della \space luce$
$$t_p=\frac{l_{cavo}}{c}$$
Ovviamente T non è esattamente uguale al valore dato ma leggermente più grande.
Il tempo di trasmissione funzione della velocità della trasmissione, quindi alla velocità del clock, è uguale alla dimensione del pacchetto/il bitrate dello stesso.

Il tempo di propagazione invece è dato dal rapporto tra distanza e velocità del canale

## Host

l’host è una macchina che ospita i processi comunicanti su rete, possiamo avere host sorgente e host destinazione.

### Protocollo

L’implementazione di uno specifico protocollo gestisce le regole in base alle quali due macchine comunicano all’interno di una rete. è diviso in diversi livelli, il livello di base è quello **fisico** (ovvero un cavo o fibra ottica) che permette la connessione tra macchine, il livello due è il **Data Link** un livello che contiene tutte le regole per operare su un singolo link; il terzo livello è il **Network** permette l’instradamento conoscendo la topologia della rete magliata, la non conoscenza o la conoscenza parziale porterebbe ad altri risultati.

Sono presenti inoltre altri livelli ovvero il **trasporto**, la **sessione**(deprecato), la **presentazione**(deprecato) e l’**applicazione**.

Al livello 4 è messa l’affidabilità, questo è reso possibile grazie a tcp e udp, la prima si occupa della comunicazione affidabile mentre alla seconda non importa nulla del canale affidabile.

### Livelli ISO/OSI

**Datalink**

Si occupa del collegamento tra due nodi, il payload viene “incapsulato” tra un header(stx) e una tail(ETX) (formati da bit), questa capsula è detta frame.

Possiamo utilizzare il bit stuffing, questo garantisce che all’interno del payload non ci sia una sequenza uguale alla tail. Si occupa infatti di inserire un bit nei dati in modo da renderlo diverso sia da header che da tail, semplicemente si controlla quanti 1 consecutivi sono presenti in header e tail, nei dati appena trova una sequenza di 1 lunga n-1 va ad inserire uno 0 per renderla diversa.

### `Broadcast(AI)`

Il broadcast è un metodo di trasmissione dati in cui un nodo invia un messaggio a tutti gli altri nodi della rete contemporaneamente. Questo tipo di comunicazione è particolarmente utile quando si deve inviare la stessa informazione a tutti i dispositivi connessi.

Caratteristiche principali del broadcast:

- Efficienza nella distribuzione di informazioni a larga scala
- Utilizzo in protocolli di rete come ARP (Address Resolution Protocol)
- Potenziale sovraccarico della rete se usato eccessivamente
- Limitato generalmente al dominio di broadcast locale per evitare congestioni

Il broadcast è ampiamente utilizzato nelle reti locali (LAN) ma è generalmente limitato o evitato nelle reti più ampie come Internet per ragioni di efficienza e sicurezza.

## `CSMA/CD(AI)`

CSMA/CD (Carrier Sense Multiple Access with Collision Detection) è un protocollo di accesso al mezzo utilizzato nelle reti Ethernet per gestire l'accesso condiviso al canale di comunicazione. Ecco i punti chiave:

- `Carrier Sense`: i dispositivi ascoltano il canale prima di trasmettere, finché non trovano il canale libero non trasmettono
- `Multiple Access`: più dispositivi possono accedere allo stesso mezzo di trasmissione
- `Collision Detection`: i dispositivi sono in grado di rilevare le collisioni durante la trasmissione

Funzionamento:

- Se il canale è libero, il dispositivo inizia a trasmettere
- Se si rileva una collisione, la trasmissione viene interrotta
- Dopo una collisione, i dispositivi attendono un tempo casuale prima di ritentare

CSMA/CD è fondamentale per l'efficienza delle reti Ethernet, permettendo l'utilizzo ottimale del mezzo condiviso e riducendo le probabilità di collisioni ripetute.

L’intervallo di tempo randomico per trasmettere è determinato dall’algoritmo BEB (Binary Exponential back-off)

64 B è la dimensione minima di una frame ethernet

## Domini di collisione
Possiamo utilizzarli al posto dei semplici cavi, e presentano i seguenti componenti:
- ### `Hub`
	è un dispositivo di livello 1 passivo.
	un hub è un centro stella passivo (non presenta `Carrier Sense` o ` Collision Detection`) di livello fisico che riceve e ritrasmette il segnale; va a modellare il comportamento del **BUS** ed è realizzabile su più livelli. La frame entra nell'hub che la propaga ai client i quali rispondono con una frame a loro volta. 
	Sull'hub dobbiamo contare come lunghezza sia l'invio che il ritorno della frame.

- ### `Bridge`
	è un dispositivo classificato a livello 2 (opera a livello `Mac`) e opera attraverso `forwarding`, andando a separare i domini di collisione a cui è collegato.
	il livello 2 locale è molto simile a quello di rete.
	La tabella di forwarding opera in questo modo: la tabella è inizialmente vuota e quando arriva un frame da A il bridge salva da quale porta del bridge il frame di A è arrivato, successivamente instrada il frame verso B in base alla sua porta:
	- se la porta di B non è nota il frame viene inoltrato a tutte le porte tranne ad A (ciò è detto `flooding`)
	- se la porta di B è nota ed è la stessa di A il frame non sarà inoltrato (sarà già arrivato poiché nello stesso dominio di collisione)
	- se la porta di B è nota ma non appartiene allo stesso dominio di collisione di A allora il frame viene inoltrato nella porta del dominio di B
	- alla risposta di B si ricomincia.
	La tabella dopo un certo periodo viene resettata e ricostruita, in modo da tenerla aggiornata.

- ### `Switch`
	è un apparato che ammette connessioni senza richiedere particolari vincoli sulla distanza, in base a ciò che viene detto dalla tabella di forwarding si sceglie cosa fare.
	Possiamo dire che sia un bridge per la funzione di forwarding ma è differenziato ad esso poiché le connessioni con i client sono `Punto a Punto` e quindi non ci sarà più carrier sense e non avremo più il vincolo $u_t > t_p$
 $$
	 U =\frac{1}{1+\frac{2B}{cF}}
	 $$


## Reti Virtuali
Le stazioni vengono raggruppate di solito dagli amministratori in base al settore.

#### Standard Vlan


#### LLC sublayer
Logical Link Control, mentre il MAC layer permette la connessione, questo permette di controllare l'invio del frame, scegliendo il ricevente.
Presenta due proposte di protocollo: 
- Affidabile (non usato)
- Non affidabile

## Livello Network

Questo è il livello 3, si occupa dell' **Instradamento** de dell' **Indirizzamento** che, come già visto, servono rispettamente di come instradare un pacchetto tra sottoreti diverse e dell'identificazione univoca di un nodo in una sottorete.


#### Ip
protocollo che si occupa dell'adressing
l'header di un IP è di 20 byte

#### Routing
Protocollo per fare Routing

#### ICMP

#### ARP - RARP
Risolviamo l'indirizzo IP nell'indirizzo MAC locale

Gli Indirizzi IP sono divisi in diverse categorie ma principalmente abbia:
- indirizzi multicast/broadcast: Classe D
- indirizzi punto-punto, queste ultime si dividono in:
	- Classe A, primo bit è 0
	- Classe B, primo bit è un 1 (classe A quindi non è), utilizziamo un secondo bit (qua = 0)
	- Classe C, Primo bit è 1 secondo è 1 terzo è 0 e così via fino alla classe  E
	- Classe D, Multicast
	- Classe E
	La differenza tra questi si ha da A -> C, infatti scendendo di classe diminuirà la quantità di hostId presenti, meno HostId = molti più NetId presenti in rete.
Problema di queste classi è lo spreco che si andrebbe ad ottenere a causa della staticità dei blocchi.
Ci sono due modi per andare a risolvere questo problema:[[
]]1. organizzativo tramite **_Subnetting_**, va ad eliminare totalmente l'idea di organizzazione iniziale
2. Operativo:
	1. **_NAT_**
	2. **_CIDR_**: (Class-Less Intern Domain Routing)


## Subnetting [Standard RFC 950]
Andiamo ad introdurre un ulteriore livello di gerarchia per indirizzare le sottoreti, l'admin di rete va quindi a dividere la rete in `SubnetId` e `HostId`, vado poi a codificare il tutto come standard RFC 950. SubnetId e HostId non sono definiti tramite stack li va invece a definire l'admin di sistema, non possiamo quindi conoscere la suddivisione di bit, poiché conosciuta solo dall'admin che può a sua volta modificare a suo piacimento.
#### Come risolviamo?
l'admin decide di fare subnetting e trova comodo la suddivisione 6 bit (subnet) 10 bit (host)
Utilizziamo quindi la maschera di sottorete (subnet mask), ogni router non ha solo una entry con ip address da indirizzare ma anche la maschera di subnetting.  La maschera è formata da 6 bit di 1 (subnetID) e 10 bit di 0 (hostId), andando a fare un and tra maschera di rete e IP otteniamo il valore dei bit di subnet che indicherà il numero della  sottorete da indirizzare.
Una `/22` è una sottorete avente 22 bit.

##### CIDR
Milano: 194.24.0._ -> 194.24.7._ ha segnato 2048 indirizzi

##### NAT {RFC 3022}
La rete presenta un IP privato e un IP pubblico.
L'indirizzo pubblico è quello che viene utilizzato, necessitiamo quindi di qualcosa che possa trasformare un IP pubblico in privato e viceversa; entra quindi in gioco il nat che si frappone tra internet privato e pubblico (unico).
