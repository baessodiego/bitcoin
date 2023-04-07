# Ledger e il Byzantine Generals' Problem


## Indice

+ [Definizioni introduttive](#prima-di-iniziare-alcune-utili-definizioni)
+ [Il ruolo del ledger](#il-ruolo-del-ledger)
+ [Il Byzantine Generals' Problem](#byzantine-generals-problem)
+ [L'approccio di BTC al BGP](#lapproccio-di-bitcoin-al-bgp)

---

<br>


## Prima di iniziare, alcune utili definizioni: 

+ **Ledger**: registro completo dell'attività di un business o di un individuo, solitamente traccia i trasferimenti di denaro e certificati di proprietà di beni.
+ **Blockchain**: una serie di blocchi _confermati_, ognuno collegato con il precedente, fino al primo blocco (Genesis Block).  
Questo registro globale tiene traccia e codifica il traferimento di un valore tra i partecipanti di un network peer-to-peer (p2p)*.  
\* p2p: rete informatica nella quale i computer degli utenti connessi fungono nello stesso tempo da client e da server.
+ **SHA256**: hash crittografato che funge da _impronta digitale_ per una stringa di testo o un file contenente una serie di dati.  
Nel network è usato per confermare l'integrità e l'autenticità delle transazioni.  
Questa funzione (Sha256) genera un hash di 256-bit (32-byte).  

> **Esempio**  
Stringa di testo: _ciao_  
Stringa codificata in SHA256: `b133a0c0e9bee3be20163d2ad31d6248db292aa6dcb1ee087a2aa50e0fc75ae2`

Prova tu: [SHA256 Converter](https://emn178.github.io/online-tools/sha256.html)

<br>

---

<br>


## **Il ruolo del ledger**

Il ledger, o registro, è usato per registrare e tenere traccia di tutte le attività economiche, come il trasferimento di denaro, il passaggio di proprietà, ecc...

I beni registrati nel ledger possono essere:
+ **tangibili**: immobili, veicoli, ...
+ **intangibili**: denaro, stocks, diritti digitali, ...

### **Ledger centralizzati** 🏦

Gli unici ledger che conosciamo ad oggi sono centralizzati, come le banche; (i ledger centralizzati) li diamo per scontati perche sono sempre stati l'unica forma di registro usata.

Esempi di ledger centralizzati usati oggi:
+ transazioni bancarie e della carta di credito
+ registro delle prenotazioni in un hotel
+ lista di nomi dei proprietari di un auto
+ informazioni legate al tuo ID (documento d'identità)

Ad occuparsi di registrare le nostre attività è un operatore fidato, come la banca (per il trasferimento di denaro) o l'anagrafe (per il registro delle informazioni).  

> Ma questi operatori _fidati_ non sono infallibili!

Le persone / istituzioni incaricate a registrare le nostre attività possono:
+ **non essere affidabili**. _Per esempio potrebbero creare nel registro un falso trasferimento di proprietà_ 👿
+ **escludere enti che non approvano**. _Per esempio una banca potrebbe bloccare i bonifici che arrivano da un determinato business._ ❌
+ **perdere dati sensibili** in seguito ad attacchi informatici, problemi tecnici o disastri ambientali. 🔓

### **Ledger Decentralizzati** 🧩

Il termine decentralizzato si riferisce al fatto che non esiste un _unico_ luogo fisico in cui sono salvati tutti i dati relativi ad un registro ma che invece sono condivisi all'interno di un network.

I tre principali vantaggi di un ledger decentralizzato:

+ invulnerabilità alla **censura**. Nessuno ha il completo controllo sui dati, quindi nessuno può decidere cosa escludere.
+ invulnerabilità a possibili **atti illeciti** da parte di un ente incaricato al registrare dati.
+ invulnerabilità alla **perdita di dati**. I registri sono salvati e condivisi su una grande rete di computer: se ci dovessero essere problemi tecnici su uno di questi computer, ci sarebbe il backup salvato sugli altri.

<br>

---

<br>


Problema con i ledger decentralizzati:

> Chi decide le regole del ledger e come si raggiunge il consenso da parte della maggioranza?

Il modello a cui si ispira la Blockchain di Bitcoin è stato ricavato dal _Byzantine Generals' Problem_
(Problema dei generali bizantini)


## **Byzantine Generals' Problem**

L'idea che sta alla base del _consenso_ è data da questo problema, abbreviato BGP, proposto da Marshall Pease, Robert, Shostak e Leslie Lamport nel 1982.  

È espresso attraverso una situazione in cui 10 generali bizantini, con le rispettive truppe, sono accampati fuori dalle mura nemiche e devono decidere come agire: devono attaccare o ritirarsi?  

I generali possono comunicare solo attraverso i loro messaggeri. Il problema è che alcuni generali potrebbero essere dei traditori e decidere di comunicare il falso.

Nel nostro caso possiamo paragonare i generali ai nodi del network peer-to-peer e i traditori ai nodi con l'obiettivo di verificare delle transazioni fraudolente.

Una soluzione proposta è quella del consenso che sta dietro alla blockchain di Bitcoin. Il [whitepaper](https://bitcoin.org/bitcoin.pdf) di Bitcoin fu proposto per la prima volta sul web il `31 ottobre 2008` da una persona / gruppo con lo pseudonimo di **Satoshi Nakamoto**.

Ad oggi è la migliore soluzione al BGP mai proposta ed è quella attualmente utilizzata.

<br>

---

<br>

## **L'approccio di Bitcoin al BGP**

Prima di iniziare, alcune utili definizioni: 

+ **bitcoin**: con la _b minuscola_ indica la cryptocurrency (unità di conto) usata all'interno del network di Bitcoin.
+ **Bitcoin**: con la _B maiuscola_ si usa per descrivere il concetto, il network, il progetto e la community.
+ **Indirizzo Bitcoin**: è una stringa di lettere e numeri (codificata in sha256) collegata ad un portafoglio digitale, a cui si possono inviare bitcoin.
+ **Transazione**: una _registrazione_ che informa il network del trasferimento di bitcoin tra due nodi.
+ **Blockchain**: è il registro completo delle transazioni compiute all'interno del network.  
Mostra come, da chi e verso chi è stata fatta la transazione.  
La blockchain è pubblica e mostra le transazioni in ordine cronologico.

> Naviga nella blockchain: [Blockchain Explorer](https://blockchain.com/explorer)


### **Il registro di Bitcoin: la Blockchain**

Quando si fa riferimento a un _nodo_ ci si riferisce ad un dispositivo collegato al network di Bitcoin.  

Come ci si collega? Basta scaricare un software, scaricare sul proprio computer la copia della blockchain e collegarsi ad internet, in questo caso saremo dei _full node_ (copia completa della blockchain sul proprio dispositivo `~400GB`)

> Problema I: come si tiene sincronizzata ogni copia della blockchain all'interno del network?  

> Problema II: Come fa un nodo a sapere quale informazione accettare e quale rifiutare, non essendoci nessuna istituzione centralizzata a stabilire le regole?  

La soluzione si è trovata adattando il consenso tra i nodi al Byzantine Generals' Problem (BGP).

### **La sincronizzazione della blockchain**

1. Quando un utente crea una transazione, essa viene trasmessa a tutti i nodi all'interno del network e in pochi secondi la maggior parte dei clients (dispositivi) nel mondo la vedranno.

2. A questo punto la transazione viene etichettata come `unconfirmed` (non confermata). Bisogna verificare se la transazione è fraudolenta o no.

3. Bitcoin conferma la transazione e risolve il Byzantine Generals' Problem attraverso un processo chiamato **_mining_**. Se la transazione viene rifiutata, si ripete il processo.

### **Introduzione al mining e al Proof Of Work**

Da ora chiameremo **_miners_** i nodi che si occupano di verificare e di registrare le transazioni nella blockchain.

Il _mining_ è il processo nel quale un nuovo blocco viene verificato e connesso alla catena di blocchi della blockchain. Quando un _miner_ registra un nuovo blocco viene ricompensato con dei bitcoin, in questo caso diremo che i BTC sono stati **_mintati (minted bitcoins)_**.

Ricordiamo che non ci saranno piu ricompense dopo che il network raggiungerà i `21.000.000 BTC` totali.

L'integrità della transazione e del blocco viene verificata tramite la potenza computazionale del miner con un processo automatico chiamo **_Proof Of Work_**.

Cosa fa il miner:

1. Raggruppa 📦 le transazioni non ancora confermate e le inserisce in un blocco, chiamato _candidate block_ perchè non è ancora sicuro che verrà registrato nella blockchain.

2. Costruisce ⛏️ il _candidate block_ con:
+ una referenza all'ultimo blocco valido della blockchain
+ il _nonce_, un numero casuale usato per il Proof Of Work.  

3. Risolve ⚙️ il Proof Of Work e manda il _candidate block_ al network per farlo verificare agli altri nodi.

4. Se il blocco viene validato ed è quello che è stato creato con più potenza computazionale, il miner riceverà la ricompensa 💰.

Quando si parla di _ricompensa_ ci si riferisce a dei bitcoin che riceverà il miner per aver speso tempo ed elettricità (tenere acceso un macchinario per il mining consuma più di 2kW/h).

La ricompensa è composta da:
+ il _block subsidy_, che fornisce BTC al network ogni volta che un blocco viene creato. Viene dimezzata ogni `210.000 blocchi` (~ 4 anni), per avere un decremento della fornitura di BTC; nel 2008 la ricompensa era di `50 BTC`, oggi è arrivata a `6.25 BTC` per blocco ♦️. 
+ le _fees_, cioè le tasse che paga l'utente per inviare i propri bitcoin.

♦️ Nel 2140, quando si stima che ci saranno i 21M di bitcoin nel network, i miners riceveranno solo più le _fees_ come ricompensa. Oggi ci sono 18M di bitcoin (più dell'80% del totale fissato).

> Cosa succede se 2 miner creano e verificano 2 blocchi, con informazioni (come le transazioni) diverse, allo stesso istante? Quale dei due viene scelto?

Quando un _client_ deve decidere quale blocco accettare, sceglierà ovviamente l'ultimo della catena ma anche quello che è stato creato con più difficoltà, cioè quello che ha avuto bisogno di più potenza computazionale da parte del miner.

Il blocco che viene scartato diventa _orfano_ e le transazioni al suo interno dovranno essere nuovamente inserite in un altro blocco.

### **Lo scopo del Proof of Work**

> Perchè dovrei usare la blockchain ed avere la necessità di tutta questa energia quando posso usare un normale database? 

Perché ciò che sta alla base della blockchain e del suo consenso è la **sicurezza**: l'investimento di potenza computazionale, tempo ed energia aumenta la sicurezza di tutto il sistema! Ad un miner non conviene creare un blocco con informazioni false, perché non verrebbe accettato dal network e quindi consumerebbe energia inutilmente ($$$).

---

<br>

[⬅️ Capitolo Precedente](/capitolo1.md) | [Capitolo Successivo ➡️](/capitolo3.md)
