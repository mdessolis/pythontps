# Python for TPS

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
    
    len(a)      # resituisce 34
    a[1]        # restituisce 'a'
    'alla' in a # restituisce True ('alla' si trova dentro la stringa a)
    'Alla' in a # restituisce False('Alla' non si trova nella stringa a, la ricerca è case sensitive)
    for c in a: # esegue un ciclo for memorizzando in c una ad una tutte le lettere presenti in a
    
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

### Operatori di assegnamento ###

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
    
### Operatori condizionali ###

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
        'alla' in "Balla coi lupi" # restituisce True perché la stringa 'alla' si trova dentro la stringa "Balla coi lupi"
        
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
    
    
    
