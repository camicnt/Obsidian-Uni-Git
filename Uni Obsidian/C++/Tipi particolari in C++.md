## Tipo Reference
I **reference** vanno **obbligatoriamente** **inizializzati**! Non è possibile che non facciano riferimento a nulla.

```
int  appoggio = 999;
int &ref = appoggio; // ref = = = appoggio
ref = 0; // appoggio = 0;
```
Il reference è un'**alias** di una variabile, tutto quello che viene fatto a ref viene fatto ad appoggio, quando usiamo ref usiamo appoggio.
Un reference è un "puntatore mascherato" che non si deferenzia. E' un modo più comodo per accedere ai dati. 
Noi passiamo alle funzioni dei dati per reference, quindi condividiamo quei dati con i reference.
Essendo un reference sempre inizializzato, è sempre valido e ha sempre un valore. Non restituirà mai un indirizzo strano.
Non ha senso usare un reference con una variabile che si trova nello stesso scope, perchè basterebbe usare la variabile stessa.
#### Nota bene: &
- Se & viene accostata ad una variabile non si intende l'indirizzo di un puntatore, ma si vuole creare una variabile reference.
- Quando un reference riferisce una certa variabile, resta sempre legato alla variabile che riferisce. Tuttavia il suo valore può cambiare, ma non cambierà mai la variabile che referenzia, riferirà sempre uno e un solo dato.
- Esiste un puntatore a void ma non esiste un reference che referenzia una variabile void.

## Tipo Struct
Una **struct** è un tipo di dato che aggrega altri tipi di dati. Possiamo definire dei tipi custom.

**CHIUDERE LA STRUCT CON }; !!!**

```
struct pippo {
	int i;
	double d;
	char c;
}; 

pippo p; // inizializzazione della struct pippo
p.i; // accediamo al dato i con la dot notation
pippo p2 = {5, 3.14, 'a'}; // istanziazione + inizializzazione della struct pippo p2
```
Una struct e una classe dal punto di vista di C++ sono la stessa cosa. La differenza è che una struct è **pubblica** e invece la classe è **privata**, quindi tutti possono accedere e modificare i valori delle variabili di una struct.
**NOTA BENE**: l'ordine di valori delle variabili che assegniamo ad una struct in fase di inizializzazione è importante!!! 

##### Per indicare un puntatore a struct usiamo - >
```
pippo *pptr = &p2;
pptr - > i; // leggo/scrivo l'intero tramite puntatore
(*pptr).i; // leggo/scrivo l'intero tramite struct
std::cout << sizeof(pippo) << std::endl;
```

da quanto abbiamo visto sul compilatore i dati che compongono la struct occupavano: int = 4, double = 8, char = 1, ma tutta la struct pippo pesa 24. Questo perchè il compilatore ha deciso che è più efficiente impacchettare i dati in 8 + 8 + 8 byte.
Se cambiassi l'ordine dei dati all'interno della struct può cambiare la dimensione della struct. Ad esempio se avessimo in ordine int =4, char = 1 e double = 8, il compilatore ha deciso di inglobare int e char che pesano 5 byte, in un pacchetto da 8 byte. Di conseguenza la struct peserà 16 byte in memoria.
**IMPORTANTE**: è buona prassi ordinare in ordine di "peso" in memoria, i tipi dei dati che fanno parte della struct. Nel nostro esempio char, int e infine double. 
**padding dei dati** -> impacchettare i dati con dei byte che non servono a niente per completare il pacchetto

##### Direttiva del processore
```
#pragma pack(push, 1)
struct pippo{
	char c;
	int i;
	double d;
};
#pragma pack(pop)
```
La **direttiva del processore** serve a forzare il compilatore a non usare il padding, così da usare *esattamente* lo spazio necessario in memoria
Se int occupa 4 byte, char occupa 1 byte e double occupa 8 byte, lo spazio che il compilatore occuperà ora sarà 13 byte.
## Tipo Enumerativo
Il tipo **enum** permette di usare dei nomi di comodo a delle variabili al posto di usare le costanti.
Sono un modo per rappresentare un'informazione finita tramite dei nomi.
```
enum giorno {lun =1, mar = 2, mer = 3, gio =4, ven = 5, sab = 6, dom =7};
giorno g = lun; // in questo caso quando scriviamo lun è come scrivere 1 (il suo valore)
// oppure
enum giorno {lun, mar, mer, gio, ven, sab, dom};
giorno g = lun;
```
I nomi contenuti nella enum devono essere univoci.
I valori associati sono tipizzati.

## Keyword typedef
La **keyword typedef** di permette di dare un nome nuovo a un tipo di dato (a volte i dati sono fastidiosi da scrivere, tipo (* ptr2)[2]. 
**typedef   nome_vecchio   nome_nuovo**
```
typedef unsigned Long int uli; // avere dei nomi di dati più gestibili
uli pluto;
```
L'uso più serio di typedef è *nascondere un dato*.
## File header
Solitamente contiene:
- struct
- enumerazione
- typedef
**NOTA BENE:** usare **SEMRPE** le guardie ( #ifndef, #endif...) 

## Asserzioni
Un'**asserzione** è un test che si possono inserire nel codice e associamo a questo test una condizione che deve essere vera, se la condizione non è vera viene generato un errore a runtime (non è un'eccezione). Dunque, sono valutati a runtime.
Vengono usate per testare il codice, infatti sono test automatici che vengono valutati a runtime.

**Suggerimento:** riempire il codice di test, che verranno usati per valutare il codice a runtime.
```
#include <cassert>
unsigned int N = 0; // N sempre positivo perchè è unsigned
		assert(N>0); // test per contollare che N sia sempre positivo
```
Le asserzioni vengono compilate solo se il codice viene compilato in modalità debug, perchè sono test di debug. Spariscono dal codice se questo viene compilato in modalità ''release/olease/elise???''

Occorre controllare la correttezza dei parametri ricevuti da una funzione tramite asserzione, posta prima del body della funzione.
```
double nsqrt(double x, double epsilon) {
    assert(x>=0);
    assert (epsilon>0);
    ... // body
}
```
Le asserzioni sono una sorta di "contratto" tra noi, che implementiamo la libreria, e il programmatore che vuole usarla. Il programmatore, se vuole che il suo codice funzioni, deve sfruttare le asserzioni.

Le asserzioni usate prima del body di una funzione prendono il nome di **precondizioni**.
## Puntatori a funzione 
Sono usati per rendere il codice flessibile/generico.
```
//puntatore ad una funzione che prende in input un double e ritorna un double
double calcola_integrale_2(int N, double(*f)(double)){  

}
```
