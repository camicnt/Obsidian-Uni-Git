## Cmath e le librerie ibride "c... etc"
I file header ereditati dalla libreria Cmath vivono in "due mondi": tutte le funzionalità che vivono nelle librerie "ibride" che iniziano per "c..." vivono anche nel namespace std importato con #include <iostream>, quindi se importiamo <iostream> posso usare le funzioni della cmath senza std davanti.
