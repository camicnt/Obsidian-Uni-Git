Un **array primitivo statico** è una sequenza di dati non interrotta e dello stesso tipo, i dati sono quindi salvati in un'area di memoria contigua, così da permettere un accesso sicuro ai dati tramite puntatori.
Per evitare errori ed eccezioni quando si legge un array primitivo,  e non puntare ad una cella di memoria che non esiste (dopo l'ultimo elemento dell'array), esiste una cella ulteriore che può essere usata nei cicli per segnare la fine dell'array.

Allocazione contigua di dati.
Di base gli array non sono inizializzati.
Per inizializzare un array, occorre inizializzare ogni cella dell'array uno per uno. E' possibile inizializzare in fase di istanziazione dell'array.

```
int array[4] = {1, 2, 3, 4}; // array statico di dimensione 4
```
La dimensione di un array statico non potrà mai essere cambiata nella vita di un array.
Per riempire tutte le cellette dell'array in modo agevole devo usare un ciclo:

```
int array[10];
for (int i = 0; i < 10; ++i) {    // è più efficiente fare ++i al posto di i++
	array[i] = i;
	std::cout << array[i] << std::endl;
}
```


Gli array sono dati primitivi, non sono classi e non sono oggetti, quindi l'assegnamento di array primitivi non è permesso.
In C++ gli array non hanno nessun meccanismo di **index put of bounds detection** quindi non possiamo capire se abbiamo puntato ad un'area di memoria al di fuori dell'array (quindi casiniii).


```
char array[3]; // non inizializzato
char array2[3] = {'a', 'b', 'c'}; // inizializzazione
char array3[3] = {'d', 'e'}; // inizializzazione parziale
int array4[] = {1, 2, 3, 4}; // dimensione automatica

array1 = array2; // ERRORE
array2 = {'p', 'q','r'}; //ERRORE
array3[0] = 'a'; // OK
```

## Array e puntatori
Un array non è un puntatore e non è un indirizzo. 
Ho bisogno di un puntatore per puntare ad un dato dell'array.

```
int array[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
int *p = array;
std::cout << *p << std::endl; // derefenzio il puntatore, p punta a 0

// forma esplicita
int *p2 = &(array[0]); // stessa cosa di prima
std::cout << *p << std::endl;
```

### Stampa di un array con un puntatore
Dato il nostro array e il nostro puntatore:
```
int array[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
int *ptr = array;
```

#### Soluzione 1) stampa array con indice i + 1
```
for (int i = 0; i < 10; ++i) {  
	array[i] = i;
	std::cout << array[i] << std::endl;
```
#### Soluzione 2) Stampa con puntatore ptr +1
"p" è un puntatore a interi, che viene spostato di **1 * sizeof(int)**, quindi il puntatore si sposta da una cella all'altra perchè * sizeof(int) 
```
for(int i = 0; i < 10; ++i){
	std::cout << *(ptr + i) << std::endl; 
}
```

#### Soluzione 3) Stampa con puntatore ptr
**NOTA BENE:** Per evitare errori ed eccezioni quando si legge un array primitivo,  e non puntare ad una cella di memoria che *non esiste* (**dopo l'ultimo elemento** dell'array), esiste una cella ulteriore che può essere usata nei cicli per segnare la fine dell'array.
```
for(; ptr <= &array[9]; ptr++;) {   // &array[9] -> indirizzo della cella 9
	std::cout << *ptr << std::cout;
}
```
Avrei potuto anche scrivere *for( ; ptr < &array[10]; ptr++)* per dirgli di uscire alla cella dell'array che non esiste, ma possiamo usare come "sentinella".

Possiamo anche usare un puntatore che ci indica l'indirizzo dell'ultima cella dell'array, in questo caso è il puntatore end. 
```
for(int *end = &array[9]; ptr <= end; ptr++){ 
	std::cout << *(ptr) << std::endl;*
}
```

### Array multidimensionali
```
int array2[3][2] = {{1, 2}, {3, 4}, {5, 6}}; // 3 righe e 2 colonne
array2[1][1] = 90; // assegnamo 90 alla cella (i, j) = (1, 1)
```
Dato che questo è un array di array di interi, di conseguenza dobbiamo inizializzare uno ad uno i sottoarray usando le graffe { }. In questo esempio abbiamo 3 righe e 2 colone, di conseguenza abbiamo 3 sottoarray da 2 elementi.

Una cosa che non è possibile fare è usare un puntatore monodimensionale per puntare ad un array multidimensionale.
```
int *ptr2 = array2; // NO DA ERRORE

int (*ptr2)[2] = array2; // corretta scrittura di un puntatore bidimensionale
```

## Come leggere le variabili
```
int array2[3][2] = {{1, 2}, {3, 4}, {5, 6}};
 5   2  1   4      3      // ordine con la quale leggo
int (*ptr2)[2] = array2;
int array3[5][3][10];
int (*ptr3)[3][10] = array3;
int *ptrx[2];
```
**Regola**: parto dalla variabile, poi vado a destra, mi fermo quando trovo una parentesi tonda, allora vaso a sinistra, mi fermo quando trovo una parentesi tonda, poi vado di nuovo a destra, poi a sinistra, etc...

- Ptr2 è un puntatore a un array di 2 interi.
- Ptr3 è un puntatore di un array di array di interi. 
- Ptrx è un array di due puntatori interi.

```
std::cout *ptr2 << std::endl; // stampa l'indirizzo della cella (0, 0)
std::cout **ptr2 << std::endl; // stampa il valore della cella (0, 0), che è 1
std::cout *(*ptr2 +1) << std::endl; // stampa il valore nella cella (0, 1), che è 2
									// * fuori dalla parentesi indica che stiamo deferenziando (*ptr2 +1)
									// quindi stiamo stampando il suo valore 
```

### Stampare un array bidimensionale
#### Stampa array2 con gli indici
```
for(int i = 0; i < 2; ++i){
	for(int j = 0; j < 1; ++j){
		std::cout << array2[i][j] << std::endl;
	}
}
```
#### Stampa array2 con i doppi puntatori
```
int array2[3][2] = {{1, 2}, {3, 4}, {5, 6}};
int (*ptr2)[2] = array2; // puntatore ad un array di 2 interi
// end è un puntatore ad un array di due interi
// l'array che cicla (ptr2) e l'end devono essere dello stesso tipo

for(int (*end)[2] = &array2[2]; ptr2 <= end; ++ptr2){
	int *start = *ptr2; // indirizzo di inizio
	int *end2 = *(ptr2 +1); // indirizzo di fine
	
	// devo andare dall'indirizzo 0 a quello successivo
	// start contiene l'inizio della riga 
	// 
	for(; start <= end2; start++){
		std::cout << *(start) << "/t";
	}
	std::cout << "/n";
}
```


