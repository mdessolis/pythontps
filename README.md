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
    
    # Adesso assegnamo uno string literal alla variabile a
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
    
