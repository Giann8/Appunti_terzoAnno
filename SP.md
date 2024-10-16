## SP - L1

Script kiddie: prendono script online senza conoscerne il funzionamento (cracker piccoli)

**Computer Security:**

- individuare gli strumenti per poter garantire le proprietà di **Integrità, Confidenzialità e Accessibilità.**

**Confidenzialità**: un sistema è in grado di garantire la confidenzialità quando preserva le informazioni mantenendo certe restrizioni verso altre persone.

**Integrità:** il sistema è in grado di garantire l’integrità quando non permette di eliminare o modificare il contenuto di un file da parte di qualcun altro.

**Accessibilità:** Garantisce il funzionamento nonostante ciò che può accadere.

**Confidenzialità**: può essere violata quando si fa una copia non autorizzata di un software.

Un asset può essere sempre compromesso, seppur con maggiore difficoltà.

**Vulnerabilità:**debolezza di un sistema

**Threat:**(minaccia) qualunque circostanza che ha il potenziale di causare un danno.

**Controlli:** Misure per ridurre i danni possibili.

Attacco: sfruttamento di una o più vulnerabilità da parte di una minaccia, dove definiamo con **Exploit** il metodo di sfruttamento.

Gli attacchi possono essere:

**Passivi:** il sistema non viene modificato (intercettazione), non possiamo quindi accorgercene, obiettivo è la raccolta di informazioni.

**Attivi:** Possono essere rilevati poiché serve per danneggiare le infrastrutture.

Le contromisure:

Possono prevenire(se avviene un attacco si cerca di evitare che accada di nuovo), individuare(si cerca di accorgersi dell’attacco in corso, segnalando così la presenza di un attacco), e recover(in caso non si riuscissero ad utilizzare le prime due allora si cercherà di ripristinare il prima possibile la macchina allo stato di funzionamento iniziale).

il ransomware non si può prevenire, non sempre si rileva.

Disclosure: Un evento o circostanza nel quale un’ntità ottiene accesso a dati per cui non ha autorizzazioni ( **esposizione:**  dati sensibili inviati direttamente all’entità non autorizzata, **Intercettazione: Man in the middle è una prova,** **l’entità ottiene i dati che vengono inviati da una fonte ad un’altra, Inference:** I dati vengono ottenuti dall0entità attraverso una comunicazione che non per forza contiene tali dati, **Intrusion:** un’entità ottiene i dati a cui non ha accesso aggirando i sistemi di sicurezza)

Deception. Un’entità autorizzata riceve dati falsi credendo siano veritieri (**Mascheramento:** un’entità non autorizzata ottiene accesso ad un sistema o svolge un’azione malevola fingendosi un utente autorizzato;  **Falsificazione** dei dati; **RIpudio:** viene falsamente negata da parte di un’entità malevola la sua partecipazione ad un azione non autorizzata)

