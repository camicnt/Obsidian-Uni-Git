Il passaggio di parametri a funzioni si ha quando vogliamo passare un parametro ad una funzione perché vogliamo che quel parametro venga usato dalla funzione stessa per eseguire una qualche operazione.
Il passaggio di parametri a funzioni in C++ ha la stessa semantica dell'inizializzazione di una variabile. Quindi quando noi passiamo un dato ad una funzione, a seconda di come viene passato, quel dato viene copiato nella variabile del parametro della funzione; quindi quella variabile viene inizializzata con il valore passato dalla funzione stessa.

Vi sono diversi modi per passare un parametro ad una funzione:
- per valore
- per puntatore
- per reference
Un dato può essere passato `const` o non `const`, quindi costanti o non costanti.

## Passaggio di parametri per valore
ESEMPIO: una volta che viene chiamata funct, si ha una nuova variabile sullo stack, la variabile v. La variabile v è una variabile **indipendente** da i. Quindi una volta che si è passato i, abbiamo **due parametri** in memoria con il valore 10.
```
voud funct (int v){
	v = 90;
};

int main(){
	 int i = 10;
	 funct(i);
}

```
Quando viene chiamata una funzione, si ha un cambio di contesto nel flusso di esecuzione del programma. Il flusso di esecuzione passa alla funzione stessa. Quindi prima della chiamata alla funzione stessa, si salva sullo stack lo stato dell'applicazione corrente, dopodiché si passa all'esecuzione della funzione. La funzione allocherà e deallocherà le variabili di lavoro e successivamente si tornerà al contesto di esecuzione principale.

Il **passaggio per valore** crea una copia del dato in memoria, indipendente da quello di partenza.