# Concurrent Database Access — OMNeT++ project

Questo repository contiene il codice per il Project 4 (Concurrent database access). I file principali sono sotto `progetto/`.

Struttura rilevante:
- `progetto/simulations/DatabaseNetwork.ned` — network che istanzia gli utenti (`User`) e le tabelle (`Table`) e le connessioni.
- `progetto/src/User.ned`, `User.cc`, `User.h` — modulo `User` che genera richieste di accesso.
- `progetto/src/Table.ned`, `Table.cc`, `Table.h` — modulo `Table` che implementa la semantica FCFS, letture concorrenti e scritture in mutua esclusione.
- `progetto/simulations/omnetpp.ini` — configurazioni d'esempio per eseguire simulazioni con distribuzioni `uniform` e `lognormal`.

Come importare ed eseguire in OMNeT++ (IDE):
1. Apri OMNeT++ IDE e importa la cartella `perfermance-project` come progetto esistente.
2. Assicurati che i file sorgente C++ siano sotto `src/` del progetto e che i file `.ned` siano riconosciuti.
3. Se il tuo compagno ha una diversa implementazione di `Table`, puoi sostituire `src/Table.*` con la sua versione.
4. Apri `omnetpp.ini` (in `progetto/simulations`) e scegli la configurazione desiderata (ad esempio `Uniform_N10_p0.8` o `Lognormal_N10_p0.8`).
5. Esegui la simulazione (Run) o fai una sweep cambiando `**.numUsers` e `**.user[*].readProbability`.

Note su parametri e calibrazione:
- `**.user[*].lambda` (nel file .ini) è il rate usato nel modulo `User`. Controlla `User.cc` se vuoi interpretarlo come mean interarrival time invece del rate.
- Puoi calibrare i parametri della distribuzione lognormale modificando i parametri `m` e `s` in `User::selectTableLognormal()`.
- `serviceTime` (S) è impostato come parametro in `User` e passato alle `Table` come parametro nella richiesta; ogni richiesta usa quel valore per la durata fissa.

Cosa posso fare ancora:
- Aggiungere script (PowerShell) per lanciare più esecuzioni con valori diversi di N e p e raccogliere i risultati.
- Esporre i parametri della lognormale come parametri NED per facilitarne la calibrazione.
- Aggiungere vettori/statistiche aggregate a livello di network per misurare throughput totale (accessi/sec) direttamente.

Dimmi come vuoi procedere: continuo con uno script di sweep, oppure eseguo l'esportazione dei risultati/metriche aggiuntive?