Disruption (viene interrotto o modificato il corretto funzionamento di un sistema di servizi o funzioni (**Incapacitazione: disabilitato un componente del sistema; Corruzione:** vengono modificate le funzioni di sistema attraverso la modifica di dati o funzioni; Ostruzione: un’azione malevola attuata per bloccare la corretta funzionalità di un servizio ostruendo un’operazione di sistema (ddos))

Usurpation: l’entità non autorizzata ottiene accesso ad un sistema (appropriazione indebita: viene ottenuto accesso non autorizzato logico o fisico di un sistema; Misuse: un componente di sistema presenta un errore che può rendere critica la sicurezza del sistema)

Superficie di attacco, insieme delle vulnerabilità di un sistema. Bisogna quindi ridurre la superficie di attacco che può essere a livello rete, software e hardware.

La parte più vulnerabile è però quella umana

Implementazione

Assicurazione e valutazione, fasi che avvengono dopo la verifica del sistema per valutarne la qualità così da poterlo poi verificare formalmente.

Ci sono standard di sicurezza internazionali (NIST- Nationale Institute of Standard Tecnology, rilascia lo standard NIST800 cui controparte globale è l’ISO international organization for standardization, che rilascia l’ISO-27k)

## SP-l2

Sistema operativo di riferimento: linux(unix)

il sistema operativo è un programma fondamentale per l’uso di un calcolatore

all’accensione del computer il so presente prende il controllo

Insieme ad un sistema operativo troviamo la libreria delle syscall, le system utility (programmi forniti insieme al so che permettono il funzionamento e la cancellazione di alcuni programmi)

Linux è un derivato di Unix, nato alla fine degli anni ‘60 da un progetto per il primo sistema operativo multitasking chiamato **MULTICS** 

Il progetto fallì rimanendo però pietra miliare per altri sistemi operativi.

Il processo è l’insieme delle attività da svolgere a cui vengono allocate delle risorse

il codice eseguibile viene allocato nella memoria, lo spazio è allocato per le variabili dinamiche, uno stack è allocato per memorizzare le variabili dinamiche (terminate il loro uso vengono cancellate)

in caso più processi venissero avviati insieme si avrebbe un segnale di interrupt che porterebbe al termine alcuni processi dopo un certo numero di cicli clock.

L’interrupt è un segnale a due bit 01.

la system call fork() crea una copia del processo chiamato, viene duplicato, si avrà quindi il processo A e il processo generato detto (child), una copia esatta di A con la sola differenza nel pid (process identifier)

fork restituisce :

- -1 al processo genitore
- 0 al processo figlio

```c
#include <stdio.h>
#include <unistd.h>

int main(void){
pid_t x;
x=fork();
if (x==0)
	printf("In child:fork() returned %Id\n",(long)x);
else
	printf("In parent:fork() returned %Id\n",(long)x);
}
```

```c
pid_t childpid=0;
for(i=1;i<n;i++)
	if (fork()!=0) kill;
```

Il processo padre genera un figlio dopodiché si killa, il processo figlio con i+1 genera un figlio e si killa così via per ogni figlio generato.

```c
pid_t childpid=0;
for(i=1;i<n;i++)
	if (fork()==0) kill;
```

Il processo padre genera un processo figlio e lo killa.

Al termine di un processo tutti i file vengono chiusi, i processi figli deallocati e la memoria liberata.

il genitore conosce i pid di ogni figlio quindi può scegliere a quale figlio terminare (con NULL si termina al primo).

Un processo è detto fantasma se non ha informazione (solo PCD).

Tutti i processi sono definiti da un numero (il PID). i processi in linux possono operare in fg(foreground) e bg(background) 

I comandi i bg possono avere come suffisso ‘&’ per poter essere avviati dalla linea di comando in modo autonomo.

si possono visualizzare i processi con ps e tutti i processi in esecuzione si aggiunge -fae

con la pipe (’|’) si possono mettere processi che vengono eseguiti di conseguenza attraverso l’output del precedente.

```bash
$ cat zoo.text|grep "animals" //cerca tutte le righe con "animals" all'interno
```

con >> si va ad aggiungere ad un contenuto già presente

con < si usa lo standard input

## SP-l3

File system 

Struttura dati per la gestione, allocamento e organizzazione dei file 

Drive

Cartelle

Le directory hanno diversi figli e solo un padre (struttura ad albero)

i file system possono essere rappresentati graficamente o con l’interfaccia testuale

Il percorso può essere assoluto, se direttamente collegato al root, o relativo

Ad ogni file il file system associa dei metadati per la loro identificazione

/ root

. corrente

..principale

tool find

```bash
$ find directory -name targetfile -print
$ locate .txt
$ which ps
```

which ps otteniamo il percorso assoluto dell’eseguibile

locate .txt

Struttura dati dinamica

lista→ arraylist, meglio utilizzare linked list

accesso nell’arraylist più rapido mentre nella linked devo cercare tra tutti gli elementi

la rimozione 

“l’sshkey quando cambia?”

Per essere più sicuro il sistema operativo utilizza un metodo di controllo degli accessi, che permette solo ad alcuni utenti di poter modificare o anche solo leggere un certo file.(Regole auree)

- meccanismi di autenticazione: verifica dell’identità di chi lo sta usando;
- meccanismi di accesso;
- meccanismi di decisione della guardia, per poter capire come e perché si è verificato un certo problema.

- Controllo degli accessi
    - Soggetto:umano o processi in corso su parte dell’attività generale dello user
    - Oggetto:risorse (I/O)
    - Operazioni di accesso

Il sistema cerca di capire che cosa sta succedendo e l’utente decide cosa fare.

Regole alla base:

Deve essere presente una security policy.

**ITU-T Raccomandation x.800 defines access controll.**

Previene l’uso non autorizzato di una certa risorsa e previene un uso improprio della risorsa

Esistono diverse tipologie di accesso a controllo:

- Politica DIscrezionale: è il proprietario a decidere chi può accedere e cosa si può fare su questo file.
- Mandatory access control: la politica viene decisa non da un’ entità superiore rispetto a chi crea il file , la policy viene decisa dalla macchina, dal sysadmin o dall’app developer.
- Politica a ruoli, fusione dei due.

Il tutto si ritrova in una matrice con i vari soggetti, soluzione per la matrice, :

- RIduciamo il numero di colonne, ogni colonna è relativa ad un oggetto, bisogna memorizzare il nome di ogni oggetto
- Access control list contiene gli user a cui è permesso accedere al sistema e i rispettivi permessi
- **I-node: struttura dati presente in un hard disk che contiene i metadati relativi ai file.**

In unix tutto è un file.

I token(capability), vengono creati da windows per registrare l’accesso. Contiene un codice identificativo dello user, dei

kernel

ACL: 
Authentication: la banca si fa carico di chi accede alle cassette di sicurezza

Bank’s involvement: la banca deve custodire la lista e verificare gli users

Forging access right: the key cannot be forged

Adding a new person: L’owner può aggiungere una nuova persona al gruppo dandogli la chiave

Delega: un amico può estendere i suoi privilegi a un suo amico/a

Revoca

per capire chi può accedere al file devo controllare le capability di tutte le persone

Windows:50/60millioni

Linux:30milioni

Reference monitor: viene invocato e valida ogni accesso ad una risorsa, ogni volta che un processo chiede l’accesso ad una risorsa la chiamata viene convertita in un accesso co reference monitor che decide se far accedere o no

cosa è contenuto in /etc/passwd file:

UID: numero di 16 bit che identifica ogni utente (lo 0 è superuser)

il superuser non può conoscere la password che abbiamo scelto ma la può cambiare.

L’obiettivo di un attacco è quindi quello di ottenere l’UID 0

in etc/group contains 

```java
usermod -a -G groupname username
```

I processi hanno un UID e un GID associati a loro

- real è ereditato dal processo figlio
- effective da padre o da un file che inizia ad essere eseguito

ls viene eseguito, se il comando è corretto viene fatta una fork()

if (pid==0) execve (/bin/ls)

execve → è una systemcall particolare che prende il file eseguibile e lo sostituisce al file della shell

si genera una seconda shell

gli oggetti in unix sono file

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/wait.h>

void pwncollege(){
			pid_t pid = fork();
			if (pid==0){
						execl("/challenge/embryoio_levelN",NULL);
			}else{
						wait(NULL);
			}
}
void main(){pwncollege();}
```

per ogni oggetto esistono solo tre utenti: owner,group(gruppo primario dell’owner) e other(tutti gli altri)

rwx 

possiamo cambiare i privilegi di accesso con il comando chmod (utilizzando +/- rwx o con i numeri)

inodf1 va a vedere chi è il proprietario

in una directory r vuol dire che possiamo leggere la lista di file contenuti, w possiamo aggiungere o togliere file, x possiamo eseguire il contenuto

setfacl -m u:student04:7 script00.sh

**Grep**

ricerca una stringa in un file (opzioni principali: -c conta le stringhe che hanno la stringa richiesta, -i (ignora i casi) -v stampa le linee che non hanno la stringa richiesta)

^ si usa per l’inizio stringa, . per ogni lettera qualsiasi, $ per il terminale della stringa.

per le ricerche usa le espressioni regolari (sequenze di simboli interpretate dalla shell)

**Vim**

Vi per entrare in input mode si usa i per tornare in command mode si preme esc.

**Codice sorgente**

Il codice sorgente veniva dato al compilatore che generava un file intermedio detto “codice oggetto” che veniva a sua volta dato a un linker che lo rendeva eseguibile. Il gcc oggi ha fuso queste due parti in un’unica compilazione.

Abbiamo quindi codice oggetto, codice sorgente e codice eseguibile.

Ci sono diversi passaggi, da codice ad assembler, da assembler ad oggetto, il linker recupera delle librerie e lo trasforma in formato eseguibile per poi essere caricato nel sistema.

**Output di un compilatore**

le informazioni vengono ottenute in modo diverso, standard elf per linux(presente nel mondo unix o da sony) oltre al codice contiene informazioni utili al sistema operativo per mandare in esecuzione un programma .text→.rodata(read only), con readelf -h possiamo leggere l’header del programma.

L’entry point dell’applicazione è l’indirizzo di memoria della prima istruzione del programma.

**Sezioni**

Sono tutte le informazioni che servono per poter costruire l’eseguibile, sono presenti N sezioni in base alla grandezza e funzioe del programma quindi non tutte vengono usate. Viene usato quindi il section header table, una struttura dati che contiene le section e il loro indirizzo.

- text:code
- .data: dati dichiarati con un valore iniziale
- .rodata:
- .bss
- .plt
- .got
- .got.plt
- .symtab

si possono vedere con `readelf -s ————-`

Le sezioni servono per comporre i segmenti che compongono l’eseguibile.

`objdump`  legge elf headers e può anche disassemblare.

Compile con:

`gcc filename -c targetfilename`

`gcc filename -o targetfilename`

**Formato rilocabile**

Nel formato rilocabile il compilatore traduce il programma partendo dall’indirizzo zero.

### Come nasce un processo

Viene letto il comando da CL, avviene un fork che crea una seconda shell; Exec è una syscall che per essere eseguita contiene il tipo elf, i sistema operativo legge e cerca l’elf, per verificare che sia tale controlla nell’header che gli dice dove si trovano tutti i segmenti dei file su disco. Se il file inizia con #! (shebang) è uno script.

File dinamicamente linkato:

File staticamente linkato: è autonomo, contiene tutto ciò che gli serve per andare in esecuzione.

ogni processo di linux ha una memoria che contiene:

- binario
- librerie
- Heap
- stack
- ogni memoria

## Elf

Esecuzione: il compilatore introduce una chiamata a una libreria start main

```java
#include int main(int argc /*numero degli argomenti*/,char *argv[]/*puntatore a carattere*/, char *envp /*variabili ambiente*/)
```

**System call:** Viene effettuata una system call grazie alla quale avviene  creato un processo che interagisce con il kernel. 

```java
strace ls -l mostra le systemcalls  chiamate dai processi
```

i signals sono syscall speciali che mettono in pausa l’esecuzione del processo e invocano l’handler. Il processo viene generato dalla fork e termina attraverso la [exit il](http://exit.il) genitore che genera un processo deve fare la wait su quel processo, il PCB mentre viene svolto il wait() su un processo figlio, entra in zombie. Periodicamente si sveglia il processo uno che va a ripulire il sistema dai processi zombie (settando il loro pid a 1).

## Privilege escalation via complete mediation

Permette di concedere certi diritti di accesso rispetto ad altri, parliamo di privilege escalation quando un soggeto passa da un insieme di diritti “0 a 10”, il processo passa da uno stato user ad uno stato kernel, utilizziamo questo meccanismo per permetterne l’uso controllato. Il meccanismo di complete mediation è il setuid. Con /etc/passwd possiamo modificare la password della macchina, da owner si passa a root e siamo in grado di modificare il file shadow. Real UID identifica il vero onwer del processo mentre effective uid identifica il privilegio del processo. Sudo è un file setuidato grazie al quale otteniamo temporaneamente privilegi root. Un processo si forka e il figlio ottiene l’intero UID del genitore, se il file che deve essere mandato in esecuzione è setuidato viene cambiato il EUID del processo con quello dell’owner

Da system manager o root come facciamo a setuidare? attraverso chmod possiamo settare il bit di setuid in ottale si aggiunge 4 all’inizio per toglierlo si mette 0 (ez)

## Scripting

https://devhints.io/bash

La shell interpreta i comandi o a uno a uno o con la pipe, fare shell scripting vuol dire fare un programma indirizzato alla gestione di sistema in modo tale che uno non debba più eseguire la stessa sequenza di comandi. si inizia con #! /bin/bash non dobbiamo più dichiarare le variabili ma vengono definite con $

```bash
$ bob = 'hello world' #si memorizza la variabile
$ echo $bob #cerca e stampa contenuto
```
Se si esce dalla shell tutte le variabili vengono cancellate

```bash
$ foo = 3
$ foo b=b3
```

con set possiamo vedere le variabili.

#! stampa tutti gli argomenti

$* tutti gli argomenti

$n l’argomento in posizione n

while [testo] #anche for

do

done

-a condition → and

core dump file è il file che può essere generato dal sistema quando si verifica un fault in un processo

# Assemblerx86

usato spesso per performance-critical parts of a program. Nel mondo della sicurezza è importante la conoscenza di assembly poiché la prima cosa che si fa è invertire da codice eseguibile ad assembler, esistono anche convertitori da eseguibili a c ma non sempre sono corretti. Serve anche per ottimizzare il codice, permette infatti di scrivere codice efficiente che può essere eseguito direttamente sulla macchina senza librerie.

Dati possono essere manipolati solo all’interno dei registri, possiamo sommare dati solo tra registri o tra un registro e un immediato.

I registri sono 16 i primi 8 RAX RCX RDX RBX RSP RBP RSI RDI.

Direttive: sono precedute da un punto.

```nasm
LOOP add rax,3
			jmp LOOP
```

i dati possono essere messi in variabili o registri, i registri sono un tipo di memoria speciale direttamente accessibili dal processore. L’unico modo per modificare una variabile è portarla in registro e modificarla all’interno di esso.

Se nel registro RAX prendiamo gli ultimi 32 bit si chiamerà EAX, i 16 AX. Solo due tipi di dati **Numeri** e **Caratteri**.

I dati vengono definiti all’interno dei programmi con db (databyte) sta al programmatore stabilire se la riga di codice debba essere considerata come carattere o numero.

Per accedere ai dati in memoria si può usare l’accesso diretto o indiretto.

- Register adressing: si sposta il contenuto fuori o dentro a un registro.

Gli immediati servono a caricare dati direttamente negli indirizzi, se non si mette nulla il dato viene intrepretato come decimale altrimenti con 0x come esadecimale. Mettendo un registro all’interno delle quadre il contenuto sarà considerato come indirizzo del registro da cui prendere il contenuto.

Per caricare l’indirizzo di buffer in un indirizzo devo usare `lea rex, buffer` poi `mov rax, [rex]`.

- Mul (dati senza segno), imul (dati con segno); bisogna usare imul, in mul viene preso implicitamente r sax come registro contenente un immediato.
- Divide div(””), idiv(””)
- Compaire (comp) compara i registri

systemcall: numero delle syscall viene messo in rax, parametri negli altri registri mentre il risultato in eax. File video è caratterizzato da un file descriptor a 1.

pwn.college.laser.di.unimi.it

nomecognome email unimi

root/challenge

```nasm
.intel_syntax noprefix
.global _start
.section .text
		_start:#inizio file assembly
```

objdump -d ex1

`gcc -nostdlib -static -o ex1 ex1.s`

`objcopy --dump-section .text=ex1.txt ex1`

cat ex1.text|/challenge…. (da fare per la consegna dell’esercizio) (signo black)

chiamata syscall

numero syscall in rax

primo parametro in rsi

[Comandi shell](https://www.notion.so/Comandi-shell-ef9835aa741b4bd9872dc72737b7e730?pvs=21)

```nasm
.intel_syntax noprefix
.global _start
.section .text
_start:
        lea rdi,pInputBuffer
        mov rsi,100
        call ReadLine

        lea rdi, pInputBuffer
        mov rsi,rax
        call Print

        #Usciamo dal programma
        call Exit;

Print:
        mov r8, rdi
        mov r9, rsi

        mov rax,1
        mov rdi,1
        mov rsi,r8
        mov rdx,r9
        syscall*
        ret

ReadLine:
        mov r8,rdi
        mov r9,rsi

        xor rax,rax
        mov rdi, 0
        mov rsi, r8
        mov rdx,r9
        syscall
        ret

pInputBuffer:
        .space 100
```

## Shell Coding

è scritto in linguaggio macchina che viene usato per sfruttare delle vulnerabilità interne al codice attraverso un attacco di code injection. Viene immesso all’interno di un processo in funzione che va quindi a svolgere tale codice e quindi le azioni che vogliamo svolgere sulla macchina.(WRITTEN, INJECTION, EXECUTED).

L’attacco base è un attacco di code injection che avviene all’interno della memoria per poter funzionare, viene usata nelle architetture di Von Neumann poiché programmi e dati occupano lo stesso spazio di memoria; tale attacco non può essere effettuato in una macchina di tipo Howard.

Prima cosa da fare è individuare un pezzo di codice vulnerabile.

```c
gdb -q checkbug
x/s $rip and x/i $rip
```

0x00007fffffffde20

La variabile name del programma viene messa nello stack.

Nel codice l’errore è l’inversione dei parametri.

Dobbiamo quindi fare in modo che il linguaggio macchina mandi in esecuzione lo shellcode

```c
mov rax, 59
lea rdi, [rip+binsh]
mov rsi, 0
mov rdx , 0
syscall
binsh:
.string "/bin/sh"
```

per iniettare il codice bisogna fare una pipe con cat in modo tale che il suo output venga dato all’eseguibile. Non funziona, allora se mette er trattino (-).

---

```bash
gcc -fno-stack-protector -z execstack main.c -o main
```

hexdmp shellcode

si apre la shell con la syscall execve (codice 0x3b)

objcopy -0 binary —only-section=text shell5 shell

strings shellcode.text

shell-storm.org

che indirizzo da mettere in rax per eseguire il buffer?

gdb nomefile

`b main` metto un break point al main

## Countermeasures

Le contromisure sono implementate in quattro diversi livelli di sistema, sono tutti meccanismi messi in campo per bloccare un attacco *smash in the stack,* queste contromisure vengono però implementate nel sistema operativo successivo, nel sistema operativo viene implementato il **ASLR.**

Questo va a randomizzare gli indirizzi di partenza di alcuni componenti ogni volta che viene caricato un processo.

L’altra contromisura viene adottata a livello di compilazione ovvero Stack Guard, il compilatore quando fa le chiamate va a vedere se nello stack è presente il valore guard aggiunto, in caso non fosse allora si verrà buttati fuori dal processo. Se sono uguali li stampiamo altrimenti chiamiamo stack mach failed.

Chris Eagle.

Mettendo il codice terminale, con i caratteri terminatori di stringa si avrà un blocco che terminaerà il processo e non. permetterà di fare un buffer overflow.

### Non-executable stack

Se il processore riceve un indirizzo specifico allora marcherà la parte di codice in modo da impedirne la compilazione.

### Data Execution Prevention

Marca una a una le pagine di memoria come non e seguibili

# Malware

è un programma che viene caricato in modo nascosto sul sistema con l’obiettivo di di compromettere la confidenzialità, l’integrità e la disponibilità dei dati della vittima.

Classificazione dei Malware, non esiste ancora oggi una terminologia e una classificazione specifica per i malware

Sono però divisi in base a come si diffondono e a cosa fanno(**`payload`**, codifica delle azioni che il malware svolge sul sistema infettato).

Quelli con programmi host

Quelli che vivono in modo autonomo

Quelli che utilizzano vari mezzi di infezione (trojans)

Quelli che si diffondono all’attivazione (virus, worms)

Il payload può compromettere il funzionamento del sistema o modificare il contenuto dei file e ovviamente nascondersi.

Inizialmente i virus venivano costruiti in assembly e richiedevano una grande capacità di software development dai creatori, sono stati creati quindi dei Toolkit che permettono di pre-costruire dei malware in base all’obiettivo finale.

(Toolkit acquistabili sul darkweb)

Stacks-net 

### **Advanced Persistent Threats**

Viene introdotto nel sistema che deve essere attaccato e rimane in incognito fino alla sua attivazione, adottando particolari tecniche per rimanere tale.

### Viruses

Sono programmi che infettano altri programmi. All’esecuzione del virus l’entry point fa partire il virus e poi il programma in modo da infettarlo.

Un virus è composto da tre componenti:

- Infection mechanism:(infection vector) che determina come si diffonde il virus
- Trigger: con che evento o condizione si attiva il virus
- Payload: determina cosa fa il virus quando viene avviato

### Macro and Scripting viruses

All’interno dei documenti(quali word, excel e powerpoint) possono essere avviati dei linguaggi macro

### Encrypted virus code

Codice del virus è cifrato, e presenta una funzione di encryption decryption che, al suo avvio, inizia a creare chiavi di cifratura differenti creando così dei virus gemelli diversi, la sua debolezza? la funzione di encryption decryption non poteva essere cifrata e questo portava a cercare questa parte. I costruttori di virus hanno fatto in modo che la encryption decryption routine cambiasse ogni volta creando così dei polimorfi, ciò permise di far saltare completamente il sistema delle signature. Il meccanismo di signature non è più sufficiente, per contrastarli ci è arriva kaspersky cui intuizione lo ha portato a pensare che il virus in memoria deve essere in chiaro, i virus polimorfi non li becco solo con la signature, apro una virtual machine avvio il virus che decifra il codice signature.

Per intervenire su ciò vennero creati i virus metamorfi, virus che possono anche essere in chiaro ma che cambiano di generazione in generazione in modo da rendere ogni coppia di virus diversa.

Per contrastarlo si manda in esecuzione il virus in virtual machine per vederne gli effetti.

### Worms

Sono malware che vanno in esecuzione autonomamente, va a cercare altri servizi di rete su altre macchine muovendosi in maniera randomica. Viene inviato in un file tramite indirizzo email, la macchina ha un certo indirizzo ip inizia o a generare indirizzi ip o a seguire la lista che ha, andando ad infettare tutta la rete

### Mobile code

Vengono immesse applicazioni contenenti malware nei marketplace, apple controlla con un team android controlla in modo automatico.

### Drive-By-Downloads

L’attacco viene guidato attraverso il download, l’attacco arriva poi dal server che sfrutta la vulnerabilità presente all’interno del browser.

### Clickjacking

Si basa sulla programmazione javascript e sulla capacità di utilizzare finestre trasparenti, un esempio è l’utilizzo di un clickjacking che va a sovrapporsi alla pagina di gmail e portandomi ad eliminare inconsciamente le email.

Chernobyl virus

Klez

Ransomware 

### Botnet

L’attaccante entra nel calcolatore e va a creare un bot  che viene usato per scopi illeciti. Si è interessati principalmente al pc e non ai dati presenti al suo interno, viene usata la macchina infettata per mandare email spam o diffondere malware. Sono molto difficili da rimuovere. Un bot viene controllato da una zona centrale della rete.

### Keylogger

Captures keystrokes to allow attacker to monitor sensitive information(pswd, usr)

### Spyware

Manda in tempo reale informazioni

### Ransomware

Criptano dati per riscatto.

indirizzo Ip ⇒ provider ⇒ macchina

### Backdoor

Utilizzata per poter marcare come accessibile una macchina non sapendo cosa farne da subito

### Rootkit

Un insieme di programmi installati nel sistema che permettono di nascondere l’attacco andando a sostituire un insieme di comandi utlizzati per il monitoraggio.

Possono operare in **user mode** e **kernel mode.** alcuni fanno partire il sistema operativo all’interno di una virtual machine.

Per impedire l’entrare in contatto con tali malware ci sono tre punti fondamentali:

- Prevention
- Detection
- Response

Ed implementare varie pratiche nelle aziende:

- Policy
- Awareness

Preparare i dipendenti ai possibili attacchi

- Vulnerability mitigation

Ridurre

- Threat mitigation

Ridurre le possibili minacce.

## Generations of anti-virus softwares

First generation: simple scanners

- Requires a malware signature to identify the malware
- Limited to the detection of kknown malware

Second generation: heuristic scanners

- Uses heuristic rules to search for probable malware instances
- Another approach is integrity checking.
- interity checking (tutto il software viene congelato permettendo il controllo del codice, se si modifica viene eliminato. Funziona solo con quelli preinstallati)

Signature: sequenza di byte che identifica il virus

## EDR (Endpoint Detection and Recovery)

Hanno sostituito gli anti-virus, sono oggetti altamente complessi che sono in grado di fare diverse attività. Principale cambiamento è il collegamento al cloud

Integrating threat Intelligence, feeds and IOCs (indicator of compromise, indica il livello di compromissione della macchina)

## AbracadabraWorm

ssh è il servizio più usato e più semplice da attaccare, estrae tutti i file che contengono la parola abracadabra. Trovato il file lo prende e lo manda ad un server

## NEC security

Oltre alla system security che si basa sulla macchina e sulla protezione da parte degli attaccanti che si impossessano di tale macchina abbiamo anche la network security.

La rete presenta due hosts(end point) che, attraverso un link ( ciò che appunto collega gli host), riescono a scambiarsi informazioni, gli hosts comunicano scambiandosi messaggi e perché ciò sia possibile devono potersi scambiare informazioni. Sono presenti anche i router che ricevono i messaggi e li smistano, generano traffico.

Esistono :

- Ethernet Hub: aumenta il traffico, prende il messaggio e lo manda a tutti
- Selective Ethernet Switch: che inizialmente funziona come un hub e poi riesce ad imparare gli indirizzi IP dei vari hosts permettendo degli scambi.

i Computer sono connessi ad un network attarverso una network Interface Card.

LAN

WAN più grande network rispetto agli altri tipi di network presenti

Sulla rete internet ogni host ha due indirizzi, u n MAC address, che serve per essere riconosciuti all’interno della LAN e l’altro è l’IP address; il mac address è un numero in 48 bit. Non è immutabile ma viene creato ed è unico per ogni telefono.

IP address è in 32 bit, dovrebbe essere unico ma non è p vero, IPV4 è il protocollo che gestisce i bit e ne tiene al massimo 4 miliardi, l’ultimo protocollo aggiunto è l’IPV6 mantiene fino a 128 gb.

Come fa un host a chieder un altro servizio ad un altro host.

Una macchina divide in pezzi un file e lomanda in rete,in cao un nodo si rompa/ sia pieno allora effettuo il packet switching, il sistema decide poi se riordinarli e mandarm+li modifica comunque.

Vengono poi passati a dei procolli

Connection lsee f 

## TCP:

- Protocolli di Transport che arrivano dall’alto
- Il protocollo IP si preoccupa di aggiungere al pacchetto le informazioni necessarie per poter arrivare a Destinazione, indirizzo che non è dlell’intestatario finale

bensì del primo router

- informazioni id instradamento

Incapsulation:

Upper layers   posta elettronica

tcp/udp 

IP

Layer 2 toglie internet header

Layer 1 bit stream

Payload di un pacchetto IP è un pacchetto tcp cui payload è l’informazione

rete internet è basata sul principio del best effort 

![Screenshot 2023-11-14 alle 15.55.17.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/74ad38c0-d1a1-4f83-b841-f49978dd2db3/Screenshot_2023-11-14_alle_15.55.17.png)

Pacchetto frame di ethernet

chi riceve il pacchetto ethernet togli gli header

Per potere comunicare con i pacchetti attraverso la lan devo conosce il MAC, è stato quindi introdotto ARP(address resolution protocol); di un host non si conosce il MAC address ma l’IP address, per recuperare il mac address (che serve per ricostruire il pacchetto ethernet che deve girare sulla rete) si utilizza ARP che recupera attraverso alcuni meccanismi (DNS) l’indirizzo host, viene infatti mandata una richiesta a tutte le macchine presenti sulla lan che inviano l’indirizzo IP proprio , se questo corrisponde a quello giusto allora verrà usato il suo MAC address e a questo verranno. inviati tutti i pacchetti  a quel MAC address. in caso nessuna macchina rispondesse i pacchetti verrebbero mandati al router che cercherà nella WAN.

![Screenshot 2023-11-14 alle 16.06.52.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/662582ab-4e07-4455-8d4c-3fc6d27537a4/Screenshot_2023-11-14_alle_16.06.52.png)

Network Attacks 

![Screenshot 2023-11-14 alle 16.23.04.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/f41719d6-5b69-457c-afa7-c810f9c708de/Screenshot_2023-11-14_alle_16.23.04.png)

La rete internet doveva essere realizzata per poter permettere agli stati uniti di sopravvivere anche a fronte di un attacco nucleare, successivamente venne creata per poter facilitare la comunicazione

## Spoofing

Consiste nella modifica del source address di alcuni pacchetti che , in base all’indirizzo modificato, assumono l’identità di:

- un server
- un router
- un web server
- un Host
- uno User

Questo avviene perché molti protocolli dei network non forniscono un meccanismo di autenticazione.

Modificare i pacchetti in modalità promiscua. Per fare un attacco di intercettazione vi sono diversi modi, un esempio è l’intercettazione della radiazione presente nel rame.

La più difficile da intercettare è la fibra ottica. Microonde e onde radio sono facilmente intercettabili

Wireshark

FingerPrinting, devo attaccare un sistema ma prima di tutto capire che sistema è

Port scanning,

### Protocollo ARP (protocollo di livello 2)

è presente una tabella chiamata arp cache che contiene da una parte l’IP add e dall’altra il MAC add. Viene mandato a tutti sulla rete un “messaggio” in cui viene chiesto chi possiede un certo indirizzo mac; si ottiene così l’indirizzo IP corrispondente.

L’arp cache viene aggiornata molte volte e in modi differenti

## Attacco MITM

Sfrutta le debolezze del protocollo arp, dobbiamo convincere A a mandare i pacchetti che deve mandare a B alla macchina C, che sceglieràa se tenerli o farli arrivare a B.

Andiamo ad “avvelenare” la cache mettendo cose che non sono veri. All’host A mando un reply dicendo che l’ip della macchina B ha come MAC add l’indirizzo MAC di C.

Per fare questi attacchi esiste un tool (Ettercap)

 

## DoS- DDoS

Tentativo di prevenire gli user di un certo servizio di poter usufruire dello stesso

![Screenshot 2023-11-16 alle 15.27.11.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/4ad720d9-a05e-4ec6-9451-ef83a9aca41d/Screenshot_2023-11-16_alle_15.27.11.png)

## Smurf Attack

Attacco basato sull’invio di un’enorme quantità di ping alla macchina, ogni macchina connessa alla rete riceve un ping da un indirizzo ip vittima e risponde inviando altrettanti ping che faranno bloccare la macchina.

## tcp Hijacking - SYN|ACK

viene inviato un pacchetto SYN con un numero casuale allegato, il server dispone 

Dirottamento del tcp

## Syn Flood

La macchina viene intasata in modo tale da non essere più accessibile dalla rete.

## RSH

permette di eseguire da remoto comandi su un’altra macchina

Macchina di shimomura, vengono inviati 20 segnali syn alla macchina di shimomura che risponde con altrettanti segnali syn|ack

## Linguaggio di scripting

posso mettere in un form del codice javascript e inviarlo, questo verrà visualizzato come se fosse codice del sito. (attacco tipo reflected xss)

```c
<script>alert(1)</script>
```

Per filtrare bloccando questo attacco si possono utilizzare varie librerie, si può fare un filtraggio manuale ma non è efficiente poiché non blocca tutte le possibilità.

Per provare xssgames

## Sql injection

```sql
SELECT * FROM Products WHERE ProductId = 15; DROP TABLE Suppliers;
SELECT * FROM Orders WHERE OrderId = 16 AND 1=1;
SELECT * FROM Users WHERE Login = 'Administrator' -- ' AND Password = ''
```

Permette ad uno user di modificare una query non protetta in modo da eseguire operazioni  a cui non potrebbe avere di solito accesso. Queste injections sono ottenute con lo scopo di integrare lo user-supplied information all’interno delle queries dinamiche: la query risultante è differente in base a ciò che lo user richiede.

Si possono ottenere tutti gli username con `SELECT*FROM users WHERE username = ‘vv’ or ‘x’=’x’`(questo restituisce tutto poiché sempre vera).

Andando per tentativi posso capire i tipi presenti nelle varie tabelle

Esiste una tabella che contiene il nome di tutte le altre tabelle

Metasploit viene utilizzato come tester degli attacchi attraverso una macchina creata da esso.

Devo evitare di andare a completare la connessione in certi casi.

Sudo `nmap -sS`, si ottengono i servizi delle varie porte

con  `nmap -O` ottengo anche la versione del sistema operativo oltre alle altre informazioni generali

Nmap Idle Scan, sfrutta la segmentazione  Ip

Fare una connessione alla macchina con l’id dello zombie, si manda il syn alla macchina vulnerabile che, in caso chiudesse le porte, resetterebbe la macchina zombie al secondo tentativo.

scaricare virtual box su virtual box anche kali, metasploitable 2

# Defensive security

## Host protection System

Abbiamo tre differenti momenti che caratterizzano un qualunque sistema di protezione:

- Autenticazione, per sapere chi è la persona che entra, decidendo poi cosa può fare successivamente
- Autorizzazione
- Controllo

Devo trovare anche dei meccanismi per mettere in pratica le regole adottate

- Subjects are active entities i.e. they perform operations
- Objects: are passive entities they suffer operations executed by users and subjects
- Rights: memory access, access to files, invocation of methods in an object system

the reference monitor is the set of mechanisms which on any system are in charge of the access control that is the enforcing of the access control rules

In practice should offer:

- Complete mediation
- Be Tamper proof (non corruttibile)
- Be small enough to understand (verify)

### Identification

La politica di sicurezza definisce quale soggetto può accedere e con quali modalità, per fare ciò bisogna avere un meccanismo che identifica chi accede, ciò avviene nella fase di autenticazione. Per farsi identificare dal compilatore l’utente e la macchina sanno una cosa che solo loro sanno.

Per quanto riguarda la protezione crittografica ciò che viene memorizzato nel sistema non è la password ma una parola criptata, viene infatti immessa in un algoritmo che modifica la parola trasformandola in un codice

### Password vulnerabilities

Il meccanismo delle password è idealmente perfetto e sarebbe inattaccabile se utilizzato correttamente, l’utilizzo erroneo (utilizzando password brevi e semplici) rende questo meccanismo molto facile da attaccare

### Attacchi high tech

Sono attacchi che richiedono competenze informatiche e l’uso di strumenti informatici (john the ripper)

- brute force: La password viene memorizzata sui file attraverso l’uso di particolari algoritmi crittografici, con questo attacco si avrà una riuscita sicura al 100% a discapito di un aumento esponenziale del tempo di elaborazione
- dictionary: abbiamo un dizionario di parole che potrebbero essere simili alla password, si controlla che la sha sia uguale a quella della password e il gioco è fatto.
- rainbow attack:

### Salt

prendiamo una parola password, la diamo in pasto all’algoritmo e si ottiene la parola cifrata che sarà sempre così, per renderla più sicura e diversa dalle altre sue copie (utilizzata magari da diversi utenti) si va ad aggiungere il sale, caratteri che modificano la parola cifrata, questo andrà a rendere inutile il rainbow attack.

### Controlli biometrici

Problemi:

- possono essere invasivi: controllo della retina
- possono essere costosi

### Controlli token (what you have)

Si vanno ad utilizzare dei numeri generati randomicamente (token intesa sanpaolo, app one time password) direttamente sincronizzati con i server a cui ci si deve connettere

Tecniche di clonazione della carta di credito, un dispositivo appoggiato sul lettore delbancomat cllegato via wifi ad un’auto a 10 metri di distanza che clona la carta di credito (bulgari so esperti)

Sim card security, ogni sim card contiene informazioni importanti utilizzate per identificare il possessore.

### Strong authentication

Multifactor authentication, we use different  authentication elements (2fa password+random token)

### SSO

Single sign-on permette di accedere una sola volta

![IMG_1169.HEIC](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/f3b51bb1-f728-4141-8028-64ba8baf326d/IMG_1169.heic)

Un esempio è eduroam che è utilizzata in tutto il mondo e che ci permette di essere identificati/autenticati anche in università in svizzera ecc..

## Access Control

Ogni volta che un utente si è autenticato vado a controllare se è  autorizzato a compiere certe attività

Sono meccanismi di prevenzione che prevengono l’uso non autorizzato di una certa risorsa e l’uso di una risorsa in modo illecito. Una persona accede ad una risorsa solo se presente nel registro delle persone che hanno il permesso per accedere a tale risorsa. Garantisco così integrità e confidenzialità delle risorse.

![Soggetto.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/d843cd46-0334-44bc-ab62-4eb922c91274/Soggetto.png)

### Politica di controllo degli accessi mandatoria

La risorsa che vogliamo proteggere è il sistema operativo, dobbiamo cioè individuare un metodo di controllo degli accessi che permetta di proteggere il sistema operativo

### 80x86 MAC policy

vengono assegnate etichette che decideranno cosa fare nell’ambito del sistema. Ogni soggetto/oggetto può avere 4 differenti etichette divise in 4 anelli che vanno dall 0 (kernel, può fare tutto) al 4 (per i software)

Ogni componente è considerato un segmento e possiede un’etichetta che esprime il suo livello d protezione. il DPL (descriptor privilege level) specifica il livello del segmento a cui appartengono i segmenti.

L’hardware memorizza il DPL mentre il CPL indica il livello di protezione

Policy: un soggetto con privilegio c (ring) può accedere a dati con livelli di privilegio D. Ogni volta che il computer viene avviato il Privilege checker metterà a confronto per evitare che uno user di livello 3 possa accedere a dati di livello kernel attraverso un “cavallo di troia” ovvero utilizzando un altro user con livello 0 come copertura. l’hardware va a proteggere accessi non autorizzati nel’hardware

### Controlled invocation

è un meccanismo che consente ad un programma utente di accedere a codice protetto di un sistema operativo, è un meccanismo che viene implementato attraverso le system calls in modo controllato. Questo meccanismo fa uso di un gate (struttura dati) che gli permetterà, grazie alla system call, di svolgere solo l’azione data dalla stessa syscall, viene salvato il contesto del processo, viene fatto un jump ad un indirizzo preventivamente memorizzato all’interno di una tabella.

Gli obiettivi primari di un IT audit includono:

- valorizzare i sistemi e i processi in modo da mettere in sicurezza i dati della compagnia
- determinare i rischi di certe informazioni della compagnia e comunicarle
- va a verificare che non ci siano problemi di varia natura

Per fare ciò l’IT audit va a ritirare il registro dei log che viene aggiornato dal reference monitor con ogni nuova operazione svolta all’interno del sistema permettendo all’IT auditor di riconoscere eventuali irregolarità.

L’analisi dei dati per scoprire o fare la diagnosi degli eventuali problemi di sicurezza, ciò può essere svolto anche post mortem (successivamente all’attacco).

per leggere i file di log possiamo utilizzare vari comandi per testi dato che si trovano in questo formato, altri hanno comandi apposta per essere letti poiché sono in binario e si possono trovare tutti in /var/log

Security information event manager

La politica del rewriting è sconsigliata alle grandi organizzazioni.

## Cryptography

studia i meccanismi che ci permettono di trasformare certi documenti in modo reversibile facendo si che possano essere letti solo da poche persone.

Il modello di riferimento:

abbiamo mittente e destinatario che vogliono comunicare in modo segreto e l’intruso cerca di capire ciò di cui vogliono parlare

Nell’ambito della crittografia esistono due chiavi

chiave simmetrica(privata)

chiave asimmetrica(pubblica)

la funzione di encriptazione prende come input il Plaintext P e una chiave restituendo il testo criptato, si dice chiave simmetrica perché è uguale per entrambe le funzioni di encryption e decryption, stream cypher (si crypta carattere per carattere) block cypher(si crypta in blocco alcune lettere)

### DES(data encryption standard)

Nato in America in idm, è un block cypher di 64 bit (8 caratteri), usa chiavi da 56 bit esistono delle sue varianti come il triplo des (svolto tre volte) abbiamo poi il double des e il triple des diviso in doppia e tripla chiave.

### AES:Advanced Encryption Standard

128, 192,256 bit, venne adottato dagli americani come  algoritmo per poter criptare file top-secret

### Cipher Block Chaining (CBC) Mode

il primo blocco viene messo in xor con un initialization vector 

Con ECB, in caso avessimo molte ripetizioni nel testo ci ritroveremmo con un testo non ben criptato

Nel 1976 DIffie,W. e Hellman pubblicarono un libro “New Directions in Cryptography” dove cercarono di prevedere che nel nostro mondo sarebbero esistite due chiavi, una pubblica e una segreta che, se generate a coppie, avrebbero una cifrato una frase e l’altra decifrato la stessa frase

Con la mia chiave privata posso cifrare il messaggio e chiunque abbia la mia chiave pubblica possono decifrarla. facendo così si va a rendere effettiva l’autenticità del documento, questa operazione è detta anche firma digitale

il problema della crittografia a chiave pubblica è l’intercettazione da parte di un man in the middle.

## Funzioni One way

Funzioni matematiche che prendono in input un file di dimensione qualsiasi e questi restituiscono stringhe di 512bit.

Per verificare che la firma digitale per l’Hash del documento è corretta dobbiamo:

1. prendere la HASH key privata e decodificarla con la publlica
2. Andare ad estrarre l’hash in chiaro

per garantire l’integrità aggiungiamo una chiave che ricevono entrambe le chiavi, non srà più una chiave di encryption ma di integrità

Quando un utente sottomette la sua chiave pubblica ad una altro utente gli invia contemporaneamente un certificato che attesta tale chiave

La certification autority è un’entità alla quale ci si rivolge per poter ricevere una certificazione, questa viene poi viene immessa in un Public key Infrastructure in modo da poter essere gestita anche in caso di smarrimento della stessa

## RFC(Request For Comments)

sono documenti scaricabili e disponibili in rete in maniera totalmente gratuita

## Protocollo Key Exchange (Diffie-Hellman)

Inventato per poter permettere a due persone di scambiarsi segreti su un canale in chiaro (tracciabile)

### Discrete logarithm problem

Problema risolvibile sempre se presenta un numero primo

Alice e Bob devono condividere un segreto, entrambi calcolano un numero casuale in modo che attraverso un certo modulo possano scambiarsi segretamente la chiave, problema di questo algoritmo è sempre il Man in The Middle (seppure remota e non immediata)

### Strategia di confidenzialità

### Integrità

è sufficiente che io studi un meccanismo che attacchi ad ogni messaggio un hmac

Problema di tipo politico:

- Trattato di varsena:
    - scritto da alcuni paesi dopo la seconda guerra mondiale, serve a non danneggiarsi l’uno con l’altro e quindi il divieto di scambiarsi armi strategiche e nucleari senza autorizzazione, questo ci tocca poiché tale divieto vale anche per gli algoritmi crittografici.

Gli algoritmi crittografici successivamente vennero liberalizzati per l’uso commerciale.

Altro problema è dove facciamo la crittografia:

- può essere fatta a livello applicazione, della crittografia si occupa il programmatore, comporta quindi la conoscenza da parte dei programmatori di elementi di crittografia, un esempio è la end-to-end encryption (whatsapp) che non permette la visione dei messaggi se non da una delle due parti della chat.
- livello rete, traffico cifrato a livello di IP e rimane cifrato fino al’altro ip, se faccio la crittografia a livello tcp il programmatore deve sapere quali numeri usare e necessita di particolari  librerie (VPN)
- livello trasporto (GMAIL)

Varia anche la quantità dei dati cifrati:

- Lv transport cifrati i dati e un pezzo di header
- Lv rete cifrati dati, tcp e parte dell’IP
- Lv software solo dati
    
    ![IMG_1199.HEIC](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/02a5fd94-a8a8-41a9-9d0d-73703e28ad89/IMG_1199.heic)
    

Protocollo utilizzato dalla crittografia a livello rete è IPSEC

Sottomodulo di IPv6, venne tolto per problematiche di sicurezza. venne poi adattato per lavorare su ipv4, è una risposta agli attacchi di intercettazione e di spoofing.

Abbiamo diversi algoritmi, AES modalità CBC con chiavi a 124 bit, o tripleDES-CBC con chiavi a 168 bit

Permettono:

- autenticazione dell’utente
- confidenzialità
- integrità, su singolo pacchetto

il programmatore che scrive su una macchina a livello IPSEC non deve preoccuparsi del tracciamento dei suoi dati.

- AH, Fa un controllo di integrità su tutto il pacchetto
- ESP

Il pacchetto originale ip è formato da IP header,TCP header e data

ci sono però due tipi aggiuntivi, tunnel mode, dove il pacchetto IPsec viene inserito all’interno dell’IP, Transport mode, viene aggiunto IPsec header

Il transport viene utilizzato quando si ha un collegamento diretto tra Client e server mentre il tunnel mode, viene utilizzato se si passa da nodi prima di poter arrivare al client/server, nei nodi viene ritirato l’IP header e arriva a destinazione.

Authentication header, si prende l’IPheader a cui si aggiungono alcune informazioni

![Screenshot 2023-12-19 alle 15.12.45.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/a0b857ba-8d76-4d04-bb25-23803deb32b4/Screenshot_2023-12-19_alle_15.12.45.png)

![Screenshot 2023-12-19 alle 15.12.19.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/ddf28075-3f71-4cf3-addf-d28af3408869/Screenshot_2023-12-19_alle_15.12.19.png)

come si implementa?

- partiamo con un security policy database, un oggetto che contiene le security policy che specificano il tipo di trasformazione da effettuare nel pacchetto, se andiamo in tunnel mode o transport mode e altre informazioni. Va definita una security policy per ogni senso dei dati (quelli che ricevo e che invio)

dal 2005 venne adottato, assieme all’ultima versione, IKE, un protocollo attivato inconsapevolmente dall’utente quando tenta di comunicare con un altro client

![Screenshot 2023-12-19 alle 15.25.20.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/ebd9f677-5d3c-4c28-a2d8-b33a17045148/Screenshot_2023-12-19_alle_15.25.20.png)

![Screenshot 2023-12-19 alle 15.26.07.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/9479bb86-6b36-44d1-b07a-ff493fdcd585/Screenshot_2023-12-19_alle_15.26.07.png)

### IPsec, benefici

Concede un livello di sicurezza per tutte le applicazioni da TCP in poi

Trasparente a programmatori e user

estendibile ad altri algoritmi crittografici

### IPsec,contro

Sicurezza livello traffico

Blocca l’Accesso ai non-IPsec Hosts

### SSL/TLS

Protocollo pensato da NETSCAPE security, pensato come sicurezza tra due host a livello trasporto, mentre a livello tcp abbiamo abbiamo le porte, Protocollo con maggior riferimento in browser e server (http)

- Server authentication
- Client auth
- Data confidentiality
- data integrity
- distribution/generation  of session keys

Per autenticare un soggetto, lo stesso deve esibire una chiave x.509 e utilizza gli algoritmi:

- rsa
- dh
- dss
- fortezza

Handshake permette di condividere chiavi segrete tra client e server

Record protocol: macina

Protocollo base: negoziazione tra client e server per decidere gli algoritmi da usare, ci si scambiano le chiavi ed infine i dati.

L’hand shake come funziona?

viene inviata una richiesta di connessione dal client al server che risponde con un altro numero random e con un CipherSuite inviando successivamente la chiave pubblica, il client prende la chiave del server e cifra un numero casuale inviandolo come tale al server stesso.

Dopo aver contrattato calcolano il pre_master_secret

![Screenshot 2023-12-19 alle 15.44.12.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8966f6ff-4fda-4cfd-93a6-676a9ac4742e/b85ba4c9-3aa8-4614-b4a5-70268c6fd5e7/Screenshot_2023-12-19_alle_15.44.12.png)

L’autenticazione del server attraverso il certificato è obbligatoria

Una volta che sono state definite le chiavi di autenticazione il record protocol prende il pacchetto tcp da inviare

- lo comprime
- calcola il MAC
- cifra il pacchetto
- aggiunge l’header TLS
- lo invia

https è la versione di http costruita non su su tcp ma su tls

Possono comunque esserci dei BUG in questo livello che permettono la rottura dei sistemi e quindi la possibilità di rubare chiavi di cifratura

### Crittografia end to end

Con questa crittografia impediamo il man in the middle, con questa crittografia i dati vengono criptati da un client all’altro, viene utilizzato da:

- Telegram, che utilizza MTproto
- whatsapp e signal, che utilizzano Signal
- Wire

### MTProto

creato per telegram, presuppone che tutto ciò che viene fatto sotto non sia sicuro, due protocolli di crittografia differenti:

- cloud chats, memorizzati in chiaro sui server
- secret chats, memorizzati in modalità cifrata

come avviene la chat?

Entrambi i client stabiliscono una chiave con il server quando A deve comunicare con B,  invia la chiave al server che decifra, telegram mantiene quindi le chat in chiaro all’interno del server.

Nelle secret chats la crittografia è differente, alfaRa manda al server che intercetta e invia a B che invierà a sua volta alfaRb al server. il problema è quindi che  il server può fare man in the middle, per evitare questo la stessa telegram consiglia di scambiarsi le chiavi e vedere (outofband) se vi è stata qualche violazione.

### Signal Protocol

è sempre presente un server, al momento della creazione dell’account viene creato un record nel database in cui viene memorizzato un pacco di materiale crittografico a nostra insaputa, vengono generate queste chiavi, nel  momento in cui A deve parlare con B accede alle informazioni pubbliche.

La chiave che viene calcolata entra nel KDF che genera una nuova chiave per decifrare il messaggio e una chiave per cifrare il successivo (key ratchet), in signal le chiavi vengono modificate ad ogni messaggio mentre in MTProto ogni 100, la sicurezza sta nel perdere solo pochi messaggi  con signal e molti in proto. inoltre signal non memorizza nel server i messaggi mentre proto (per una scelta di mercato che permette l’accessibilità da altri device dello stesso utente) si.

# PGP

### Web Of Trust

OpenPGP permette di decidere in modo autonomo di chi fidarsi e quanto.

```sql
gpg --full-generate-key
gpg --list-keys
gpg --import file.key
gpg --keyserver keyserver.ubuntu.com --recv-keys "chiave"
gpg --output file.txt.enc --encrypt --recipient "Graziano Nobile" file
gpg --decrypt
```

possiamo usarlo come programma per cifrare messaggi

La firma spesso spacca

## Password cracking

Per evitare che la mia password venga indovinata posso utilizzare un salt che, nonostante la password sia uguale, impedisca di entrare ad un attaccante.

### John the Ripper

software tool che permette di craccare password anche con bruteforcing

- single john mypassword —single
- wordlist: john mypassword —wordlist=file.txt
- Incremental: john —incremental mypassword
- External

## Defenses security

Per evitare di essere attaccati dobbiamo adottare una strategia di difesa

Per prima cosa si identifica la vulnerabilità, si cerca di proteggere il sistema

Si identificano anomalie e i processi per poter rilevare eventuali attaccanti

In caso di mancato blocco di un eventuale attacco si recupera ciò che si è perso.

### Basic cybersecurity tools

Abbiamo già visto alcuni strumenti:

- Crittografia
- Protocolli crittografici(signal)
- antivirus

### Firewall

Analizza traffico di rete e in base alle caratteristiche impostate riesce a decidere quali pacchetti tra quelli letti, buttare via o far passare. Viene organizzato in modo tale da permettere un unico punto di entrata e uno di uscita. Tutti i pacchetti sospetti vengono bloccati, entrano però in gioco i virus immessi con cavalli di troia.

Primo firewall disponibile sul mercato è il Packet filter, non entra all’header IP (che contiene indirizzo utente, destinatario)

- Stateful inspection
- Proxy firewall:
    - Application Gateway
    - circuit-level Gateway

(queste differenze non esistono più, si parla di next generation firewall)

Packet filter:

- Data Available Ip source,Transport protocol,TCP/UDP, ICMP message type,Packet options
- Actions Available
    - allow the packet to go trought
    - Drop the packet
    - Alter the Packet
    - Log informatiom about the packet

### Stateful packet filter

Si ricorda le connessioni aperte 

Allow SSH external hosts to internal hosts

- two rules:
    - Inbound and outbound
- How to know? a packet is for SSH?
    - Inbound: src-port>1023,dst-port=22
    - Outbound: src-port=22,src-port>1023
    - Protocol=TCP
- ACK Set?

Internal hosts can access DMZ (zona demilitarizzata, servizi pubblici), oppure può uscire. Un host esterno può accedere nel DMZ ma non può accedere all’intranet, host in DMZ possono accedere ad internet ma non all’intranet, un attaccante che riesce a compromettere un host in DMZ non potrà quindi attaccare l’intranet usando quello stesso host.

La DMZ riduce all’osso le funzionalità e le librerie del sistema operativo 

I proxy filewalls 

- Hanno due connessioni invece di una sola
- anche a livello di trasporto

Application level payloads

Per poter essere completamente sicuri dovremmo avere almeno un firewall per ogni applicazione (http, tcp)

Molta sicurezza ma si paga a livello prestazionale

### Air Gap

Nell’Air Gap passa traffico e viene deciso cosa far passare, a differenza del firewall in questo caso si ha un server che controlla ogni cosa senza permettere una connessione diretta tra macchina e network.

Se si vuole utilizzare http proxy bisogna mettere l’opzione anche sul browser per dirgli che le azioni verranno proxate

### New Generation Firewall

Si tratta di un firewall che permette ispezioni profonde nei pacchetti, questo firewall inoltre si adatta agli attacchi bloccando per esempio chi effettua scansioni con nmap

### IDS

In caso il firewall non reggesse e l’attacco passasse entrano in gioco gli **Intrusion Detection System** cui scopo è individuare in tempo reale un’intrusione;

Questi analizzano 

- Host-Based,su pc o device remoti, su un server  o su un host
- Network-based, su punti strategici nel network, traffico di rete; hanno bisogno quindi di sensori messi nella rete per individuarne il traffico

Si differenziano per il tipo di informazioni che elaborano possono entrambi essere:

- Signature-Based,cercano stringhe di bytes o sequenze maligne
- Anomaly-Based,

`Misuse detection`

- Un attacco viene individuato attraverso una serie di azioni ed eventi che lo caratterizzano (sequenze syscall, packet patterns)
- bisogna conoscere però a priori che avverrà un attacco
- Identificano attacchi tipo:
    - Buffer overflow
    - una setuid lancia un comando con alcuni valori strani

`Anomaly detection`

- Partendo da un modello che definisce le normali funzioni di un server viene identificata situazioni che deviano significativamente dalle stesse.
- Questo individua potenziali attacchi sconosciuti
- Si basano quindi sull’analisi del sistema

### Hids

Tutto quello che riguarda gli host vengono dati in pasto agli host intrusion detection system, syscalls, command line, network data, processi…

I controlli vengono fatti in live

### Network based IPS

### IDS errors

- Falsi negativi: fallisce l’individuazione di una attacco classificato come inizio di un’attività maligna
- Falso positivo

Gli Ids sono stati arricchiti negli anni con sistemi di prevenzione

Non essendo presenti sempre persone capaci di individuare tali vulnerabilità e pericoli sono stati creati i SIM, security information management che raccolgono tutti i  dati in arrivo al sistema e capaci di fare, grazie al machine learning, un report finale sopperendo così alla carenza umana

### SOC

I security operation center hanno come cuore le SIEM, sono dei centri di competenza e nascono sulla falsa riga dei centri di sorveglianza, (esistono anche i cybersecurity SOC), sono centri che raccolgono tutti i dati che passano attraverso i loro serve e attraverso i SIEM individuano eventuali attacchi, i soc sono quindi centri di detection, host based e cercano di prevenire grossi danni derivanti da un attacco informatico, in caso di attacco informaticoil tutto viene affidato al CSIRT, computer security incident response team

## Privacy in computing

Definizione:

- The right to be let alone
- The right to individual autonomy
- The right to a private life
- The right to control information about oneself

é quindi un diritto per tutti, la nozione di privacy come diritto nasce nel 1890 durante un processo riguardante una foto pubblicata sul giornale in america.

Primo garante alla privacy italiano fu s. rodotà, secondo cui la privacy riguarda soprattutto la dignità e la vita privata delle persone.

Confidenzialità e privacy vengono spesso confuse

La privacy diventa quindi un diritto fondamentale, che se vuiolata, rendono la persona non pù autonoma delle sue esigenze.

Il grande problema della privacy riguardo chi allora può.

Inoltre va a peggiorare la privacy il valore attibuito alle azioni di mercato

- Personal Identifiable Information: immediate identification of a person
- Non-Pil non entirely or frequently data to identify a person
- location data
- Device/ Netqork Data

Ex Non_pll:

- Websites Visited
- Search queries
- Online communication
- File Downloads and Uploads
- Streaming and Media cosumption

### Privacy threats

Minacca alla privacy, un esempio è una query ad un gruppo poichè condividiamo con chi ci consegna tale prodotto.

infine le importazioni.

Quali sono i principali obiettivi di un attacco alla privacy?

- furto di identità, l’obiettivo è impersonificare una persona, farsi scambiare per un altro
    - phishing
    - data breach
    - Social engineering
- Profilazione della persona, tipo di attacco mirato a costruire il profilo comportamentale di una persona
- Data breach

Per evitare la profilazione cosa possiamo fare? non molto

Questa cosa è peggiorata grazie agli informatici attraverso big data, machine learning e altre cose

I data breach sono i più utilizzati attacchi:

- Equifrax
- Ashley Madison: rubati 30 milioni di dati
- Cambridge analytica: thisisyourdigitallife, gli utenti di facebook dovevano svolgere un test dando però l’accesso ai propri dati e a quelli degli amici, permettendo a cambridge analytica di profilare circa 70 milioni di persone
- Campagne politiche di trump o idee riguardanti la brexit: si ricevevano diversi banner che andavano ad influenzare il voto dei vari paesi

c’è una top 10 dei più grandi dara breach dalle organizzazioni: primo è yahoo

Ci sono due approcci differenti per proteggere la propria privacy: legge e e tecnologia

- Con le leggi promulgate dai governi per cercare di contenere ed evitare gli abusi di questi dati
- Auto-regolamentazione dei vari business
- PETs (privacy-enhancing technologies) adopted by individuals (PGP è l’esempio di PET)
- Educazione sulla privacy dei consumatori e degli esperti IT

Legal Protections

### General Data Protection Regulation

Developed with a focus on social media and cloud providers, but affects everyone

The aim is for the EU to strengthen and unify data protection to give control back to individuals

it comes into play on 25th may 2018

Anche i cookie vengono ritenuti informazioni personali

Le organizzazioni devono avere il consenso scritto da parte dell’utente

La raccolta delle informazioni non è vietata ma deve essere preventivamente verificata da parte dell’utente, l’organizzazione si deve impegnare a garantire che abbia predisposto le giuste precauzioni per proteggere tali dati, in caso contrario verrebbe multata.

Negli stati uniti non esiste il diritto costituzionale riguardante la privacy

Pseudonimità, l’identità di una persona è nota solo in alcuni contesti 

Anonimità

inosservabilità e Unlinkabilità, si riesce ad utilizzare una risorsa ma non si viene loggati

Uso di database criptati (crypto-database), con un databreach verrebbero scaricati i dati ma sarebbero comunque cifrati

## PET

- Tor project,The onion router è un progetto che parte negli anni ‘90 dalla marina militare americana, permette a tutti di utilizzare internet mantenendo privato l’indirizzo IP. Il download installa una versione custom di firefox con settaggi utili per prevenire azioni malevole, viene usato per aggirare censure
- TEE, Trutsted execution environment, sono environment dove vengono isolati il codice eseguito e i dati a cui si ha avuto accesso, così da proteggerli confidenzialmente
- Cookie profiling, utili per la sessione ma identificano la persona
- Proxy for anonimous communication, l’internet access provider può vedere la nostra comunicazione, il proxy ci aiuta ad anonimizzarla. ha diversi problemi, il primo riguarda la natura del proxy, essendo un server può essere degradato o comunque attaccato per deanonimizzare le informazioni. è stato quindi introdotto TOR

## TOR, the onion routing

Faccio passare il pacchetto attraverso diversi nodi

Il suo nome viene dal fatto che i messaggi vengono cifrati a strati, il messaggio cifrato viene inviato ad ogni nodo che ad uno ad uno decifra il messaggio in base al livello di criptaggio. l’ultimo livello è criptato solo se era stato criptato inizialmente. esiste un altra cifratura a tre nodi per i siti .onion

gli url in tor sono randomici con .onion alla fine, in the hidden wiki sono presenti diversi link

Si possono fare attacchi di correlazione sul primo e ultimo nodo per poter ricostruire il flusso dei dati