# Le basi di una cryptocurrency


## Indice

1. [Hashing]()
2. [Block]()
3. [Blockchain]()
4. [Network]()
5. [Mempool]()
6. [Consenso]()
7. [Wallet (portafolio)]()
8. [Signature (firma digitale)]()
9. [Transazioni]()

## **Hashing**

**Hash**: impronta digitale (unica) legata ad un' informazione.

Partendo dall'informazione (per es. una transazione) si arriva all'_hash_ tramite una funzione di hash, nel caso di bitcoin sarà la funzione `SHA256` ♦️. Questa funzione prende tutte le informazioni date e le trasforma in una stringa a 256 bit. 

♦️ SHA è l'acronimo di "Secure Hashing Algorithm" e 256 sono i bit del valore ottenuto.

## **Block**

Il blocco funge da contenitore di informazioni, come la lista di transazioni che devono essere verificate, che verranno poi aggiunte alla blockchain.

Il blocco è formato da 2 parti:

+ **Block Header**: è la "cima" del blocco, formato da:
    + hash del blocco precedente
    + data e ora della propria creazione
    + _merkle root_, cioè l'unione delle informazioni di tutte le transazioni in un singolo hash
    + _nonce_, un valore che può essere utilizzato una sola volta nel network ed è il valore che devono trovare i miners per creare il blocco. [Approfondimento nel punto 6]()
+ **Block Body**: è il corpo del blocco, e contiene una lista di transazioni e le informazioni riguardo ad esse.  

Il blocco ha una grandezza limite in MB (Megabyte) che non può superare.  
Inserendo transazioni aumenterà il peso del blocco ed una volta raggiunto il limite si dovrà creare un nuovo blocco.

Viene creato un blocco ogni `~10 minuti`. Questo è il tempo medio di risoluzione di un blocco in base alla _difficoltà attuale_, che viene ricalibrata ogni `2016 blocchi, ~2 settimane`; ciò significa che un blocco può essere creato in 1 minuto come in 30, dipende dalla fortuna del miner nel trovare velocemente il _nonce_.

> Perché si cerca di tenere in media un tempo di 10 minuti? Relativamente lungo rispetto alle altre blockchain.

Per evitare il più possibile di di avere simultaneamente la risoluzione di 2 blocchi, che è una delle cause di rallentamenti all'intenro del network di BTC. In media questo avvenimento avviene 1 volta a settimana. [Approfondimento nel punto 6]()

## **Blockchain**

