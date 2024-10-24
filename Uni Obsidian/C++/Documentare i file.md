1) descrizione della funzione
2) lista di parametri e valori di ritorno
3) precondizioni
4) return
```
/** -> apro il commento
	@brief Funzione che calcola la radice quadrata di un numero -> commento breve (una riga)

	Funzione che calcola la radice quadrata di un numero 
	reale positivo usando il metodo di Newton                 -> commento lungo

	@param x valore di input                                  -> parametri
	@param epsilon errore di approssimazione

	@pre x >= 0                                               -> asserzioni/precondizioni
	@pre epsilon>0

	@return la radice quadrata approssimata di x              -> return
*/ -> chiudo il commento
```
Solitamente su una singola riga si dice cosa fa la riga di codice seguente, con il commento breve.
Un **commento breve** può essere scritto anche usando il tag `@brief`.
Il commento breve deve stare su una sola riga.
##### Documentare parametri/precondizioni / asserzioni
Occorre esplicitare i parametri usando `@param`: es. `@param x Numero reale positivo di input`(valore  di input).
Posso scrivere esplicitamente la descrizione di un parametro, oppure la tengo più semplice e specifico i controlli menzionando le asserzioni, tramite `@pre epsilon>0`. 
```
/**
	@param x valore di input 
	@pre x>=0
*/
```
##### Documentare la return 
`@return la radice quadrata approssimata di x`
##### Postcondizioni
`@post len(str) == len(result)`
Sono delle condizioni che assolutamente devono valere, al termine dell'esecuzione del mio blocco di codice. Qualcosa che mi dica "tutto è andato bene".
Vengono fatte tramite delle asserzioni di controllo.

##### Lancio di [eccezioni](Eccezioni)
`@throw std::bad_alloc in caso di fallimento della new`
Il mio blocco di codice potrebbe generare un'eccezione, e la cosa va segnalata.
## File di progetto di Doxygen  
![[Pasted image 20241017102255.png]]
Metto il punto per indicare una qualsiasi cartella.

![[Pasted image 20241017102410.png]]
- all entities -> documento qualsiasi cosa
- include cross-referenced etc... -> documentazione HTML
- selezioniamo C++

**SELEZIONARE QUELLI IN ROSSO**
![[Pasted image 20241017102617.png]]
![[Pasted image 20241017102634.png]]

File >> save as >> Doxyfile >> salvato nella dyrectory corrente (**DOVE HAI I FILE SORGENTI**)

Per generare la documentazione scrivere sul **cmd**: `doxygen`

![[Pasted image 20241017103526.png]] 
La cartella `HTML` **DEVE ESISTERE**. Il file **files.html** contiene tutta la documentazione.
Per aggiornare i files, basta rieseguire doxygen.
Nel **Makefile** si può aggiungere un tag per generare anche la documentazione del codice.

## Documentare le funzioni
E' importante segnalare la necessità di rimuovere dei dati dalla memoria, che sono stati creati sullo heap e di conseguenza devono essere cancellati dalla memoria dal chiamante. 
Ad esempio se una funzione crea un dato dinamico, dobbiamo dire al chiamante, tramite documentazione, che quel dato deve essere cancellato.

**La cessione degli ownership deve essere indicata**
**La generazione di eccezioni deve essere indicata**

```
/*4. Scrivete una funzione che ritorna una copia di una stringa passata */
/**
 * Documentazione:
 * Crea una copia della stringa C di input.
 * La stringa creata è creata sullo heap e ceduta al chiamante che deve rimuoverla dalla memoria.
 *
 * @param srt stringa C di input
 * @return puntatore alla stringa clonata
 * @pre str != nullptr
 * @post len(str) == len(result)
 * @post str[i] == result[i] per i = 0 per len(str) -> controllo consigliato
 * @throw std::bad_alloc in caso di fallimento della new
**/

char *clona_stringa(const char *str) { // ritorna un puntatore a char
    assert(str!=nullptr);
    char *copia = new char[lunghezza_stringa(str) + 1];
    char *inizio = copia;
    while(*str!='\0'){
        *inizio = *str;
        ++str;
        ++inizio;
    }
    *inizio = '\0'; 

    assert(lunghezza_stringa(str) == lunghezza_stringa(copia));
  
    return copia;
}
```

