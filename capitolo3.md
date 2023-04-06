# Le basi di una cryptocurrency

In questo capitolo vedremo gli aspetti principali di una cryptocurrency, mantenendo il focus sul bitcoin.

Ogni approfondimento di questi punti verrà discusso nei capitoli successivi.

## Indice

1. [Hashing](#hashing)
2. [Block](#block)
3. [Blockchain](#blockchain)
4. [Network](#network)
5. [Mempool](#memory-pool-mempool)
6. [Consenso](#consenso)
7. [Wallet (portafolio)](#wallet)
8. [Signature (firma digitale)](#signature)
9. [Transazioni](#transazioni)

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
3. [Delegated Byzantine Fault Tolerance](#delegated-byzantine-fault-tolerance-dbft)

<br>

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

<br>

### Proof of Stake (PoS)

È un altro tipo di algoritmo che si basa sull'attribuzione di voti ai membri del network, che dipendno dal loro _successo_* nella blockchain.  
\* migliorare ed avere un impatto positivo sulla blockchain.

⚠️ Non ci sono i miners, ma ci sono i **_validators_**, cioè tutti coloro che _mettono in stake_ i propri coins per validare il blocco che verrà aggiunto alla blockchain.

Maggiore sarà la quantità di coins in stake, maggiore sarà la probabilità di essere ricompensati per la creazione del blocco. Chi creerà il blocco verrà ricompensato con una percentuale proporzionale a quanto messo in stake.

> Chi usa il PoS al momento?

Le principali blockchain che usano il PoS sono:

+ **Ethereum**: è passato dal PoW al PoS tramite il [progetto Casper](https://academy.binance.com/it/articles/ethereum-casper-explained).
+ **Dash**: è il pioniere del PoS, creato sulla base di BTC.
+ **Lisk**: ha come obbiettivo la creazione di app decentralizzate ed usa il DPoS (Delegated Proof of Stake).

<br>

### Delegated Byzantine Fault Tolerance (DBFT)

È un algoritmo basato sull'assegnazione di _ruoli_ ai nodi per la coordinazione del consenso.

⚠️ Non ci sono i miners, ma i nodi sono divisi in:

+ **Nodi ordinari**
+ **Nodi di consenso**: cioè quelli che hanno il ruolo di validare i blocchi

> Come fa un nodo ordinario a diventare un nodo di consenso?

Ci sono vari criteri che dipendono dalla piattaforma, tra cui:

+ determinate connessioni internet
+ un determinato equipaggiamento tecnologico
+ avere un minimo di monete in stake nel network

I nodi di consenso si divido nuovamente in 2 sottogruppi:

+ **Speakers**: quelli che creano il blocco e lo propongono ai delegates.
+ **Delegates**: quelli che approvano il blocco, almeno il 66% dei delegati devono essere d'accordo.

Se lo speaker corrente non ottiene il 66% dell'approvazione, diventa un delegato e un altro delegato verrà scelto per diventare il nuovo speaker.  In questo sistema tutti hanno la possibilità di diventare nodi di consenso, speaker e delegate.

DBFT è piu veloce del PoW, ma è meno sicuro.

Una piattaforma che usa questo algoritmo di consenso è **NEO**.

<br>

## **Wallet**

**Wallet Address** è un identificatore unico per il tuo wallet; per ottenerlo servono 2 chiavi, una pubblica e una privata.

### Chiave privata (Secret Key)

È un numero _casuale_ che permette di scambiare bitcoins dal tuo indirizzo wallet.

Un wallet può avere più di una chiave privata.  
La chiave privata viene usata per generare le firme digitale, confermare la proprietà di un wallet e autorizzare la propria transazione nella blockchain.

### Chiave pubblica (Public Key)

Viene creata dalla chiave privata con l'utilizzo della _crittografia a curva ellittica_. Quando si spendono e ricevono bitcoin, la chiave pubblica è rappresentata dall'indirizzo wallet.

L'algoritmo utilizzato è denominato con **ECDSA** (Elliptic Curve Digital Signature Algorithm). Con questo algoritmo è impossibile tornare indietro, al valore non ancora crittografato.

### Indirizzo Bitcoin (Bitcoin Address)

È un identificatore (unico) della destinazione dei pagamenti in bitcoin, generato dalla chiave pubblica.

È generalmente generato usando le funzioni di hash **SHA256** e **RIPEMD-160** in serie sulla chiave pubblica.

Questa serie di caratteri viene poi codificata usando la codificazione **Base58** per renderlo più leggibile.  
58 sono i caratteri alfanumerici di questa codificazione.

> Perchè 58?

Ci sono 52 caratteri nell'alfabeto (26 maiuscoli e 26 minuscoli) + 10 numeri (da 0 a 9).
Di questi 62, Satoshi ne rimosse 4 per non confondere numeri e lettere, cioè: la lettera 'O' e il numero `0`, la lettera maiuscola 'I' (i) e la lettera minuscola 'l' (elle).

> RECAP Algoritmi

Chiave Privata: `C4bbcb1fbec99d65bf59d85c8cb62ee2db963f0fe106f483d9 afa73bd4e39a8a`

⚙️ _ECDSA_ (Chiave privata)

Chiave Pubblica:
`0478d430274f8c5ec1321338151e927f4c676a008bdf8638d07c0b6be9ab35c71a1518063243acd4dfe96b66e3f2ec8013c8e072cd09b3834a1981659cc345`

⚙️ _RIPEMD-160_ (_SHA256_ (Chiave pubblica))

Indirizzo:
`c4c5d791fcb4654a1ef5e03fe0ad3d9c598f9827`

⚙️ _Base58_ (Indirizzo)

Indirizzo wallet:
`1JwSSubhmg6iPtRityqhUYYH7bZq3Lfy1T`

<br>

## **Firme Digitali (Signature)**

Vedremo cosa sono e a che cosa servono le firme digitali nel [capitolo successivo](/capitolo4.md#crittografia-transazioni-e-mining) poichè è un argomento più complicato da discutere.

<br>

## **Transazioni**

È una struttura dati che codifica e trasferisce un valore (come dei BTC) da una sorgente di fondi (input) ad una destinazione (output).

Questa è una comune transazione: 1 input e 2 output.

![transazione](/img/transazione-1input2output.png)

Tutti gli input fanno riferimento ad un output di una transazione precedente.

Gli inputs sono chiamati **UTXO** (Unspent transaction output) ed arrivano da un'altra transazione.

Il wallet fa riferimento a un certo numero di UTXO in uno o più blocchi all'interno della blockchain. I tuoi coins non sono quindi "fisicamente" nel tuo wallet, ma sono dei riferimenti a degli UTXO.

⚠️ Gli UTXO non sono divisibili, quindi se decido di inviare una piccola parte di coins del mio wallet, questo non sarà sempre possibile. *

\* Come vediamo dall'immagine, in input c'è un UTXO di valore `0.01210048 BTC` che viene completamente inviato al secondo wallet. I 2 output sono:

+ `0.00324472`, cioè il valore effettivamente stabilito dall'utente che ha inviato i BTC.
+ `0.00883038`, cioè il **resto** che verrà nuovamente inviato allo stesso indirizzo che si trova nell'input.

Nelle transazioni ci sono le **FEES**, cioè la quantità di BTC da pagare al miner per la creazione del blocco.

```
Fees = Somma degli input - Somma degli output
```

Nella transazione che si vede nell'immagine, le fees si calcoleranno così:  
`341.06$ - (91.45$ + 248.89$) = 0.72$`

---

Questa era un'infarinatura generale sulle cryptocurrencies. Nei prossimi capitoli vedremo in dettaglio i punti affrontati precedentemente.

<br>

[⬅️ Capitolo Precedente](/capitolo2.md) | [Capitolo Successivo ➡️](/capitolo4.md)