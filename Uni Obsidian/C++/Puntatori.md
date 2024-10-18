Un puntatore è sempre legato al tipo di dato a cui punta.
Se vogliamo accedere ad un dato intero il puntatore che useremo per accedervi sarà fatto così:
```
int *iptr; //è un puntatore non inizializzato, non ha un valore iniziale che punta ad una variabile di tipo intero
```
Tutte le variabili non inizializzate in C++ contengono valori a caso.
Un puntatore che punta **a caso** (non inizializzato), **E' IL MALE ASSOLUTO**. E' molto pericoloso perchè può puntare a **qualsiasi area di memoria**.
E' quindi bene inizializzare sempre un puntatore, solitamente si usa un indirizzo fittizzio per far si che il puntatore punti a *null* (0).
```
int *iptr = nullptr;
```
E' buona cosa inizializzare sempre un puntatore a null.

Per far riferimento a

Quando si usano i puntatori si stanno usando 2 informazioni:
1. il puntatore
2. il dato puntato

**Definizione:**
Il puntatore è un dato speciale che contiene un indirizzo di memoria e mi permette di accedere in modo **indiretto** ad un dato.

Può essere che in puntatore non inizializzato riferisca ad un'aria di memoria **fuori dal processo corrente**, il problema è se usiamo quel puntatore: il sistema operativo ucciderà quel processo. Se lo si usa può succedere qualunque cosa. 

## Come usiamo i puntatori?
Per usare i puntatori, e accedere al dato puntato, occorre deferenziare il puntatore.
Per **deferenziare** un puntatore bisogna spostare il puntatore (di base significa "vado alla variabile puntata").
```
int j = 789;
int *iptr2 = j;
*iptr; // j -> ho deferenziato il puntatore, è come se scrivessi j (alias)
```
**Deferenziare un valore** significa risalire al dato puntato, e quindi usare il valore del dato puntato.

**NOTA BENE:**
Non usare mai un puntatore che punta al tipo void, perchè può puntare a qualsiasi tipo di variabile.
```
// puntatore good a void
void *good; // non farlo mai
```
Il puntatore a void, essendo un non-tipo, può essere usato per fare un po' di "porcherie": manipolare un pezzo di dato come se fosse di un tipo diverso.

### Dato condiviso
Cedere e condividere un dato ad un'altra entità che vive da un'altra parte nel mio codice.
Tra puntatori si condividono dati tra diverse entità in diversi punti del codice.
Posso quindi modificare il dato tramite più puntatori.
```
// d è condiviso dai puntatori *dpdr e *dpdr2*
double d = 3.14;
double *dpdr = &d;
double *dpdr2 = &d;
```
### Puntatore + intero
Se sommo un numero intero di byte, ottengo un nuovo puntatore, che ha un nuovo indirizzo.
Partendo dall'indirizzo di memoria del puntatore, il nuovo indirizzo contenuto nel puntatore sarà pari all'**indirizzo del puntatore + N * sizeof(double)**.
```
int N = 3;
int dptr2 + N; 
// è un puntatore ad un nuovo indirizzo che vale
// indirizzo contenuto in dptr + N * sizeof(double)
```
Questo perchè la grandezza di un double è di 8 byte, quindi lo usiamo per allinearci ad una locazione di memoria realmente esistente.

### Aritmetica dei puntatori
Quando vogliamo manipolare un array di dati.
E' facilissimo causare errori di accesso della memoria.
```
double *dptr3 = dptr2 +1;
// punta ad un altro dpuble che può non esistere
```

L'errore generato dal sistema operativo è di tipo **access error segmentation fault**:

```
// probabilmente così punteremo ad un indirizzo al di fuori del processo del programma
dptr3 = dpdr2 + 100000000000; 
*dptr3 = 90;
```
Dovrebbe dare errore, il sistema operativo dovrebbe bloccarti perchè dptr3 punta ad un indirizzo al di fuori dell'area di indirizzi del processo del programma.


```
dptr3++;
dptr3--;
dpdr2 - dpdr; // numero di dati di tipo double tra i due indirizzi
```
Sottrazione tra puntatori, danno il numero di dati che vivono in mezzo tra questi due indirizzi, non gli indirizzi.

```
dpdr2 + dpdr; // non ha senso, e da errore
```

Un puntatore a un dato qualunque ha sempre la dimensione del bus degli indirizzi della ram (64 byte)

I puntatori sono due entità: il puntatore stesso o il dato puntato.

