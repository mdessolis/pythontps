# Moduli fondamentali di Python #

Uno dei grandi punti di forza di Python è nella disponibilità di un grande numero di librerie (moduli) con strumenti che semplificano la programmazione nei campi più disparati, dal calcolo numerico alla gestione dei protocolli di rete, dalle strutture dati avanzate ai modelli di gestione dell'AI.

Qui riportiamo quelle fondamentali all'insegnamento della disciplina TPS e allo svolgimento degli esercizi.

Ricordiamo che per importare un modulo in python bisogna usare l'istruzione import in una delle sue forme:

    """
    La sola clausola import mette a disposizione tutte le funzioni interne al modulo,
    ma per accedere ad una delle funzioni bisogna sempre precederne il nome con il nome
    del modulo seguito dal punto.
    """
    import numpy 
    
    print(numpy.arange(0,1,0.2)) # genera una sequenza da 0 a 1 escluso a intervalli di 0.2
    
    """
    Se si ha necessità di usare solo una funzione o una classe di un modulo allora si può
    usare la clausola from esplicitando quale funzione importare:
    """
    from math import sqrt
    
    print(sqrt(5))
    
    """
    Oppure si possono importare tutte le funzioni di un modulo con l'asterisco
    """
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

## time ##

La libreria time mette a disposizione alcune funzioni di accesso all'ora di sistema ed è molto comoda quindi per calcolare ad esempio i tempi di esecuzione di una funzione
