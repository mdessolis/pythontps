# Moduli fondamentali di Python #

Uno dei grandi punti di forza di Python è nella disponibilità di un grande numero di librerie (moduli) con strumenti che semplificano la programmazione nei campi più disparati, dal calcolo numerico alla gestione dei protocolli di rete, dalle strutture dati avanzate ai modelli di gestione dell'AI.

Qui riportiamo quelle fondamentali all'insegnamento della disciplina TPS e allo svolgimento degli esercizi.

Un elenco più completo lo si può trovare su https://docs.python.org/3.11/library/index.html.

Ricordiamo che per importare un modulo in python bisogna usare l'istruzione import in una delle sue forme:

La sola clausola import mette a disposizione tutte le funzioni interne al modulo, ma per accedere ad una delle funzioni bisogna sempre precederne il nome con il nome del modulo seguito dal punto.
    
    import numpy 
    
    print(numpy.arange(0,1,0.2)) # genera una sequenza da 0 a 1 escluso a intervalli di 0.2
    
Se si ha necessità di usare solo una funzione o una classe di un modulo allora si può usare la clausola from esplicitando quale funzione importare:
    
    from math import sqrt
    
    print(sqrt(5))
    
Oppure si possono importare tutte le funzioni di un modulo con l'asterisco
    
    from math import *
    
    # con il comando dir() possiamo vedere l'elenco di tutti i nomi importati e
    # messi a disposizione nel namespace
    dir()
    ['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__', 
    '__package__', '__spec__', 'acos', 'acosh', 'asin', 'asinh', 
    'atan', 'atan2', 'atanh', 'cbrt', 'ceil', 'comb', 'copysign', 
    'cos', 'cosh', 'degrees', 'dist', 'e', 'erf', 'erfc', 'exp', 
    'exp2', 'expm1', 'fabs', 'factorial', 'floor', 
    'fmod', 'frexp', 'fsum', 'gamma', 'gcd', 'hypot', 'inf', 'isclose', 
    'isfinite', 'isinf', 'isnan', 'isqrt', 'lcm', 'ldexp', 'lgamma', 
    'log', 'log10', 'log1p', 'log2', 'modf', 'nan', 
    'nextafter', 'perm', 'pi', 'pow', 'prod', 'radians', 
    'remainder', 'sin', 'sinh', 'sqrt', 'tan', 'tanh', 'tau', 'trunc', 'ulp']
    
Non tutti i moduli di Python sono disponibili immediatamente con l'installazione standard di Python, se il comando import dovesse dare errore, probabilmente c'è da scaricare nel sistema il modulo con il comando pip da eseguire da riga di comando:

    pip install numpy

## math ##

Il modulo math mette a disposizione diverse funzioni matematiche di base:

- **acos, acosh, asin, asinh, atan, atan2, atanh, cos, cosh, sin, sinh, tan, tanh**: *funzioni trigonometriche e iperboliche*
- **ceil(x)**: *il più piccolo intero maggiore o uguale a x*
- **comb(n,k)**: *combinazioni di n elementi in classe k*
- **e**: *esponenziale 2.718281828459045* 
- **exp(x)**: *e\*\*x*
- **factorial(x)**: *fattoriale di x*
- **floor(x)**: *il più grande intero minore o uguale a x*
- **fmod(x,y)**: *resto della divisione tra x e y, con x e y float*
- **fsum(iterable)**: *somma di valori float più precisa rispetto sum*
- **gcd(a,b)**: *massimo comun divisore tra a e b*
- **isclose(a,b, rel_tol=tolleranza, abs_tol=tolleranza)**: *True se a e b hanno una differenza massima in % di tolleranza o una differenza assoluta di tolleranza* 
- **isfinite(x)**: *True se x non è inf o NaN*
- **isinf(x)**: *True se x è inf, positivo o negativo*
- **isnan(x)**: *True se x è NaN*
- **lcm(a,b)**: *minimo comune multiplo tra a e b*
- **log(x), log10(x), log2(x)**: *logaritmi*
- **modf(x)**: *tupla (f,i) con i parte intera di x e f parte decimale* 
- **nextafter(x,y)**: *successivo numero float per andare da x a y*
- **perm(n,k)**: *Permutazioni di n elementi in classe k*
- **pi**: *PI greco*
- **pow(a,b)**: *a^b* 
- **prod(iterable)**: *Prodotto di una serie di valori*
- **degrees(r), radians(g)**: *Conversione gardi/radianti* 
- **sqrt(x)**: *Radice quadrata di x*
- **trunc(x)**: *Parte intera di x*

### Esempi ###

    from math import isclose
    
    def f(x):
        return x**3-3*x+5
        
    def search_zeros(f, a, b, step): # algoritmo non efficiente, ce ne sono migliori
        x = a
        while x < b:
            if isclose(f(x), 0, abs_tol=0.0001):
                print(f"Found f({x:.2f}) = {f(x):.2f}")
            x += step
        
    search_zeroes(f, 0, 1, 0.001) # cerca tutti gli zeri di f nell'intervallo [0,1[
    
    
## time ##

Il modulo time mette a disposizione alcune funzioni di accesso all'ora di sistema ed è molto comodo quindi per calcolare ad esempio i tempi di esecuzione di una funzione. Questo modulo fa parte dell'installazione di base di Python.

    import time
    
    """
    time() restituisce un valore float che rappresenta il numero di secondi trascorsi dal 1/1/1970 (Epoch)
    
    questa funzione è utile per calcolare ad esempio il tempo di esecuzione di una funzione
    """
    time.time()

    # esempio
    inizio = time.time()
    calcolo()
    tempo = time.time()-inizio
    print (f"calcolo() ha impiegato {tempo:.2f} secondi")
