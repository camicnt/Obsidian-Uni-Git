La ***programmazione dinamica*** , come il metodo divide et impera, risolve problemi combinando le soluzioni dei sotto problemi. 
Gli algoritmi *divide et impera* suddividono un problema in *sotto problemi indipendenti*, risolvono in modo ricorsivo i sotto problemi e combinano le soluzioni per risolvere il problema originale.
La **programmazione dinamica**, invece può essere applicata quando <u>i sotto problemi NON sono indipendenti</u>, ovvero quando *i sotto problemi hanno in comune dei sotto problemi*.

In questo contesto un algoritmo divide et impera svolge molto più lavoro del necessario, risolvendo ripetutamente i sotto problemi comuni. Un algoritmo di programmazione dinamica risolve ciascun sotto problema una sola volta e salva la soluzione in una **tabella**, evitando di ricalcolare la soluzione ogni volta che si ripresenta il sotto problema.

La programmazione dinamica si applica tipicamente ai ***problemi di ottimizzazione***. 
## **La più lunga sottosequenza comune -> LCS**
Una **sequenza** $X =\space< x_{1}, \space x_{2}, \space... , \space x_{n} >$ è un insieme di simboli appartenente ad un alfabeto, $x_{i} \in \Sigma$.
Una sottosequenza di una data sequenza è la sequenza stessa alla quale *sono stati tolti zero o più elementi*. 
Data una sequenza $X =\space< x_{1}, \space x_{2}, \space... , \space x_{n} >$*, un'altra sequenza $Z =\space < z_{1},\space z_{2}, \space ... , \space z_{k} >$ è una ***sottosequenza*** di $X$ se esiste una sequenza *strettamente crescente* $<i_{1}, \space i_{2},\space ... , \space i_{k}>$ di indici di $X$ tale che per ogni $j = 1, \space 2 ,\space... , \space k,$ si ha $x_{i_{j}} = z_{j}$ .

Date due sequenze $X$ e $Y$, diciamo che una sequenza $Z$ è ***sottosequenza comune*** di $X$ e $Y$ se e solo se $Z$ è una *sottosequenza di entrambe le sequenze $X$ e $Y$*. 

Nel problema della ***più lunga sottosequenza comune*** sono fate due sequenze $X =\space < x_{1}, \space x_{2},\space ... , \space x_{m} >$ e $Y  =\space < y_{1}, \space y_{2},\space ... ,\space y_{n} >$ e si vuole trovare una <u>sottosequenza comune di lunghezza massima</u> che è comune a $X$ e $Y$.
### Fase 1: algoritmo forza bruta 
##### Caratterizzare la più lunga sottosequenza comune
Una **tecnica forza bruta** per risolvere il problema dell'**LCS** consiste nell'enumerare tutte le sottosequenze di $X$ e controllare le singole sottosequenze per vedere se sono anche sottosequenze di $Y$, *tenendo traccia della più lunga sottosequenza trovata.* 
Ogni sottosequenza di $X$ corrisponde a un <u>sottoinsieme degli indici</u> {${1, 2, ... , m}$} di $X$. 
Ci sono $2^{m}$ sottosequenze di $X$, quindi questo approccio richiede un **tempo esponenziale**, il che lo rende inutilizzabile.
Tuttavia il problema dell'LCS gode della **proprietà della sottostruttura ottima**: i sottoproblemi corrispondono a coppie di "**prefissi**" delle due sequenze di input.
Più precisamente, data una sequenza $X =\space < x_{1}, \space x_{2},\space ... ,\space x_{m} >$ definiamo $X_{i} = \space< x_{1}, \space x_{2}, \space ... , x_{i}>$ *l'i-esimo **prefisso** di $X$ per $i = 0, 1, 2, ... , m$.

> [!Esempio]
> se $X = <A, B, C , B, D, A, B>$, allora $X_{4} = <A, B, C, B>$ e $X_{0}$ è la **stringa vuota**.
### Teorema: sottostruttura ottima di una LCS
Siano $X =\space< x_{1}, \space x_{2},\space ... , \space x_{m} >$ e $Y =\space < y_{1}, \space  y_{2}, \space ... ,\space  y_{n}>$ le sequenze; sia $Z =\space <_{1}, z_{2}, \space ... , \space z_{z}>$ una qualsiasi **LCS** di $X$ e $Y$.
1. Se $x_{m} = y_{n}$ , allora $z_{k} = x_{m} = y_{n}$ e $Z_{(k - 1)}$ è una LCS di $X_{(m-1)}$ e $Y_{(n-1)}$.
2.  Se $x_{m} \neq  y_{n}$ , allora $z_{k} \neq x_{m}$ implica che $Z$ è una LCS di $X_{(m-1)}$ e $Y$.
3.  Se $x_{m} \neq  y_{n}$ , allora $z_{k} \neq y_{n}$ implica che $Z$ è una LCS di $X$ e di $Y_{(n-1)}$.
##### Dimostrazione
 1. 

