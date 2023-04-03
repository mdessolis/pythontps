# Python for TPS

## Sommario ##

- [Introduzione](#introduzione)
- [Principi del linguaggio](#principi-del-linguaggio)
   - [Commenti](#commenti)
   - [Variabili](#variabili)
      - [Variabili numeriche](#variabili-numeriche)
      - [Variabili stringa](#variabili-stringa)
      - [Formatted string](#formatted-string)
      - [Tuple](#tuple)
      - [Liste](#liste)
      - [Accedere agli elementi di liste e tuple](#accedere-agli-elementi-di-liste-e-tuple)
      - [Set](#set)
      - [Dictionary](#dictionary)
   - [Controllo del flusso](#controllo-del-flusso)
      - [if](#if)
      - [while](#while)
      - [for](#for)
      - [List comprehension](#list-comprehension)
      - [match](#match)
   - [Operatori e funzioni di base](#operatori-e-funzioni-di-base)
      - [Operatori di assegnamento](#operatori-di-assegnamento)
      - [Operatori condizionali](#operatori-condizionali) 
      - [if inline](#if-inline)
      - [Assegnazioni parallele](#assegnazioni-parallele)
   - [Funzioni](#funzioni)
      - [Passaggio di argomenti per riferimento o per valore](#passaggio-di-argomenti-per-riferimento-o-per-valore)
      - [Built-in functions](#built-in-functions)
   - [Classi e Oggetti](#classi-e-oggetti)

## Introduzione

Il linguaggio Python si è imposto negli ultimi anni per una notevole flessibilità nelle istruzioni e per una sempre più crescente disponibilità di librerie di ausilio alle problematiche più disparate, dalla matematica all'AI alla analisi delle reti.

In questa breve dispensa vedremo i fondamenti del linguaggio e diversi esempi di uso per lo studio di alcune tematiche legate all'insegnamento di **TPS** nelle classi quarte e quinte dell'articolazione **Informatica** dell'indirizzo **Informatica e Telecomunicazioni**.

## Principi del linguaggio

A differenza degli altri linguaggi di programmazione Python non usa parentesi graffe o altri simboli per rappresentare correttamente i blocchi di istruzione, ma l'indentazione. E' quindi fondamentale scrivere in modo ordinato le istruzioni rispettando rigorosamente l'indentazione, per convenzione di solito impostata a quattro spazi.

### Commenti ###

E' bene iniziare sempre ogni programma e ogni funzione con delle righe di commento. In Python per indicare i commenti multiriga si usano di solito tre virgolette o tre apici come delimitatori, tenendo però presente che gli stessi delimitatori possono essere usati anche nelle assegnazioni:

    """
    Questo è un commento in un programma
    """
    
    a = """
    Questa è una stringa
    su più righe assegnata alla variabile a
    """

I commenti su singola riga invece si scrivono preceduti dal carattere hash #

    """
    Questo è un commento in un programma
    """
    
    # Adesso assegniamo uno string literal alla variabile a
    a = """
    Questa è una stringa
    su più righe assegnata alla variabile a
    """
    
### Variabili ###

#### Variabili numeriche ####

Le variabili in Python non hanno necessità di dichiarazione preliminare del tipo, in quanto questo viene inferito dal valore assegnato. Quelle numeriche sono di tre tipi, **integer**, **float** e **complex**. E' da tenere presente che per le variabili intere non ci sono limiti al loro numero di cifre, mentre per quelle float dipende dall'implementazione ma in genere 2e306. Considerare anche che con assegnazioni successive una variabile può cambiare tipo e passare ad esempio da int a float. Esempi:

    a = 5
    type(a) # Mostra <class 'int'>
    
    a = a/2
    type(a) # Mostra <class 'float'>
    
    a = 87621836467784687346283746298374691823764978 # è sempre un intero
    
    a = 2e401
    a
    inf # se supera il limite di memorizzazione assegna il valore **inf**
    
E' bene precisare che le variabili hanno un comportamento differente rispetto ad altri linguaggi. Le variabili int, float (e così anche string) sono immutabili ed una assegnazione di un valore ad una variabile consiste nella creazione di un oggetto di un certo tipo e associazione di un nome all'oggetto. Se però si assegna un nuovo valore alla variabile non viene modificato l'oggetto ma ne viene creato uno nuovo.

Una prova di questo la possiamo avere usando la funzione id(variabile) che restituisce un intero identificatore univoco di una variabile:

    a = 5
    id(a) # mostra 140713457410984, ha creato un oggetto int e associato il nome a
    id(5) # mostra 140713457410984
    
    a += 1
    id(a) # mostra 140713457411016, è un oggetto int differente con associato il nome a
    id(6) # mostra 140713457411016
    
    b = 6
    id(b) # mostra 140713457411016
    

#### Variabili stringa ####

Le variabili stringa in Python sono immutabili, per cui si può assegnare un testo ad una variabile ma non si può modificarne parte ma solo riassegnare un nuovo testo.

    a = "Cuesta è una frase"
    
    """
    L'istruzione seguente restituisce errore, non si può modificare una lettera della stringa.
    'str' object does not support item assignment
    """
    a[0] = "Q" 
    
    """
    Questo è corretto perché riassegniamo l'intera stringa.
    a[1:] restituisce tutti i caratteri a partire dal secondo (v. liste)
    """
    a = "Q" + a[1:] 
    
Le variabili stringa sono anche considerate da Python come degli array (di caratteri) per cui possono essere usate come tali e si può accedere ai singoli caratteri con l'indice tra parentesi quadre oppure si possono usare alcuni costrutti di python per estrarre informazioni:

    a = "La donzelletta vien dalla campagna"
    
    len(a)      # restituisce 34
    a[1]        # restituisce 'a'
    'alla' in a # restituisce True ('alla' si trova dentro la stringa a)
    'Alla' in a # restituisce False('Alla' non si trova nella stringa a, la ricerca è case sensitive)
    for c in a: # esegue un ciclo for memorizzando in c una ad una tutte le lettere presenti in a

#### Formatted string ####

Le stringhe possono essere definite anche in modo formattato, cioè con dei codici che consentono l'inserimento di espressioni direttamente all'interno della stringa e del modo in cui devono essere mostrate.

Python offre diversi metodi per la formattazione delle stringhe ma noi ci limiteremo alla modalità definita nelle ultime versioni, in quanto più sintetica da scrivere.

Questa modalità consiste nel precedere le virgolette che racchiudono la stringa con la lettera "f" e inserire le espressioni all'interno di questa tra parentesi graffe:

    p = 15.3
    q = 12.78
    
    s = f"{p} * {q} = {p*q}" # memorizza in s la stringa '15.3 * 12.78 = 195.534'
    
    s = f"{p:.1} * {q:.1} = {p*q:.1}" # memorizza in s la stringa '2e+01 * 1e+01 = 2e+02'
    
    s = f"{p:.1f} * {q:.1f} = {p*q:.1f}" # memorizza in s la stringa '15.3 * 12.8 = 195.5'
    
    s = f"{p:.3f} * {q:.3f} = {p*q:.3f}" # memorizza in s la stringa '15.300 * 12.780 = 195.534'
    
    s = f"{p:15.3f} * {q:15.3f} = {p*q:15.3f}" 
    # memorizza in s la stringa '         15.300 *          12.780 =         195.534'
    
    f"{q:-^15}
    # crea una stringa di 15 caratteri con al centro il valore di q 
    # e riempita non di spazi ma di "-": '-----12.78-----'
    
    f"{q:^15.4f}"
    # crea una stringa di 15 caratteri con al centro il valore di q 
    # e spazi vuoti a destra e sinistra: '    12.7800    '
    
    f"{q:15.4f}"
    # crea una stringa di 15 caratteri con a destra il valore di q con 4 cifre decimali, 
    # a sinistra spazi: '        12.7800'
    
    a = 1500000
    f"{a:,}" # inserisce il separatore delle migliaia e restituisce '1,500,000'
    
    x = 0.3532
    f"{x:.2%}" # restituisce x in formato percentuale: '35.32%'
    
    t = 4
    f"{t:0>5}" # riempie di zeri non significativi e restituisce '00004'
    
    f"{t:0>5b}"# riempie di zeri non significativi e restituisce in binario: '00100'
    
#### Tuple ####

Le tuple sono delle variabili contenenti liste non modificabili di elementi. Questo significa che se vogliamo modificare un elemento della tupla ne dobbiamo creare una nuova con l'elemento modificato. 

E' invece possibile unire due o più tuple tra loro.

Per rappresentare una tupla si indicano gli elementi che la compongono racchiusi tra parentesi tonde.

    a = ("Milano", "Torino", "Bologna")
    
    a += ("Genova",) # aggiunge Genova alla tupla a (attenzione alla virgola finale, 
                     # se non messa non la considera una tupla!)
    
    a[0] # restituisce "Milano"
    
    len(a) # restituisce 4
    
    a = ("Napoli", ) + a[1:] 
    # ricrea la tupla a sostituendo il primo elemento con "Napoli" al posto di "Milano"
    # a[1:] restituisce tutti gli elementi a partire da quello di indice 1, quindi salta il primo
    
    a.count("Genova") # restituisce il numero di occorrenze di "Genova" all'interno della tupla a

#### Liste ####

Le liste sono simili agli array degli altri linguaggi di programmazione, quindi si usano per memorizzare diversi elementi in una variabile, accessibili mediante indice o iteratori e, a differenza delle tuple, sono modificabili.

    a = ["Milano", "Genova", "Bologna"]
    
    a.append("Genova") # aggiunge "Genova" in fondo alla lista
    
    a += ["Cagliari", "Bari"] # aggiunge due stringhe in fondo alla lista
    
    a[0] # restituisce "Milano"
    
    len(a) # restituisce 6
    
    a.count("Genova") # restituisce il numero di occorrenze di "Genova" all'interno di a, quindi 2
    
    a.sort() # riordina gli elementi della lista
    
    print(a) # mostra a video ["Bari", "Bologna", "Cagliari", "Genova", "Genova", "Milano" ]

    a.remove("Genova") # rimuove dalla lista a la prima occorrenza di "Genova" - messaggio di errore se non la trova
    
    a.pop(0) # rimuove dalla lista a il primo elemento e lo restituisce
    
    a.reverse() # inverte l'ordine degli elementi della lista a
    
    "Bologna" in a # restituisce True perché la stringa "Bologna" si trova nella lista a
    
#### Accedere agli elementi di liste e tuple ####

Una delle potenzialità di Python sta nella semplicità con cui si può accedere a singoli o gruppi di elementi delle liste o delle tuple. A differenza di altri linguaggi che richiedono tra parentesi quadre l'indicazione di un unico indice di accesso, in Python possiamo definire anche degli intervalli di accesso:

    v = [1,3,5,6,7,4,8]
    
    v[0] # restituisce 1
    
    v[4:] # restituisce [7,4,8] (dall'elemento di indice 4 in poi)
    
    v[:3] # restituisce [1,3] (dal primo elemento a quello di indice 3, escluso)
    
    v[-1] # restituisce 8, l'ultimo elemento
    
    v[:-2] # restituisce tutti gli elementi a parte gli ultimi due
    
    v[1:3] # restituisce gli elementi di indice 1 e 2, quindi [3,5]
    
    v[::2] # restituisce gli elementi di posizione zero e pari [1,5,7,8]
    
    v[1::2] # restituisce gli elementi di posizione dispari [3,6,4]

#### Set ####

I set sono degli elenchi di elementi non modificabili e non duplicati. Si rappresentano racchiudendo gli elementi tra parentesi graffe. 

Tenere presente che gli elementi sono disposti in ordine casuale quindi non si sa quale sequenza venga restituita in un ciclo di scansione o ad esempio eseguendo il metodo pop() che estrae un elemento a caso.

Sono molto comodi da usare in certi contesti perché semplificano molte operazioni che con liste o tuple richiederebbero procedure apposite.

    s = {"Milano", "Bologna", "Roma", "Bologna"}
    # crea un set di 3 elementi. Il quarto non viene considerato perché già presente
    
    len(s) # restituisce il numero di elementi del set s, quindi 3
    
    s.add("Napoli") # aggiunge un elemento al set s
    
    s.update({"Palermo", "Catania"}) # aggiorna il set s aggiungendo gli elementi del set {"Palermo", "Catania"}
    
    s.remove("Catania") # rimuove l'elemento "Catania" dal set s, errore se non lo trova
    
    s.pop() # rimuove un elemento dal set. Attenzione, l'elemento rimosso è random
    
    s = {"Milano", "Bologna", "Roma", "Bologna"}
    s2 = {"Bologna", "Milano", "Catania", "Avellino"}
    
    s.intersection(s2) # restituisce un set composto dall'intersezione di s con s2 - {"Bologna","Milano"}
    
    s.union(s2) # restituisce un set composto dall'unione di s con s2 - {"Bologna", "Milano", "Catania", "Avellino", "Roma"}
    
    s.difference(s2) # restitusce un set con gli elementi di s non presenti in s2 - {"Roma"}
    
    s.issubset(s2) # restituisce True se s è un sottoinsieme di s2
    
    s.issuperset(s2) # restituisce True se s2 è un sottoinsieme di s
    
    s.isdisjoint(s2) # restituisce True se s e s2 non hanno elementi in comune (intersezione = {})   

#### Dictionary ####

Il tipo Dictionary permette di memorizzare in una variabile delle coppie di elementi chiave:valore, in modo simile quindi all'array associativo del PHP o alle map del C++.

Le liste dictionary vanno dichiarate racchiudendo le coppie all'interno delle parentesi graffe e separando con il carattere ":" la chiave dal valore.

    abitanti = {
        "Milano": 3500000,
        "Genova": 850000,
        "Bologna": 560000
    }
    
    abitanti['Bologna'] # restituisce 560000
    
    abitanti['Roma'] = 4000000 # aggiunge al dizionario una chiave "Roma" con valore 4000000
    
    abitanti.keys() # restituisce una lista con tutte le chiavi memorizzate: ["Bologna", "Genova", "Milano", "Roma"]
    
    abitanti.values() # restituisce una lista con tutti i valori memorizzati: [3500000, 850000, 560000, 4000000]
    
    abitanti.pop("Roma") # elimina la chiave "Roma" (e anche il suo valore) dal dictionary
    
    for k in abitanti.keys(): print(f"{k}: {abitanti[k]}") # stampa tutte le coppie del dictionary
    
    for k,v in abitanti.items(): print(f"{k}: {v}") # stampa tutte le coppie del dictionary

### Controllo del flusso ###
 
#### if ####
 
Il costrutto if in Python ha la seguente sintassi:
 
    if condizione:
        # istruzioni per condizione vera
    else:
        # istruzioni per condizione falsa
        
    if condizione1:
        # istruzioni per condizione1 vera
    elif condizione2:
        # istruzioni per condizione2 vera
    else:
        # istruzioni per condizione1 e condizione2 false
        
Notare che python riconosce le istruzioni da eseguire nei rami veri e falsi in base all'indentazione, quindi **rispettate rigorosamente l'indentazione**.

A differenza dei linguaggi C-like (C, C++, Java, JS, etc.) non è necessario racchiudere le condizioni all'interno delle parentesi tonde.

#### while ####

Il costrutto while in Python ha la seguente sintassi:

    while condizione:
        # istruzioni da ripetere
        
Non è presente in Python il corrispondente del costrutto do..while

#### for ####

Il ciclo for in Python è uno dei costrutti più usati per la sua grande flessibilità nell'operare con liste, array e tuple:

    for variabile in intervallo:
        # istruzioni del ciclo
        
    # Esempi
    
    for i in range(0,10):
        # assegna alla variabile i i valori da 0 a 9
        
    for i in range(-10,10,2):
        # assegna alla variabile i i valori da -10 a 9 a incrementi di 2
        
    for c in "Abracadabra":
        # assegna alla variabile c tutte le lettere della stringa "Abracadabra"
        
    for i in [4,3,8,2,27]:
        # assegna alla variabile i tutti gli elementi dell'array [4,3,8,2,27]
        
    for i in ('alfa', 'beta', 'gamma'):
        # assegna alla variabile i tutti gli elementi della tupla ('alfa', 'beta', 'gamma')
        
    for i in {'alfa', 'beta', 'gamma'}:
        # assegna alla variabile i tutti gli elementi del set {'alfa', 'beta', 'gamma'}
        # attenzione: l'ordine con cui vengono assegnati gli elementi a i è casuale
        
    for r in open("file"):
        # assegna alla variabile r tutte le righe lette dal file "file"
        
Un interessante sintassi del ciclo for prevede la presenza dell'else, che viene eseguito a meno che il ciclo non sia stato interrotto con break:

    """
    Nel seguente esempio cerchiamo il valore x all'interno dell'array v. 
    Se arriviamo alla fine del ciclo senza aver trovato l'elemento allora mostriamo il messaggio
    (fare attenzione all'indentazione, else è allineato con for non con if, quindi è parte dell'istruzione for)
    """
    for i in v:
        if i == x:
            print("Ho trovato x")
            break;
    else:
        print("Non ho trovato x")
        
#### List comprehension ####

Il ciclo for può essere usato anche per generare delle tuple, liste, set o dictionary in modo simile a come si definiscono gli insiemi in matematica.

Ad esempio in matematica si può definire un insieme con la seguente definizione:

![image](https://user-images.githubusercontent.com/100513972/229029916-2b1e8f81-b887-464b-a05c-ae649cb6239f.png)

Questa definizione dice che l'insieme è composto da tutti i valori 2*x con x appartenente all'insieme dei naturali e che soddisfi il criterio x^2>3.

In Python possiamo scrivere una definizione simile tutta con un'unica istruzione. 

Alcuni esempi:

    # insieme dei valori 2x con x appartenente all'intervallo 0-100 e x^2>3
    x = {2*x for x in range(100) if x*x>3}
    
    # Punti di coordinate di una funzione f(x) nell'intervallo [a,b] con passo p
    # per generare l'intervallo non usiamo range ma numpy.arange perché range lavora solo con interi
    import numpy 
    
    def f(x):
        return x*x
    
    a = -5
    b = 5
    p = 0.5
    # la seguente istruzione genera una lista con tutte le coppie (x,f(x)) per ogni x
    # appartenente all'intervallo [a,b] con intervalli di p tra le varie x
    t = [(x,f(x)) for x in numpy.arange(a,b+.1,p)]
    
    # risultato:
    # [(-5.0, 25.0), (-4.5, 20.25), (-4.0, 16.0), (-3.5, 12.25), (-3.0, 9.0),
    #  (-2.5, 6.25), (-2.0, 4.0), (-1.5, 2.25), (-1.0, 1.0), (-0.5, 0.25),
    #  (0.0, 0.0), (0.5, 0.25), (1.0, 1.0), (1.5, 2.25), (2.0, 4.0), 
    #  (2.5, 6.25), (3.0, 9.0), (3.5, 12.25), (4.0, 16.0), (4.5, 20.25)]
    
    s = "abracadabra"
    
    # elenco delle lettere di s che siano minori di 'd'
    tupla1 = (c for c in s if c < 'd') # crea la tupla ('a','b','a','c','a','a','b','a')
    lista1 = [c for c in s if c < 'd'] # crea la lista ['a', 'b', 'a', 'c', 'a', 'a', 'b', 'a']
    set1   = {c for c in s if c < 'd'} # crea il set   {'b', 'a', 'c'}
    dict1  = {c:ord(c) for c in s if c<'d'} # crea il dictionary {'a': 97, 'b': 98, 'c': 99}
    

#### match ####

Il costrutto match è l'equivalente Python dello switch dei linguaggi C-like, però con alcune flessibilità in più nei case:

    match variabile:
        case valore1:
            # istruzioni per variabile==valore1
            
        case valore2:
            # istruzioni per variabile==valore2
            
        case _:
            # istruzioni da eseguire se nessun case precedente va a buon fine
            
### Operatori e funzioni di base ###

#### Operatori di assegnamento ####

    +   # somma
    -   # sottrazione
    *   # moltiplicazione
    /   # divisione in virgola mobile
    //  # divisione intera
    %   # resto della divisione tra interi
    **  # elevamento a potenza
    
    +=  # incremento
    -=  # diminuzione
    /=  # partizione (divisione per)
    *=  # moltiplicazione per
    
    A differenza dei linguaggi C-like, non sono presenti gli operatori ++ e --
    
#### Operatori condizionali ####

    >   # maggiore di
    <   # minore di
    ==  # uguale a 
    >=  # maggiore o uguale a
    <=  # minore o uguale a
    !=  # diverso da
    
    and # congiunzione logica
    or  # disgiungione logica
    not # negazione logica
    
    in      # verifica se un elemento (o una sequenza) è presente dentro un altro elemento
    not in  # verifica se un elemento (o una sequenza) non è presente dentro un altro elemento
    
    Esempio:
        'alla' in "Balla coi lupi" 
        # restituisce True perché la stringa 'alla' si trova dentro la stringa "Balla coi lupi"
        
Ci sono alcune differenze tra Python e gli altri linguaggi riguardo la composizione delle condizioni. Ad esempio sono corrette le seguenti istruzioni:

    a < b < c
        # restituisce True se b è compreso tra a e c
        
    4 and 5
        # restituisce 5 (ultimo elemento vero della condizione)
        
    4 or 5
        # restituisce 4 (primo elemento vero sufficiente a soddisfare tutta la condizione)
        
    3 and 4 and False
        # restituisce False perché tutta la condizione è falsa e l'ultimo risultato è False
       
    4 and 7 and a==a
        # restituisce True perché tutta la condizione è vera e l'ultimo risultato è True
        
    a==a and 4 and 7
        # restituisce 7 perché tutta la condizione è vera e l'ultimo risultato è 7
    
#### if inline ####

In python c'è anche l'operatore ternario if che può essere usato per eseguire delle assegnazioni condizionali:

    a = 5
    b = 7
    
    c = a if a>b else b # memorizza in c il massimo tra a e b
    
    print("a" if a>b else "b") # stampa "a" se a>b altrimenti stampa "b"
    
#### Assegnazioni parallele ####

Un'interessante opportunità offerta da Python riguarda la possibilità di definire delle assegnazioni da eseguire "in parallelo" evitando di dover usare delle variabili intermedie:

    a = 4
    b = 5
    
    [a,b] = [b,a] # Scambia il contenuto delle variabili a e b
    (a,b) = (b,a) # idem
    a,b = b,a     # idem
    
    # Calcolo del massimo comun divisore tra a e b
    def MCD(a,b): 
        while b != 0:
            a, b = b, a % b # assegna alla variabile a il valore di b e a b il valore del resto tra a e b
        return a

## Funzioni ##

Le funzioni in Python si descrivono con l'operatore def:

    def massimo(a,b):
      return a if a>b else b

    def print_nominativo(nome, cognome):
      print(nome, ' ', cognome)

    def niente():
      pass # l'operatore pass è obbligatorio quando una funzione è vuota
      
Gli argomenti della funzione possono essere anche impostati con valori di default e possono anche essere richiamati per nome, evitando di dover rispettare sempre il loro ordine posizionale:

    def intervallo_chiuso(a=0, b=10):
      return range(a,b+1)

    intervallo_chiuso() # restituisce range(0,11)

    intervallo_chiuso(5) # restituisce range(5,11)

    intervallo_chiuso(b=6) # restituisce range(0,7)
   
E' anche possibile definire funzioni con un numero arbitrario di parametri, inserendo un asterisco prima del nome del parametro. Questo sarà interpretato come una tupla e quindi i valori potranno essere letti con un normale ciclo:

    def somma_quadrati(*numeri):
      sommma = 0
      for x in numeri:
         somma += x*x
      return somma

    somma_quadrati(1,2,3) # restituisce 14 = 1^2 + 2^2 + 3^3
   
   
Le funzioni in Python non accettano l'overload, quindi non è possibile definire più funzioni con lo stesso nome ma differenti tipi o numero di parametri.

Se in una funzione abbiamo necessità di accedere ad una variabile esterna, bisogna dichiararla esplicitamente con l'operatore global:

    count_primes = 0

    def find_primes(interval):
      global count_primes
      for n in interval:
         if is_prime(n):
            print(n)
            count_primes += 1
            
    find_primes(range(10)) # stampa 2 3 5 7 e memorizza in count_primes il valore 4
    find_primes(range(11,20)) # stampa 11 13 17 19 e memorizza in count_primes il valore 8
    
    """
    tenere presente che in questo esempio la stessa operazione si potrebbe risolvere senza accedere 
    ad una variabile globale ma facendo restituire il conteggio alla funzione.
    Ci sono però casi, come nella gestione multi-thread, in cui è più comodo lavorare su variabili globali
    """
    count_primes = 0

    def find_primes(interval):
        count = 0
        for n in interval:
            if is_prime(n):
                print(n)
                count += 1
        return count
        
    count_primes += find_primes(range(10)) # stampa 2 3 5 7 e memorizza in count_primes il valore 4
    count_primes += find_primes(range(11,20)) # stampa 11 13 17 19 e memorizza in count_primes il valore 8

### Passaggio di argomenti per riferimento o per valore ###

In Python gli argomenti di una funzione sono passati automaticamente per riferimento se sono di tipo mutabile (quindi liste, dictionary, set o classi), mentre se sono di tipo immutabile non possono essere passati per valore in quanto una loro modifica creerebbe dei nuovi oggetti (vedi il paragrafo sulle variabili numeriche).

Se si ha necessità di accedere per riferimento ad una variabile immutabile una possibile strategia potrebbe essere quella di inserirla all'interno di una variabile mutabile (ad esempio una lista) in modo che possa essere modificata senza problemi.

    """
    In questo esempio definiamo una funzione con un parametro v che, essendo una lista, sarà passato
    per riferimento e la modifica dei suoi elementi si ripercuoterà anche alla variabile
    dichiarata esternamente alla funzione
    """
    v = [5, 32, 27]
    
    def swap_first_last(v):
        if len(v) > 0:
            v[0], v[-1] = v[-1], v[0] # scambia primo e ultimo elemento della lista
            
    print(v) # mostrerà [27, 32, 5]
    
    """
    In questo esempio la funzione riceve un parametro numerico che vogliamo
    poter modificare. Abbiamo diversi modi per farlo:
    """
    # 1° metodo: sfruttare il return
    def increment(x, limit):
        return (x+1) % limit
        
    x = 5
    x = increment(x, 10)
    print(x) # mostrerà 6
    
    # 2* metodo: passare i parametri all'interno di una lista
    def increment(param): 
        param[0] = (param[0]+1) % param[1]
    
    x = [5, 10] # 5 è il numero da incrementare, 10 è il limite
    increment(x)
    print(x) # mostrerà [6, 10]

### Built-in Functions ###

Python mette a disposizione alcune funzioni di base che possono essere applicate a differenti tipi di dati e utilissime in diversi contesti di programmazione.

Di seguito l'elenco completo e una spiegazione delle più importanti:

<img width="436" alt="image" src="https://user-images.githubusercontent.com/100513972/229367992-2f7e10b9-e3e4-4100-b911-c592ca81510f.png">

#### abs ####

Restituisce il valore assoluto di un numero.

    x = 4
    y = 5
    z = abs(x-y) # restituisce 1

#### all(iterable) e any(iterable) ####

all(iterable) restituisce True se tutti gli elementi dell'argomento sono True.
any(iterable) restituisce True se almeno un elemento dell'argomento è True.

    """
    is_prime restituisce True se x è primo, False altrimenti
    """
    def is_prime(x):
       if x<2:
           return False
       i=2
       while i*i<=x:
           if x%i==0:
               return False
           i += 1
       return True

    # Creiamo una lista con un valore bool per indicare se ciascun indice è primo o meno
    primi = list(is_prime(x) for x in range(100))
    
    all(primi) # restituisce False - non sono tutti primi
    any(primi) # restituisce True - c'è almeno un indice primo
    
#### bin(x), hex(x), oct(x) ####
 
bin(x) restituisce una stringa con il valore di x in formato binario
hex(x) restituisce una stringa con il valore di x in formato esadecimale
oct(x) restituisce una stringa con il valore di x in formato ottale
 
    bin(7)   # restituisce '0b111'
    hex(32)  # restituisce '0x20'
 
#### chr(x), ord(x) ####
 
chr(x) restituisce la stringa corrispondente al codice Unicode x
ord(x) restituisce il codice Unicode della stringa x 
 
    chr(65)   # restituisce 'A'
    chr(8364) # restituisce '€'
    
    ord("A")  # restituisce 65
    ord("€")  # restituisce 8364

#### dir(), dir(x) ####

Restituisce un elenco dei nomi del corrente namespace, quindi l'elenco delle variabili e funzioni disponibili.
Se usato con un parametro, restituisce l'elenco degli attributi dell'oggetto parametro.

    s = "testo"
    
    dir(s)
    ['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']

#### enumerate(iterable) ####

enumerate(x) restituisce un oggetto di tipo enumerate partendo dalla sequenza x. Si usa generalmente per generare i cicli di lettura su collection.

    abitanti = {
        "Milano": 2000000,
        "Genova": 700000,
        "Napoli": 1200000
    }
    
    abitanti # mostra {'Milano': 2000000, 'Genova': 700000, 'Napoli': 1200000}
    
    list(abitanti) # mostra ['Milano', 'Genova', 'Napoli']
    
    list(enumerate(abitanti)) # mostra [(0, 'Milano'), (1, 'Genova'), (2, 'Napoli')]

#### filter(funzione, iterable) ####

filter(funzione, iterable) restituisce un nuovo iterable contenente gli elementi di quello passato come argomento che soddisfano la funzione booleana passata come primo argomento.

E' una funzione molto usata perché consente di costruire delle istruzioni più compatte senza dover ricorrrere a cicli for o while.

    def pari(x):
        return abs(x)>1 and x%2 == 0
        
    list(filter(pari, range(100)) # genera una lista con i numeri pari minori di 100
    
Nell'esempio appena visto la funzione range genera 100 numeri, filter applica a ciascuno la funzione pari e genera una lista con i soli valori in cui la funzione restituisce True. E' l'equivalente delle seguenti istruzioni:

    elenco =[]
    for i in range(100):
        if pari(i):
            elenco.append(i)        

#### id(x) e type(x) ####
 
id(x) restituisce un numero intero identificativo univoco di un oggetto. Controllare gli esempi di [Variabili numeriche](#variabili-numeriche) per chiarirne l'uso.
type(x) restituisce un oggetto con indicato il tipo di dato associato a x
 
#### input(prompt) ####
 
input(prompt) è la classica funzione di Python per gestire l'input a riga di comando. Il risultato è di tipo string, quindi procedere ad opportune conversioni nel caso si debba lavorare con altri tipi di dati.
 
    x = input("Inserisci un numero: ")
    x = int(x)
    
    print("é primo" if is_prime(x) else "non è primo")
    
#### int(x), float(x) ####

int(x) restituisce un valore intero estratto dalla stringa x. x deve contenere un numero intero, altrimenti si crea un'eccezione.
float(x) restituisce un valore float estratto dalla stringa x. x deve contenere un numero float, altrimenti si crea un'eccezione.

    int("4")   # restituisce 4
    int("4.5") # restituisce errore
    int("4 5") # restituisce errore
    
    float("4.5") # restituisce 4.5
    float("4 5") # restituisce errore
    
#### len(x) ####

len(x) restituisce la dimensione di un oggetto in termini di numero di elementi.

    list(x for x in range(1,1000) if x % 3 == 0) # genera una lista con i multipli di 3 minori di 1000
    
    [0, 3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54, 57, 60, 63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99, 102, 105, 108, 111, 114, 117, 120, 123, 126, 129, 132, 135, 138, 141, 144, 147, 150, 153, 156, 159, 162, 165, 168, 171, 174, 177, 180, 183, 186, 189, 192, 195, 198, 201, 204, 207, 210, 213, 216, 219, 222, 225, 228, 231, 234, 237, 240, 243, 246, 249, 252, 255, 258, 261, 264, 267, 270, 273, 276, 279, 282, 285, 288, 291, 294, 297, 300, 303, 306, 309, 312, 315, 318, 321, 324, 327, 330, 333, 336, 339, 342, 345, 348, 351, 354, 357, 360, 363, 366, 369, 372, 375, 378, 381, 384, 387, 390, 393, 396, 399, 402, 405, 408, 411, 414, 417, 420, 423, 426, 429, 432, 435, 438, 441, 444, 447, 450, 453, 456, 459, 462, 465, 468, 471, 474, 477, 480, 483, 486, 489, 492, 495, 498, 501, 504, 507, 510, 513, 516, 519, 522, 525, 528, 531, 534, 537, 540, 543, 546, 549, 552, 555, 558, 561, 564, 567, 570, 573, 576, 579, 582, 585, 588, 591, 594, 597, 600, 603, 606, 609, 612, 615, 618, 621, 624, 627, 630, 633, 636, 639, 642, 645, 648, 651, 654, 657, 660, 663, 666, 669, 672, 675, 678, 681, 684, 687, 690, 693, 696, 699, 702, 705, 708, 711, 714, 717, 720, 723, 726, 729, 732, 735, 738, 741, 744, 747, 750, 753, 756, 759, 762, 765, 768, 771, 774, 777, 780, 783, 786, 789, 792, 795, 798, 801, 804, 807, 810, 813, 816, 819, 822, 825, 828, 831, 834, 837, 840, 843, 846, 849, 852, 855, 858, 861, 864, 867, 870, 873, 876, 879, 882, 885, 888, 891, 894, 897, 900, 903, 906, 909, 912, 915, 918, 921, 924, 927, 930, 933, 936, 939, 942, 945, 948, 951, 954, 957, 960, 963, 966, 969, 972, 975, 978, 981, 984, 987, 990, 993, 996, 999]
    
    len(_) # restituisce il numero di elementi dell'ultimo risultato (_)
    334
 
#### map(funzione, iterable) ####

map(funzione, iterable) applica a ogni elemento di iterable la funzione passata come primo parametro e restituisce un nuovo iterator

Come per filter questa funzione è usata molto perché permette di abbreviare il codice.

    import math
    
    list(map(math.sqrt, range(1,10))) # crea una lista con le radici quadrate dei numeri 1-9
    
    [1.0, 1.4142135623730951, 1.7320508075688772, 2.0, 2.23606797749979, 2.449489742783178, 2.6457513110645907, 2.8284271247461903, 3.0]
    
    # alternativa procedurale
    elenco = []
    for i in range(1,10):
        elenco.append(math.sqrt(i))
        
#### max(iterable), min(iterable), sum(iterable) ####

max(iterable) restituisce il valore massimo presente in iterable
min(iterable) restituisce il valore minimo presente in iterable
sum(iterable) restituisce la somma dei valori presenti in iterable

    v = [3,1,5]
    
    max(v) # restituisce 5
    min(v) # restituisce 1
    sum(v) # restituisce 9
    
    """
    Esempio più articolato: calcolo la deviazione standard di una serie di valori.
    Ad ogni elemento x di v viene applicato il calcolo (x-M)^2, vengono sommati tutti questi valori
    e successivamente divisi per il loro numero. Il risultato finale sarà la radice quadrata
    di questo valore medio.
    Per rendere ancora più breve il codice è stata usata una funzione lambda (funzione anonima)
    """
    def deviazione_standard(v):
        media = sum(v)/len(v)
        return math.sqrt(sum(map(lambda x: (x-media)**2, v))/len(v))
        
    # stessa funzione in modo semi-tradizionale:
    def deviazione_standard(v):
        media = sum(v)/len(v)
        somma = 0
        for x in v:
            somma += (x-media)**2
        somma /= len(v)
        return math.sqrt(somma)

#### sorted(iterable, key=None, reverse=False) ####

sorted(iterable, key=None, reverse=False) restituisce l'iterable con gli elementi ordinati. Eventualmente si può aggiungere l'opzione reverse=True per inventire l'ordinamento, oppure il parametro key=funzione per definire una funzione con un parametro che estragga dal parametro l'elemento da confrontare.

    v = [3,1,4]
    
    sorted(v) # restituisce [1,3,4]
    
    sorted(v, reverse=True) # restituisce [4,3,1]
    
    abitanti = {
        "Milano": 2000000,
        "Genova": 700000,
        "Napoli": 1200000
    }
    sorted(abitanti) # restituisce l'elenco ordinato delle chiavi
    ['Genova', 'Milano', 'Napoli']
    
    sorted(abitanti, key=lambda x: abitanti[x]) # restituisce l'elenco delle chiavi ordinate per popolazione
    ['Genova', 'Napoli', 'Milano']
    
#### zip(*iterables) ####

`zip(*iterables)` produce un iteratore generando tante tuple composte di elementi presenti in ciascun elenco passato. Può essere utile quando si vogliono creare dei cicli su più liste in parallelo.

    citta = ['BO', 'MI', 'NA']
    abitanti = [650000, 2000000, 1200000]
    
    for c,a in zip(citta, abitanti):
        print(f"{c} ha {a} abitanti")
        
    # oppure possiamo usare zip per trasformare due liste in un dictionary:
    dict(zip(citta, abitanti))
    {'BO': 650000, 'MI': 2000000, 'NA': 1200000}

## Classi e Oggetti ##

Naturalmente anche Python prevede la programmazione ad oggetti e la definizione di classi personalizzate. Del resto tutte le variabili usate dal linguaggio sono memorizzate come oggetti e hanno quindi degli attributi e metodi ciascuna (vedere la funzione dir(oggetto)).

Per definire una classe si usa la seguente sintassi:

    class NomeClasse:
        # elenco attributi 
        attributo1 = valore
        attributo2 = valore
        ...
        
        #costruttore
        def __init__(self):
            ...
            
        def metodo1(self, parametri):
            ...
            
Notare che per gli attributi non vi è distinzione tra pubblici e privati; sono tutti considerati pubblici e viene suggerito soltanto di preporre un carattere di underscore al nome per indicare quelli che si vuole considerare privati, ma comunque accessibili anche all'esterno della classe (è giusto una convenzione).

Notare inoltre nella definizione dei metodi il primo parametro obbligatorio **self** che passa l'oggetto stesso alla funzione in modo che possa accedere agli altri elementi della classe (è l'equivalente del *this* di altri linguaggi).

    """ Esempio: definiamo una classe Punto """
    import math
    
    class Punto:
        x = 0
        y = 0
        
        def __init__(self, x=0, y=0):
            self.x = x
            self.y = y
            
        def distanza_da_origine(self):
            return math.sqrt(self.x**2 + self.y**2)

    
    p1 = Punto()     # crea un oggetto Punto con coordinate (0,0)
    p2 = Punto(3, 1) # crea un oggetto Punto con coordinate (3,1)
    
    print(p2.distanza_da_origine()) # restituisce 3.1622776601683795
    
    p2.x = 2         # cambiamo la coordinata x in 2
    
    print(p2.distanza_da_origine()) # restituisce 2.23606797749979

Ci sono casi in cui si vogliono gestire delle classi alla stregua dei record, con quindi diversi attributi da inizializzare in fase di creazione dell'istanza. In questo caso può essere comodo ricorrere ad un modulo di python chiamato **dataclasses** che aggiunge automaticamente alla classe il costruttore con tutti i parametri da inizializzare.

    from dataclasses import dataclass
    
    @dataclass
    class Libro:
        titolo : str
        autore : str
        editore: str
        genere : str
        
        def mostra(self):
            print(f"{self.titolo} - {self.autore} - {self.editore} - {self.genere}")
            
    libro1 = Libro("Impariamo Python", "F.C.", "Mondadori", "Informatica") # crea un oggetto Libro assegnando tutti gli attributi
    
    libro1.mostra() # mostra "Impariamo Python - F.C. - Mondadori - Informatica"
    
    libro2 = Libro() # dà errore perché il costruttore attende 4 parametri

        
    

        
