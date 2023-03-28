# Ledger per le transazioni

Prima di iniziare, alcune utili definizioni: 
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

## Il ruolo del ledger

Il ledger, o registro, è usato per registrare e tenere traccia di tutte le attività economiche, come il trasferimento di denaro, il passaggio di proprietà, ecc...

I beni registrati nel ledger possono essere:
+ tangibili: immobili, veicoli, ...
+ intangibili: denaro, stocks, diritti digitali, ...

### **Ledger centralizzati**

Gli unici ledger che conosciamo ad oggi sono centralizzati, come le banche; (i ledger centralizzati) li diamo per scontati perche sono sempre stati l'unica forma di registro usata.

Ad occuparsi di registrare le nostre attività è un operatore fidato, come la banca (per il trasferimento di denaro) o l'anagrafe (per il registro delle informazioni). Ma questi operatori _fidati_ non sono infallibili.

Le persone / istituzioni incaricate a registrare le nostre attività possono:
+ **non essere affidabili**. _Per esempio potrebbero creare nel registro un falso trasferimento di proprietà_
+ **escludere enti che non approvano**. _Per esempio una banca potrebbe bloccare i bonifici che arrivano da un determinato business._
+ **perdere dati sensibili** in seguito ad attacchi informatici, problemi tecnici o disastri ambientali.
