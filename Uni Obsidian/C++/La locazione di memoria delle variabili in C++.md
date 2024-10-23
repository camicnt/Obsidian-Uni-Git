## Il dato globale
Un **dato globale** è un dato che potenzialmente è visibile in qualunque punto del programma ed è allocato in una regione di memoria del nostro eseguibile predefinita. un dato globale nasce con la creazione del programma e viene rimosso dalla memoria quando il programma termina. Un dato globale si alloca al di fuori di qualsiasi funzione.
Una variabile globale può essere usata in qualsiasi file cpp se viene dichiarata anche in altri file cpp, dichiarandola nel file header degli altri file. Per fare questo usiamo `extern`.

```
int pippo = 20; // definizione
extern int pippo; // dichiarazione
```
Le variabili globali hanno una "vita globale" rispetto al programma.

## Variabili locali
Le **variabili locali** vengono definite all'interno di funzioni e hanno vita solo all'interno della funzione in cui sono usate. Sono anche dette **variabili automatiche** perchè sono dati automatici, nascono a richiesta e **automaticamente** muoiono, vengono tolte dalla memoria in automatico quando escono di **scope**; ossia quando si esce dalle parentesi graffe della funzione in cui è nata.
Le variabili locali sono allocate nello **stack** che è una memoria separata associata al nostro processo e contiene tutte le variabili locali del processo. Lo stack è dimensionato per poter contenere un certo numero di **variabili ==automatiche**== (variabili **locali alloccate sullo stack**), e quando viene riempito blocca tutto il programma (succede con i programmi *ricorsivi* che generano tante variabili automatiche).

## Variabili statiche (ibride)
Le **variabili statiche** sono locali, ma la keyword `static` da alla variabile una **vita globale**, quindi possiamo usare la variabile nel suo scope, ma quando usciamo dallo scope non viene eliminata (non muore fuori dalla funzione in cui è dichiarata).
Le variabili statiche preservano il loro vecchio valore e muoiono quando il programma muore.


```
#import <iostream>
void f(){
    static int z = 0; // definizione di una variabile statica
    std::cout << "z: " << z << std::endl;
    z = z + 10;
}

int main(){
	f(); // stampa z : 0
    f(); // stampa z : 10 // perchè la definizione viene fatta 1 sola volta, mantiene il valore vecchio della variabile se viene riutilizzata, perchè è statica
}
```

## Dati dinamici
I **dati dinamici** sono allocati nella **RAM** (se c'è spazio, normalmente c'è) e non nello stack. Vengono allocati attraverso una keyword speciale **==new==**. Il risultato dell'operazione new restituisce un **indirizzo di memoria**, quindi usare i puntatori è l'unico modo per ricondurci ad un dato dinamico allocato in RAM (non stack!!), e poi scriveremo il dato in RAM tramite il puntatore.
```
double *p = new double; 

/** questo puntatore è un dato automatico che vive sullo stack e viene rimosso dalla memoria quando usciamo dal main, quello che ci attacchiamo con la new NON MUORE se usciamo dallo scope della variabile. Dobbiamo rimuoverlo NOI!!
*/

delete p; // rimuovere il dato dinamico
p = nullptr;
```
 Un dato dinamico nasce a richiesta ma non muore automaticamente: **non sono dati automatici**.
 I dati dinamici nascono a richiesta e muoiono a richiesta, quindi dobbiamo richiedere la loro eliminazione.

**Memory leak** -> il dato dinamico viene lasciato in RAM e non viene rimosso.
Per rimuovere un dato dinamico si usa **==delete==**.  

> [!NOTE] Regola aurea: dopo delete, nullptr
> Dopo la delete di un puntatore, il dato allocato in RAM viene eliminato, ma il puntatore p (dell'esempio) punta ancora alla cella di memoria in cui era salvato il dato dinamico, quindi occorre fare `p = nullptr;` così che il puntatore non  punti più a nessuna cella (altrimenti sarebbe pericoloso, perchè p potrebbe puntare a qualsiasi cosa).

**mulloc** e **calloc** sono funzioni C di basso livello e non sono in grado di gestire la allocazione e rimozione delle classi in memoria. In C++ viene usata la keyword **new** e **delate**.

##### Ricapitolando
I dati automatici (sullo stack) vengono deallocati automaticamente all’uscita di scope. I dati dinamici (sullo heap) vengono deallocati solo tramite delete esplicito. Non esiste Garbage Collection.
#### Allocare un'array di dati dinamici
Occorre usare `delete[]` se abbiamo un array di dati dinamici.
```
double *p = new double[1000000];
delete[] p; 
p = nullptr;
```
