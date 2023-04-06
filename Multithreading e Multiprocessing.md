# Multithreading e Multiprocessing #

## Differenza tra multithread e multiprocessing ##

Per **thread** si intende un blocco di istruzioni (di solito una funzione o un metodo) eseguito all'interno di un processo in parallelo con altre istruzioni.
  
Pensiamo ad esempio ad un browser che deve mostrare una pagina web: se questa contiene diverse immagini/fogli di stile o altri elementi esterni il browser dovrà scaricare tutti questi file. Ebbene, di solito questo lo fa in parallelo facendo partire una procedura di download (thread) per ciascun file in modo da ottimizzare i tempi.

Oppure pensiamo ad un qualunque sistema di videoscrittura: mentre digitiamo il testo questo automaticamente viene impaginato e spesso anche controllato come ortografia. Ebbene, queste operazioni sono probabilmente eseguite da thread paralleli alla digitazione.

Nel caso del thread quindi si lavora sempre all'interno di un singolo processo di esecuzione che ha al suo interno delle diramazioni di esecuzione che lavorano in parallelo. Però, essendo un singolo processo, l'area dati e i registri di esecuzione del codice sono comuni, quindi i thread condividono tutti gli stessi dati.

Per **processo** si intende invece un blocco di codice che viene eseguito in genere in modo autonomo sul computer e al quale viene quindi assegnato un proprio spazio di memoria. Ad esempio se avviamo un programma di videoscrittura verrà creato un processo di esecuzione e assegnato a questo un codice univoco (detto PID). Nulla ci impedisce però di lanciare due esecuzioni contemporanee del programma, creando però due processi che non condividono tra loro nessuno spazio di memoria.

E' però possibile programmare un codice per istruirlo a dividere l'esecuzione del processo in più sottoprocessi da avviare in parallelo, sfruttando in questo modo le caratteristiche dei moderni processori, composti da più core che possono tranquillamente eseguire operazion in parallelismo reale.

A differenza però di una esecuzione multithread, in quella multiprocess non vi è condivisione della memoria per cui bisogna prevedere, nel caso se ne abbia bisogno, strumenti per far comunicare tra loro i sottoprocessi.


