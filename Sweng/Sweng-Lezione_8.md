## `Bug tracking`

Tengono traccia e gestiscono tutte le segnalazioni  sui difetti di un software.
Hanno centralizzato le segnalazioni in modo tale da impedire il moltiplicarsi delle stesse. 
Il bug tracking era molto difficile sopratutto considerando il modello a cascata (poiché privo di backtracking).
Il concetto principale dei bug tracker è appunto la segnalazione o comunque la comunicazione tra vari developer riguardo possibili bug.

### Bug workflow e ciclo di vita (simile a FSM)

  
![Bug workflow](https://marcobuster.github.io/sweng/assets/06_bug-workflow.png)

### Unified Process

### Best practice

- Sviluppare iterativamente
- Gestire i requisiti
- Usare a


# Progettazione

### Refactoring
Come già detto quando andiamo a fare il refactoring del codice non dobbiamo modificare il funzionamento delle feature presenti (fase invisibile al cliente) e inoltre non possiamo aggiungere dei test rispetto alla fase verde appena raggiunta.

### Design Knowledge
Dove la salviamo? 
0. in memoria
1. nei documenti di design (scritti in linguaggio naturale)
2. le piattaforme di discussione
3. UML
4. nel codice stesso

### Come condividiamo
0. metodi
1. design pattern
2. principi, a cui punteremo molto nel corso.