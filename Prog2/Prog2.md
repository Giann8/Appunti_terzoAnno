# Programmazione

Programmazione - L1

**Metodologia**

Affidabilità

Efficienza

**Decomposizione**: scompongo in più parti l’artefatto. (modularità)

- Stesso livello.
- Le parti devono essere approcciate in modo indipendente.
- Combinati per ottenere la soluzione.

**Astrazione**

- Astrazione per parametrizzazione, su qualunque copia di dati
- Specificazione
- Astrazione procedurale, si va a suddividere in procedure
- Tipo di dato (informazioni e comportamento)

-Astrazione iterazione

-Astrazione per gerarchia

**Java**

JVM

src.java

Quelli eseguiti dalla JVM sono le src.class

Oggetti=Classi in java.

Ci sono informazioni (dette stato dell’oggetto) e delle operazioni che voglio effettuare a partire da quello stato (detti metodi).

Ogni classe ha più istanze.

Struttura PRG - tante classi

```java
public class NomeClasse {

stato

metodi

header{
corpo
}

Esempio metodo int static somma(int x, int y){returnx+y;}
Public static void main(String[] args)

}
```

struttura del metodo:

- modificatori: parole chiave di java che modificano le funzionalità dei metodi (public, private e secure)
- return type: il tipo di dato da restituire;
- nome del metodo: ciò che identifica il metodo;
- parametri, parametri e nome del metodo sono identificati nella “firma”;
- corpo del metodo, insieme di istruzioni  eseguite all’invocazione del metodo.

Variabili:

- Di istanza: viene allocato loro spazio quando viene istanziata l’oggetto a cui appartengono.
- Locale: il cui ciclo di vita termina al termine del funzionamento del metodo.
- globale

### **Metodi costruttori**

non ha tipo di ritorno (ovvero non ne dichiara alcuno) ed è chiamato automaticamente e solamente quando viene istanziato quel tipo di oggetto;

è presente in ogni classe e presenta lo stesso nome

Pacchetti (gerarchica)

-fs

-naming

-incapsulamento

Moduli (nuh uh)

Collezione di pacchetti

**Toolchain**

**Java17 JDK**

Testing unit,gradle

Per compilare java nomefile.java otteniamo nomefile.class

Java nomefile

Variabili java (stack)

Tipo nome valore

Primitivi

Riferimento fanno riferimento alle istanze dell’oggetto (avere più riferimenti complica il codice)

Un array è un tipo di riferimento

Oggetti (heap)

Come si istanziano gli oggetti e come si invocano

**Istanziano:** Pippo P = utilizzo new NomeClasse(…..), restituisce un riferimento

**Invocano:** P.abbaia(…)

selezione

IF (espressione booleana)istruzione

```java
public class main void{
if(bool1==bool2){system.println("totgay")}
}
```

```java
	public class FascePEGI{
public static void main(String[] args){
try (Scanner s =new Scanner(System.in)){
	int età = s.nextInt();
System.out.println("l'età è "+ età)
}
	if (età<4){...}
}
}
} 
```

```java
WHILE(e)i
array in java int[] int[][]
new int [7][3];
3+m[i][j]
```

Verifica di un quadrato magico

### I/O + ARGS,List<…>

Object,String,Number

Animale a =new Cane(”Bau”)

Dispatching: se io se scrivo a=failverso() apparent or actuald

Object o=new Cane(”bau”)

```java
((Cane)o).faileVerso()
```

## Astrazione procedurale

Ci aiuta a cogliere gli elementi che ci servono e a considerare uguali cose che non lo sono.
Utilizzando requires andiamo a definire gli argomenti da poter utilizzare all'interno del metodo, se si utilizzassero argomenti differenti da quelli de requires si avranno effetti non conosciuti (crash, restituizione di un eventuale exception).

- **Astrazione per parametrizzazione:** eliminazione dei dettagli uguali che distinguono le realizzazioni in modo da generalizzare. andiamo a prendere i dettagli uguali e li andiamo a raggruppare
- **Astrazione per fattorizzazione:**
- **Astrazione per specificazione:** interesse su cosa si fa non sul come. Viene stipulato un “contratto” tra ideatore e user per cui dato un certo input il codice funzionerà sempre.

**Località:** a chi scrive non interessa la zona di modifica, all’utilizzatore non interessa il come viene fatto un certo lavoro, l’utilizzatore della funzione dispone del contratto nel quale vengono scritte le informazioni principali. 

**Modificabilità:** manutenzione, se ho sbagliato qualcosa e nel contratto è giusto ho sbagliato qualcosa non nel contratto ma nel codice, si può mantenere un codice senza impattare il contratto

Utilizzando **_Throws_** in coda al codice il programma solleva un'eccezione in caso di problemi.
--> Sollevare ``java THROW new E()``
#### Eccezioni
- Checked
- Unchecked


## Pacchetti

Un **package** in Java permette di raggruppare in un'unica entità complessa classi Java logicamente correlate.

## “Schema” e Javadoc - I magici tre

Utilizzo tre clausule:

- Requires: alcuni valori dati in input possono verificarlo
- Effects: output
- Modifies: Modifica x, non bisogna mettere in input il valore originale

Commenti con /** …*/ il compilatore prende quello che si trova all’interno come descrizione javadoc. La parte di **EFFECTS** che riguarda la parte di **MODIFIES.**

