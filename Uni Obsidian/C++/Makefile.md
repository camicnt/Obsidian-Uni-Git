Il programma Make può essere usato per qualsiasi cosa, perchè è semplicemente un sistema che interpreta delle regole (e le regole possono essere qualsiasi cosa).
Deve contenere per primo il target finale del nostro progetto, quello che vogliamo tenere.
`nome_target.exe : file_oggetto` -> cosa ottengo : cosa uso

```
test_nsqrt.exe: test_nsqrt.o nsqrt.o
  g++ test_nsqrt.o nsqrt.o -o test_nsqrt.exe

test_nsqrt.o: test_nsqrt.cpp
  g++ -c test_nsqrt.cpp -o test_nsqrt.o

nsqrt.o: nsqrt.cpp
  g++ -c nsqrt.cpp -o nsqrt.o
```
Struttura del make: cosa vogliamo ottenere": " "ingrediente1" " " "ingrediente2" ...
Usare le TAB!!! (VS Code trasforma le tab in spazi, in automatico, è consigliato settare le tab al posto degli spazi).

Lui valuta se i file oggetto, che sono file intermedi, devono essere compilati.
Il make si accorge se un file deve essere compilato o meno, e per compilarlo deve applicare le regole del make.
La radice è l'eseguibile e i file oggetto sono i passi intermedi.
Il make va a ricercare a ritroso, se possiede già i file che gli richiediamo, se non li possiede va avanti a cercare di produrre il file corretto.
Il make è interessato ai file sorgenti o intermedi per realizzare i target, non si preoccupa dei file header perchè sono già inclusi nel cpp.
```
clean:
    rm *.o *.exe
```
