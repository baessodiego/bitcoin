# Crittografia, Transazioni e Mining

## Indice

1. [Crittografia in Bitcoin](#crittografia)
2. [Funzioni di hash](#funzioni-di-hash)
3. [Crittografia asimmetrica o "a chiave pubblica"](#crittografia-asimmetrica)
4. [Firme digitali](#firme-digitali-digital-signatures)
5. [Transazioni](#transazioni)
5. [Mining](#mining)

---

<br>

## **Crittografia**

L'ecosistema di Bitcoin usa una coppia di chiavi digitali _privata-pubblica_ (relazionate matematicamente), create usando la crittografia ellittica (**ECDSA**: [Elliptic Curve Digital Signature Algorithm](https://it.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm)).

### **Chiave Privata (Privkey)**

È essenzialmente un numero generato casualmente che deve essere mantenuto segreto. La Privkey viene usata per generare le firme digitali, confermare l'autenticità e autorizzare l'invio di bitcoins.

### **Chiave pubblica (Pubkey)**

Viene generata dalla chiave privata con l'utilizzo della crittografia ellittica. Quando si inviano e ricevono bitcoins, la chiave pubblica è rappresentata dall'[indirizzo bitcoin](#indirizzo-bitcoin).

_Immagina la chiave pubblica come il tuo numero del conto della tua banca e la chiave privata come il PIN per accederci che deve essere mantenuto segreto._

### **Indirizzo Bitcoin**

Un [indirizzo Bitcoin](#indirizzi-bitcoin) è quello che identifica la destinazione dei pagamenti in bitcoin. Viene generato dalla chiave pubblica tramite un algoritmo e fa riferimento ad essa.

È generalmente generato usando le funzioni di hash **SHA256** e **RIPEMD-160** in serie sulla chiave pubblica.

Questa serie di caratteri viene poi codificata usando la codificazione **Base58** per renderlo più leggibile.  
58 sono i caratteri alfanumerici di questa codificazione.

> Perchè 58?

Ci sono 52 caratteri nell'alfabeto (26 maiuscoli e 26 minuscoli) + 10 numeri (da 0 a 9).
Di questi 62, Satoshi ne rimosse 4 per non confondere numeri e lettere, cioè: la lettera 'O' e il numero `0`, la lettera maiuscola 'I' (i) e la lettera minuscola 'l' (elle).

<br>

> RECAP degli algoritmi usati

- Chiave Privata: `C4bbcb1fbec99d65bf59d85c8cb62ee2db963f0fe106f483d9 afa73bd4e39a8a`

⚙️ _ECDSA_ (Chiave privata)

- Chiave Pubblica:
  `0478d430274f8c5ec1321338151e927f4c676a008bdf8638d07c0b6be9ab35c71a1518063243acd4dfe96b66e3f2ec8013c8e072cd09b3834a1981659cc345`

⚙️ _RIPEMD-160_ (_SHA256_ (Chiave pubblica))

- Indirizzo bitcoin con scarsa leggibilità:
  `c4c5d791fcb4654a1ef5e03fe0ad3d9c598f9827`

⚙️ _Base58_ (Indirizzo)

- ✅ Indirizzo bitcoin:
  `1JwSSubhmg6iPtRityqhUYYH7bZq3Lfy1T`

<br>

Nella maggior parte dei casi sia la chiave privata che la chiave pubblica sono contenute nel wallet.

![chiave privata e pubblica](/img/cap4/chiaveprivata-terminal.jpeg)

La chiave privata collegata alla chiave pubblica (e quindi all'indirizzo BTC) è:
`L3nzYUMrpMua59tqgnR7Gk37nvr5458auGzXRWQnUWY5fuZCu6ab`

La chiave pubblica (indirizzo bitcoin) è:
`1aavsnddTKS3fWFiW83tOVWqHCZY+pFAd`

<br>

---

<br>

## **Funzioni di hash**

Le funzioni di hash sono ampiamente usate in Bitcoin: per gli indirizzi, negli script e nel PoW.

Quando una transazione viene condivisa con il network, la funzione SHA-256 viene usata per crittografare i dati durante il trasferimento.

Le funzioni di hash vengono utilizzate anche nella blockchain per verificare l'integrità dei blocchi e per stabilire l'ordine cronologico di ogni singolo blocco.

Abbiamo imparato che Bitcoin usa SHA-256 come funzione di hash.  
L'output di questa funzione è lunga 256 bits (32 bytes). \*

\* `1 byte = 8 bits`

L'hash generato da SHA-256 è solitamente rappresentato da una stringa di 64 caratteri esadecimali, ciò significa che ogni byte è rappresentato da 2 caratteri esadecimali.

[Prova tu a crittografare la parola "Bitcoin" con SHA256](https://emn178.github.io/online-tools/sha256.html).

Ricorda che i caratteri maiuscoli non generano lo stesso risultato dei minuscoli!

```
# SHA256 (sha256sum)

Bitcoin = b4056df6691f8dc72e56302ddad345d65fead3ead9299609a826e2344eb63aa4

bitcoin = 6b88c087247aa2f07ee1c5956b8e1a9f4c7f892a70e324f1bb3d161e05ca107b
```

<br>

---

<br>

## **Crittografia asimmetrica**

La crittografia asimmetrica, anche conosciuta come crittografia a chiave pubblica, viene usata per condividere le informazioni tramite una coppia di chiavi.

Vengono usate 2 chiavi:

- **Chiave Privata (`Kpriv`)**, che deve essere mantenuta segreta dal proprietario.
- **Chiave Pubblica (`Kpub`)**, che è visibile a tutti.

Quando si cripta un messaggio, il mittente cripta il messaggio `M` usando la chiave pubblica del destinatario per produrre il messaggio `C`.

Il destinatario decripterà il messaggio criptato `C` usando la propria chiave privata per vedere il messaggio originale `M`.

- **M** è il messaggio non ancora criptato / decriptato, chiamato anche _plaintext_.
- **C** è il messaggio criptato, chiamato anche _ciphertext_.

```js
C = encypt(M, Kpub);
M = decrypt(C, Kpriv);
```

⚠️ È praticamente impossibile trovare la chiave privata partendo dalla pubblica. Un giorno potrebbe diventare possibile tramite l'[utilizzo dei computer quantistici](https://edge9.hwupgrade.it/news/innovazione/i-bitcoin-non-saranno-a-rischio-per-i-computer-quantistici-ancora-per-diverso-tempo_104562.html).

Questo tipo di crittografia, a chiave pubblica, viene usato in Bitcoin per generare le firme digitali tramite la crittografia ellittica (ECDSA), nello specifico la curva [secp256k1](https://en.bitcoin.it/wiki/Secp256k1).

In Bitcoin:

1. La **chiave privata**, tenuta segreta dal proprietario, viene usata per _firmare_ un' hash di una transazione che autorizza l'invio delle monete che possiede.

2. La **chiave pubblica**, visibile da tutti una volta che le monete verranno inviate/spese, viene usata per _verificare_ che la corrispondente chiave privata è stata usata per generare la transazione.

<br>

---

<br>

## **Firme digitali (digital signatures)**

In questo paragrafo parleremo delle firme digitali di tipo ECDSA (crittografia ellittica).

Quando un utente effettua una transazione in Bitcoin, questa viene firmata digitalmente utilizzando la chiave privata dell'utente. La firma digitale viene poi trasmessa insieme alla transazione sulla rete Bitcoin.

Una volta che la transazione viene inclusa in un blocco e aggiunta alla blockchain, gli altri nodi della rete Bitcoin utilizzano la chiave pubblica dell'utente per verificare la firma digitale della transazione. In questo modo, gli altri nodi possono confermare che la transazione è stata effettivamente autorizzata dall'utente che possiede la chiave privata corrispondente alla chiave pubblica utilizzata per firmare la transazione.

La verifica della firma digitale nella blockchain di Bitcoin è un processo critico per garantire l'integrità e la sicurezza della rete. Poiché la blockchain di Bitcoin è immutabile, una volta che una transazione è stata confermata e aggiunta alla blockchain, non può essere modificata o annullata.

- Per effettuare un pagamento, viene generata una transazione `T`.
- Un sottoinsieme delle informazioni `M` della transazione `T` viene _firmato_.

### **Firmare una transazione `T`**

1. La transazione `T` viene creata.
2. Si selezionano delle informazioni `M` riguardo alla transazione `T`, come l'ID della transazione, le istruzioni riguardo al trasferimento ecc... `M` sta per "messaggio della transazione".
3. Si calcola l'hash `H` delle informazioni `M` (`H = SHA256(M)`).
4. Si calcola la firma digitale `S` usando l'output di una funzione di hash `Fhash` usando come parametro la chiave privata `Kpriv` del mittente.
5. Si mandano al network (in particolare ai _miners_) la firma `S`, la chiave pubblica `Kpub` e le informazioni `M`.

$\ S = Fsign(Fhash(M), Kpriv) $

$Fhash$ = funzione che calcola l'hash `H` delle informazioni `M`;  
$Fsign$ = funzione per firmare con parametri `(H, Kpriv)` che produrrà i valori `R` ed `S`;

![firmare transazione](/img/cap4/creazione-firma.jpeg)

### **Verificare una transazione `T`**

La verifica non è altro che la funzione inversa della firma.  
Per verificare una transazione bisognerà avere la _firma digitale_ (con i valori `R` ed `S`) e la _chiave pubblica_ per trovare il punto `P`, che è un punto che si trova sulla curva ellittica.

$\ P = (S^{-1} \times Fhash(M) \times G) + (S^{-1} \times R \times Kpub)$

- `R` e `S` sono i valori della firma digitale
- `Kpub` è la chiave pubblica
- `M` è l'insieme di informazioni (firmate) della transazione
- `G` è il _punto generatore_, un punto specifico sulla curva ellittica che viene scelto in modo tale da essere facilmente calcolabile e conosciuto da tutti i partecipanti della rete Bitcoin.

In conclusione, se la coordinata $\ x\ $ del punto `P` appena calcolato è uguale a `R`, allora possiamo veriricare che la firma digitale è valida.

⚠️ In questo processo la chiave privata rimane segreta e NON viene rivelata.

![validazione transazione](/img/cap4/validazione-firma.jpeg)

<br>

---

<br>

## **Transazioni**

### **P2P e nodi**

- Bitcoin viene eseguito su un network **peer-to-peer** (P2P) di computer.
- Gli utenti posseggono delle chiavi digitali che controllano la proprietà dei bitcoins registrati nella blockchain.
- Ogni computer all'interno del network viene chiamato **nodo**.

> Come si diventa un nodo?

Chiunque può diventare un _nodo_ scaricando ed installando il software _open-source_ di Bitcoin.

- Tutti i nodi sono trattati alla stessa maniera, nel sistema nessun nodo può avere la fiducia da solo. La maggioranza dei nodi saranno etichettati come quelli _onesti_, come abbiamo visto dal [Byzantine Generals' Problem](/capitolo2.md#byzantine-generals-problem).

Ci sono 3 tipi di nodi all'interno del network:

- **Full node**: è responsabile di verificare e mantenere i registri di proprietà secondo le regole del consenso.
- **Mining node**: questo nodo si occupa di processare le transazioni e aggiungere nuovi blocchi alla blockchain, in cambio di una ricompensa.
- **Pruned node**: verifica le transazioni e i blocchi ma non conserva l'intera copia della blockchain sul proprio computer, al contrario del full node.

Le transazioni vengono registrati nella blockchain e descrivono il passaggio di proprietà di una quantità di bitcoin da un proprietario all'altro.

<br>

### **Indirizzi Bitcoin**

Un indirizzo Bitcoin ha questo aspetto:

```
1FWQiwK27EnGXb6BiBMRLJvunJQZZPMcGd
```

Le transazioni nella blockchain non registrano le chiavi pubbliche ma invece un astrazione chiamata **_Indirizzo Bitcoin_** (Bitcoin address) per registrare il beneficiario di ciascun importo, consentendo una maggiore flessibilità e leggibilità.

Per creare un indirizzo bitcoin, il client Bitcoin deve prima generare una coppia di di chiavi (pubblica-privata) da un numero casuale, usando la crittografia ellittica ECDSA.

Creazione di un indirizzo:

1. Vengono applicate le funzioni di hash SHA256 e RIPEMD-160 in serie sulla chiave pubblica per generare la `keyHash`.
2. Concatenando `keyHash` e il numero di versione si compone il `data`.
3. Applicando 2 volte di fila la funzione di hash SHA256 sul `data` si genera il `dataHash`.
4. Da quest'ultimo si prendono i primi 4 bytes che verranno usati come `checksum`.
5. L'indirizzo Bitcoin sarà il risultato della concatenazione del `data` e del `checksum` codificato in _Base58_.

![schema creazione indirizzo btc](/img/cap4/creazione-indirizzo-btc.jpeg)

<br>

### **Definizione e tipologie di transazione**

Una transazione di bitcoin dice al network che un nodo ha autorizzato il trasferimento di una certa quantità di BTC ad un altro nodo.

Il nodo che riceverà i BTC, potrà a sua volta spenderli creando un'altra transazione che autorizzerà il trasferimento ad un altro nodo, e così via formando una catena.

Ogni transazione contiene uno o più `inputs`, che possiamo paragonare a degli _addebiti_ sull'account BTC. D'altra parte ci saranno uno o più `outputs`, che possiamo paragonare a dei _depositi_ sull'account BTC.

La somma degli input e la somma degli output non deve necessariamente essere dello stesso valore. Come abbiamo visto nel [capitolo precedente](/capitolo3.md), gli output sono un po' più piccoli rispetto agli input, per via delle _fees_.

Le più comuni tipologie di transazione sono:

⚡️ **Transazione da un indirizzo all'altro**

è formato da _1 input_ e _2 output_; il secondo output spesso include il "resto" che viene successivamente inviato al mittente in automatico.

![transazione1](/img/cap3/transazione-1input2output.png)

```
Input #0 Mittente
Output #0 Destinatario: I transazione
Output #1 Resto che torna al mittente: II transazione
```

⚡️ **Transazione che unisce più input**

è formato da _più di 1 input_ e da un solo _output_; viene spesso usata per sommare diversi output ricevuti in passato come resto ed inviarli come input ad un indirizzo secondario.

![transazione2](/img/cap4/transazione-1output.png)

```
Input #0 Mittente: I transazione
Input #1 Mittente: II transazione
Input #2 Mittente: III transazione
Output #0 Destinatario
```

⚡️ **Transazione che divide l'input in più output**

è formata da un solo _input_ e da diversi _output_; viene usata molto spesso dalle mining pool per pagare ogni miner che ha messo a disposizione la propria macchina per creare un blocco.

![transazione3](/img/cap4/transazione-1input.png)

```
Input #0 Mittente
Output #0 Destinatario: I transazione
Output #1 Destinatario: II transazione
Output #2 Destinatario: III transazione
```

⚡️ **Transazione "block reward"**

questa transazione non ha _input_ e solitamente ha un solo _output_ (il miner o la mining pool). L'input che potrebbe essere visualizzato è creato dalla blockchain e non si riferisce a nessun indirizzo.

![transazione3](/img/cap4/transazione-reward.png)

```
No Input
Output #0 Miner
```


<br>

---

<br>

## **Mining**

Il sistema che tiene su Bitcoin si basa sulla potenza computazionale e su algoritmi. Per mettere insieme un blocco di transazioni e confermare quest'ultimo ci vuole una gigantesca quantità di potenza computazionale.

Grazie al mining per ogni blocco creato viene generata una certa quantità di nuovi bitcoin, come una banca centrale che stampa nuova moneta da mettere in circolazione.

Il mining dà sicurezza alla rete, garantendo che una transazione verrà confermata se e solo quando verrà usata abbastanza potenza computazionale per il blocco che la contiene.  

`+ Blocchi => + Computazione => + Sicurezza`

<br>

### **Algoritmo del Mining**

Il mining consiste in una serie di passaggi ripetuta in loop:

1. **Raggruppare le transazioni** trasmesse sul network in un singolo blocco. Ogni miner può arbitrariamente decidere quale transazione includere nel proprio blocco. Solitamente sceglieranno le transazioni con le fee più alte.
2. **Verificare** che ogni transazione nel blocco sia valida.
3. **Selezionare** il blocco piu recente della catena della blockchain e inserire l'hash (dell'header) di quest'ultimo nel nuovo blocco.
4. **Provare a risolvere il Proof-Of-Work** per il nuovo blocco e nel frattempo controllare l'arrivo di nuovi blocchi dagli altri nodi.

Se verrà trovata una soluzione al Proof-Of-Work, il nuovo blocco verrà aggiunto sulla propria copia (locale) della blockchain che sarà poi trasmessa alla rete peer-to-peer.

La _performance del mining_ viene misurata in computazione di _hash al secondo_.  
La difficoltà aumenta ogni anno. Al momento viene misurata in Exa Hashes al secondo, che sono 1 quintilione di hash al secondo.

`Hashrate aprile 2023 = 347.45 EH/s`

```
H/s = Hash al secondo
KH/s = KiloHash al secondo
...
TH/s = TeraHash al secondo (1,000,000,000,000 H/s)
PH/s = PetaHash al secondo (1000 TH/s)
EH/s = ExaHash al secondo (1000 PH/s)
```
<br>

### **Difficoltà di Mining**

Il tempo di creazione di un nuovo blocco deve restare intorno ai `10 minuti`.  
La difficoltà viene corretta ogni `2016 blocchi`, circa 2 settimane.  

Più miners entrano nella rete peer-to-peer, più il tasso di creazione di un blocco salirà.  
Ma più questo tasso sale, più la difficoltà dovrà alzarsi per compensare. 

<br>

### **Ricompensa per i miners**

Risolvere il Proof-of-Work (POW) richiede molta energia e potenza computazionale, che comporta un costo per la corrente.

Per incoraggiare i partecipanti alla rete ad investire le proprie risorse nel mining, Bitcoin fornisce una ricompensa per ogni blocco creato con successo.

Questa fornitura di ricompense è scritta nel codice di Bitcoin:
+ Ad oggi la ricompensa è di `6.25 BTC`.
+ La ricompensa si dimezza ogni `210,000 blocchi` (ogni ~4 anni).
+ Il prossimo dimezzamento avverrà a Maggio 2024 e la ricompensa diminuirà a `3.125 BTC`.
+ La ricompensa verrà rimossa quando verranno raggiunti i `21 milioni` di BTC in circolazione, intorno all'anno 2140.

Oltre alla ricompensa per la creazione del blocco, i miners guadagnano anche le _fee_ pagate dagli altri utenti per aver effettuato la transazione.

Ci sono 2 modi per minare bitcoin: da soli o in quelle che si chiamano **mining pools**.

<br>

### **Solo Mining**

I miners che minano da soli usano il loro computer personale, o un hardware specializzato nel mining, per risolvere il PoW.

I solo miners verranno pagati solo se riusciranno a risolvere e trovare un nuovo blocco da soli.

Per le persone normali oramai non ha più senso investire nel "solo mining" poichè la difficoltà di mining è diventata troppo alta.

<br>

### **Pool Mining**

Il _pool mining_ è il metodo più usato ad oggi per minare BTC. Ogni miner contribuisce con la propria potenza computazionale per risolvere il Proof-Of-Work come un gruppo.

Quando un blocco viene trovato, il wallet collegato alla _mining pool_ riceve le ricompense per la creazione del blocco e le distribuisce a tutti i partecipanti della pool.

La distribuzione si basa sulla contribuzione (in termini di potenza computazionale) da parte dei miners: il miner che ha messo a disposizione più energia riceverà una ricompensa più alta di quello che ne ha messa a disposizione di meno. Ci sono 3 tipi di schema per la distribuzione della ricompensa:

Per un approfondimento sulle mining pools, sul loro funzionamento e su come distribuiscono la ricompensa dopo aver trovato un blocco, [leggi questo articolo](https://en.wikipedia.org/wiki/Mining_pool).

Questa è una lista delle più grandi pools che lavorano nella blockchain di Bitcoin.

![Lista pools](/img/cap4/pools.png)

<br>

### **Hardware per il mining**

**CPU Mining 🐢**  
All'inizio il mining si poteva fare dal proprio computer usando la CPU. Satoshi Nakamoto usò questo metodo per creare i primi blocchi. Ma quando la difficoltà crebbe si passò a metodi più efficenti.

**GPU Mining 🐇**  
Le GPU (Graphic Processing Units), le schede video, sono più veloci delle CPU per fare calcoli matematici in parallelo, proprio quello che serve nel PoW.

**FPGA (Field Programmable Gate Arrays) ⚡️**  
Sono una via di mezzo tra le CPU/GPU e le ASICs, usate prima dell'avvento di queste ultime.

**ASIC Mining ⚡️⚡️⚡️**  
Le ASICs (Application-Specific Integrated Circuit) sono delle macchine create appositamente per risolvere il PoW, svolgendo esclusivamente l'hashing con SHA-256. Sono molto più potenti ed efficenti rispetto alle GPUs.  
Ad oggi sono l'unica scelta sensata in termini di efficienza economica.

---

<br>

[⬅️ Capitolo Precedente](/capitolo3.md) | [Capitolo Successivo ➡️](/capitolo5.md)
