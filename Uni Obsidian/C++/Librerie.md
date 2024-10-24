## #include `<cmath>` e le librerie ibride "c... etc"
I file header ereditati dalla libreria Cmath vivono in "due mondi": tutte le funzionalità che vivono nelle librerie "ibride" che iniziano per "c..." vivono anche nel namespace std importato con `#include` `<iostream>`, quindi se importiamo `<iostream>` posso usare le funzioni della cmath senza std davanti.

```
/*
    #include <cmath>
    while(str < p){
    std::swap(*str, *p);
    ++std;
    --p;
    }
    */
```

## #include `<cassert>`
da importare per poter usare le [[Tipi particolari in C++|asserzioni]].

## #include `<algorithm>` 
Funzione `std::swap(* str, * p);`

## #Include `<new>`
[Eccezione](Eccezioni) `std::bad_alloc` 