**@DARAM** N ….,(requires) sull’elenco dei parametri può essere messo requires, **DEVE** esserci quello specifico parametro

```java

/**
* Classe di utilità per il calcolo delle radici quadrate.
*/

public class Radici{

	public static double radiceParziale(double x){
			/*...*/
			return x;
}
}
```

Prima penso al design e a cosa deve fare il programma poi lo implemento

### Criteri

- Minimamente vincolanti: tanto più il contratto è vincolante più difficile diventa programmarlo, bisogna si dare vincoli ma non incatenare troppo il programmatore.
    - no algo
    - prestazioni
    - Sottospecifica
    - non-determinismo
    - Generalità
    - chiarezza e semplicità

- **Parziale/totale:** un programma si dice parziale se non rispetta totalmente il contratto, totale se lo rispetta completamente.

- Graceful degradation

## Eccezioni

Servono a segnalare eventuali problemi presenti nel programma.

Dove scrivere della presenza delle eccezioni?

Elenco in EFF, tu puoi darmi qualsiasi cosa in ingresso ma farò qualcosa di diverso (sollevare un’eccezione) in caso mettessi qualcosa di sbagliato (”non req”), eventuali effetti collaterali (modifiche) devono essere specificati poiché possibilmente distruttivi. 

## Astrazione dei Dati

Info→ rappresentazione
costruire, osservare e modificare

```java
Class Stud{
	Campi
	costruttori
	Metodi
}
List <integer> elem;
1 elem!=null
2 null appartiene a list
3 Duplicati #per ora non ci interessa
4 ordine #per ora non ci interessa
```

Come si specificano?
Astrazione per parametrizzazione (Dati)
Astrazione per specificazione (comportamenti)

Se ho un riferimento final la variabile non potrà più cambiare, la mutabilità nella specificazione non ha niente a che fare con la mutabilità dell’implementazione.

Private va a infierire sul nome variabile non sul suo contenuto, vuol dire che per evitare che qualcuno possa vedere/modificare il contenuto, esso non è visibile esternamente dalla classe in cui viene implementato.

```java
private IntSet(List<Integer> els){
		this.els = els;
}
public IntSet(List<Integer> els){
		this(new ArrayList<Integer>(other,els))
}
```
# Methods

I vari metodi appartenenti alla classe madre vengono ereditati/sovrascritti nella classe figlia.
si dividono in:
- ###### Costruttori
```java
class g {
public g(){}
}
```
- ##### Fabbricatori 
```java
class g{
public static c method(){}
}
```
- ##### Osservatori
```java
class g {
public c method(){}
}
```

`String toString()` restituisce una string

@Overrides viene letta dal compilatore


```java
@Overrides
<header>{
}
```

```java
@Override
public String toString(){
	StringBuilder sb = new StringBuilder();
	sb.append("Array: ");
	int i
}
```

```java
x.equals(y)=> x.hashcode==y.hashcode
```

se è mutabile devo garantire che sia ancora possibile l’uguaglianza.

```java
public boolean equals(Object o){
	if (o==this) return true;
	if (!(o instanceof Poly)) return false;
	Poly q = (Poly) o;
	if (degree() != q.degree()) return false;
	return Arrays.equals(coeff, q.coeff);
}

@Override
public int hashCode(){
	return Objects.hash(degree(),coeff);
}
```

implementare la classe frazione informazione: mantenere numeratori e denominatore. costruttori: bisogna riflettere (grande santini)

operazioni:+, *

Stare attenti al segno, riflettere se ha senso mantenere le soluzioni in forma ridotta o no (o entrambe) potrebbe avere senso un metodo che da frazione non ridotta la restituisce ridotta.

== & hashcode

toString()

MCD, valutare se sia il caso di sovraccaricare.

### Dati

“codice” Attributi metodi(costrutti)

RI,Af

“Mondo”

informazioni operazioni contratti

RI viene preservato

se prima{ RI(s)=si

⇒ dopo la { RI(s)=si

- costruttore
- Metodi - modificazionali - osservazionali

P.117

- mutability
- op. categories
    - constructors
    - fabbricators
    - observators
    - mutators
- adequacy

## Iteration Abstraction

“Iteration Protocol”

Generatore oggetto

```bash
boolean hasNect()
T next()
```

Iteratore Metodo

Gen<"T">fo

Implementazione 

- “Dove” come accedo alle info senza “esporre REF”
    - esterno (altro file)
    - interno (stesso file)

## Gerarchia dei tipi

(composizione e delega)

Se uno in un pezzo del codice rimpiazza un tipo con un sottotipo il funzionamento di tale programma non deve cambiare

### Classe Astratta e Classe Concreta

La presenza di un metodo astratto obbliga i sottotipi ad avere quel metodo astratto

## Estensione

- L’ereditarietà è utile, strumento reso possibile dal polimorfismo e dal dispatching, presenta però alcuni limiti
- Composizione + delega, approccio ortogonale a quello dell’ereditarietà

# Gerarchia dei tipi

### LSP
1. Rule signature
	Deve avere tutti i metodi di T con la stessa segnatura
1. metodi
	per ogni metodo il comportamento del figlio deve essere uguale a quella del padre
3. proprietà 
	se ho una proprietà descritta nel super-tipo devo averla anche nel sotto tipo