Le eccezioni vanno gestite in un certo punto del codice quando effettivamente si può fare qualcosa in conseguenza di quell'errore.
Quindi la domanda è: metti il blocco `try{ ... } catch(...) { ... }` nella parte di corpo di funzione che può potenzialmente generare un'eccezione, oppure lo metto nel main, dove la funzione che può generare un'eccezione viene lanciata?
Con il ramo `catch` viene fatto il recovery degli errori. Questo significa che è successo qualcosa, e per sistemarlo devo lasciare il mio programma in uno stato potenzialmente funzionante.

La risposta alla domanda, la troviamo guardando quale parte di codice smetterebbe di funzionare a causa dell'eccezione generata.

> Esempio: data la funzione che clona una stringa e crea un dato dinamico per riuscire a passare il puntatore alla stringa clonata. Gestiamo l'eccezione nel main perchè dopo c'è una print che dipende dall'output della nostra funzione, quindi è lì che dobbiamo mettere il blocco `try{ ... } catch(...) { ... }` per permettere al programma di funzionare.
```
char *clona_stringa(const char *str) { // ritorna un puntatore a char
    assert(str!=nullptr);
    unsigned int lengthstr = lunghezza_stringa(str);
    char *copia = new char[lengthstr + 1];  -> linea che genera l'eccezione
    char *inizio = copia;
    while(*str!='\0'){
        *inizio = *str;
        ++str;
        ++inizio;
    }
    *inizio = '\0'; 
    assert(lengthstr == lunghezza_stringa(copia));
    return copia;
 }

int main(int argc, char *argv[]){
    char *clone = nullptr;
	if (argc > 1){

		try{
		        clone = clona_stringa(argv[1]);
	        } catch (std::bad_alloc &e){                 --> gestiamo l'eccezione nel main
			 std::cerr << "Impossibile allocare la stringa." << std::endl;
	        }
	        std::cout << clone << std::endl;
	   }
	    else {
	        std::cerr << "ERRORE: Inserire almeno un argomento." << std::endl;
	    }

    delete[] clone; // per evitare di avere un memory leack
    clone = nullptr;
    return 0;
}
```

## Gestire internamente un'eccezione
Se decidiamo di gestire internamente l'eccezione generata, è importante comunicare al chiamante che un'eccezione è stata chiamata. 
Questo perchè il chiamante non è in grado di rendersi conto che un'eccezione è stata generata, di conseguenza è **necessario** dirgli che una funzione è fallita con un'eccezione.
Per fare ciò, ==**SI DEVE**== rilanciare ==un'altra eccezione al chiamante==, così che si può rendere conto che la funzione è fallita e di conseguenza può gestire l'eccezione generata.

> [!NOTE] Esempio di lancio eccezione al chiamante, dopo averla gestita internamente con try, catch
> 
	void f(){
	    int *a = nullptr, *b = nullptr;  
	    try{
	       b = new int[20000];
	   }
	    catch(std::bad_alloc &e){
	        delete[] a;
	        a = nullptr;
	        throw;     -> IMPORTANTISSIMO!!! Rimanda la stessa eccezione al chiamante
	    }
	    // todo
	    delete[] a;
	    a = nullptr;
	    delete[] b;
	}


> [!NOTE] Regola aurea
> Quando viene generata un'eccezione bisogna sempre domandarsi se occorre eliminare qualcosa, soprattutto se si è fatta una `new`.

## Gerarchia delle eccezioni
Se abbiamo diversi blocchi try, catch l'eccezione viene intercettata dal blocco che cattura l'eccezione più specifica.


