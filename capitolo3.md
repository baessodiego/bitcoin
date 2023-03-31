# Le basi di una cryptocurrency


## Indice

1. [Hashing](#hashing)
2. [Block](#block)
3. [Blockchain](#blockchain)
4. [Network]()
5. [Mempool]()
6. [Consenso]()
7. [Wallet (portafolio)]()
8. [Signature (firma digitale)]()
9. [Transazioni]()

<br>


## **Hashing**

**Hash**: impronta digitale (unica) legata ad un' informazione.

Partendo dall'informazione (per es. una transazione) si arriva all'_hash_ tramite una funzione di hash, nel caso di bitcoin sarà la funzione `SHA256` ♦️. Questa funzione prende tutte le informazioni date e le trasforma in una stringa a 256 bit. 

♦️ SHA è l'acronimo di "Secure Hashing Algorithm" e 256 sono i bit del valore ottenuto.

<br>

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

<br>

## **Blockchain**

È il ledger digitale che contiene l'intera history delle transazioni fatte sul network.  
Ogni blocco è collegato tramite l'_hash_ del blocco precedente, ecco da dove arriva il termine _block_ (blocco) _chain_ (catena).

Ogni blocco è numerato: il primo, chiamato _Genesis Block_ è il blocco numero 1. Ad oggi abbiamo superato i `700.000` blocchi (2023).

> Cosa succede se cambio il valore di un parametro di un blocco?

Se viene modificato un valore di un blocco, cambierà il suo hash che quindi sarà diverso dall'hash del blocco successivo!  
Questo porta all'invalidazione di tutti i blocchi successivi al blocco modificato.

<br>

## **Network**

La blockchain di Bitcoin è un network _peer-to-peer_, cioè una rete di nodi che permetta la condivisione di informazioni tra gli utenti del network stesso. L'utente non si collegherà ad un server centrale, ma ad un gruppo di altri nodi connessi nella rete (~10 connessioni per nodo).

È anche un network _distribuito_: cioè una rete che consente la diffusione delle informazioni tra più utenti.

Ci sono 3 tipi principali di network:

+ **Centralizzato**: tutte le informazioni sono mantenute in un'unica location (es. server di una banca).
+ **Decentralizzato**
+ **Distribuito**: ognuno ha lo stesso potere / permesso di vedere le infomazioni contenute nel network. Ogni nodo ha un'esatta copia della blockchain sulla propria macchina.

<br>

## **Memory Pool (Mempool)**

È il posto in cui le transazioni _non ancora confermate_ "aspettano" di essere aggiunte al blocco.

I miners si occupano di prendere le transazioni dalla mempool, inserirle nel blocco per poi aggiungerlo alla blockchain. Se il blocco su cui sta lavorando un miner A "perde la gara", perchè un miner B ha trovato prima di lui la soluzione, le transazioni prese dal miner A torneranno nella mempool.

⚠️ Se dopo 14 giorni la transazione è ancora in attesa nella mempool, verrà annullata e rimossa.

Una transazione deve attendere la verifica / conferma di 6 blocchi per essere verificata.

<br>

## **Consenso**

L'idea che sta alla base del consenso di una blockchain lo trovi nel [capitolo 2, Byzantine Generals' Problem](/capitolo2.md#byzantine-generals-problem).

Ci sono 3 principali tipi di consenso, usati in diversi tipi di blockchain: 

1. [Proof of Work](#proof-of-work-pow)
2. [Proof of Stake](#proof-of-stake-pos)
3. [Delegated Byzantine Fault Tolerance](#)

### Proof of Work (PoW)

È un sistema in cui le informazioni, nel nostro caso i blocchi, sono costose da produrre (_work_) ma facili da verificare (_proof_).

I miners devono disporre di molta potenza computazionale per trovare l'esatto valore numerico, chiamato _nonce_, per avere come risultato l'esatto numero di _zeri_ all'inizio dell'hash del blocco stabilito dal network.

```
L'hash del blocco n. 783,349 è:
000000000000000000025fbc10754a289f82f998e982c67f9529639721e7f1e5

La difficoltà sta nel trovare un hash che inizi con 19 zeri.
Più zeri ci sono nella richiesta di hash, più sarà difficile da trovare.

Informazioni del blocco (Block Data) + Nonce = Hash
```

L'hash del blocco lo trovi su [blockchain.com/explorer](https://www.blockchain.com/explorer/blocks/btc/783349)

Prova a minare un blocco con [questo simulatore online](https://andersbrownworth.com/blockchain/block).*  
\* La difficoltà nel simulatore è a 4 zeri iniziali.

> Come viene ricompensato il miner?

Il primo miner che trova il _nonce_ viene ricompensato in 2 modi:

+ **Fee** delle transazioni fatte sul blocco trovato
+ **BTCs** creati dalla risoluzione del blocco, ricordo che questo è l'unico modo per introdurre nuovi bitcoins nel network.

> Chi decide la difficoltà di mining?

I creatori della blockchain di BTC hanno scelto di mantenere il tempo di creazione di un blocco ad una media di `10 minuti`.

Ogni 2 settimane viene regolata in automatico la difficoltà:  

+ creazione del blocco << 10 min => aumenta la difficoltà (più _zeri_)
+ creazione del blocco >> 10 min => diminuisce la difficoltà (meno _zeri_)

> Perchè proprio 10 minuti?

Per questioni di sicurezza.  
Se fosse troppo veloce, alcuni hacker potrebbero riuscire a cambiare i dati _prima_ della verifica del blocco più facilmente.  
D'altra parte, se fosse troppo lenta, ci sarebbe un tempo di attesa per la verifica di una transazione molto lungo.

❌ Problemi del PoW

+ **Consumo di energia elettrica $$$**  
Tutti i computer e le farm connesse h24 sparse nel mondo hanno un consumo di energia elettrica complessivo che va oltre al consumo di uno stato come l'Irlanda! Oltre ad essere costoso è anche fortemente inquinante.

+ **Possibilità di un miner di avere troppo potere (> 50%)**  
Se 1 di queste pool raggiungesse il 51% di potere computazionale mondiale sarebbe un problema: quella pool avrebbe il potere di modificare i dati della blockchain a proprio piacimento, facenso saltare il processo del consenso.

### Proof of Stake (PoS)

È un altro tipo di algoritmo che si basa sull'attribuzione di voti ai membri del network, che dipendno dal loro _successo_* nella blockchain.  
\* migliorare ed avere un impatto positivo sulla blockchain.

⚠️ Non ci sono i miners!