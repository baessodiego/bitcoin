# Tipi di blockchain

## Indice

1. [La blockchain di Bitcoin](#la-blockchain-di-bitcoin)
2. [Tipologie di blockchain](#principali-tipologie-di-blockchain-in-base-allautorizzazione--permesso)
3. [Algoritmi per il consenso](#principali-algoritmi-per-il-consenso)
4. [La blockchain di Ethereum e gli Smart Conctracts](#la-blockchain-di-ethereum-e-gli-smart-contracts)




## **La blockchain di Bitcoin**

Le proprietà della blockchain di Bitcoin sono:

+ **Pubblica**: tutte le transazioni nel network sono pubblicamente verificabili e disponibili a tutti.
+ **Aperta**: chiunque può entrare o uscire dal network, validare le transazioni e minare bitcoins.
+ **Peer-to-peer** : le transazioni non hanno bisogno di intermediari o autorità centralizzate, ma sono inviate da un nodo all'altro.
+ **Distribuita**: è conservata e validata in tutto il mondo da una grande varietà di nodi nel network (_full nodes_).
+ **Sicura**: grazie al consenso, finchè il 50% dei nodi all'interno del network sarà onesto.
+ **Affidabile**: non essendoci un operatore centralizzato, il network è mantenuto online grazie ai nodi sparsi nel globo 24/7, tutti i giorni dell'anno.
+ **Immutabile**: modificare la blockchain diventa sempre più computazionalmente difficile, poichè l'aumento di difficoltà implica un fabbisogno di energia più alto.
+ **No autorizzazioni**: non c'è bisogno di credenziali, autorizzazioni o verifiche per entrare nel network.
+ **No restrizioni geografiche**: basta la connessione internet o satellitare per entrare nel network, in ogni parte del mondo.
+ **Resistente alla censura**: nessuno ha il potere di bloccare una transazione finchè è una transazione che rispetta le regole del consenso.
+ **Neutrale**: il network di Bitcoin è agnostico rispetto agli account che mandano e ricevono bitcoins.  
  Non bloccherà un account neanche se scambierà bitcoin per scopi illegali.

<br>

## **Principali tipologie di blockchain in base all'autorizzazione / permesso**

| Blockchain |                               | Leggere                                                      | Scrivere              | Fare commits                            | Esempi                                                       |
| :--------- | :---------------------------- | :----------------------------------------------------------- | :-------------------- | :-------------------------------------- | :----------------------------------------------------------- |
| **APERTA** | Pubblica senza autorizzazione | Aperta a tutti                                               | Tutti                 | Tutti                                   | Bitcoin, Ethereum                                            |
| **APERTA** | Pubblica con autorizzazione   | Aperta a tutti                                               | Utenti autorizzati    | Tutti o una parte di utenti autorizzati | Registro delle transazioni di un'azienda visible al pubblico |
| **CHIUSA** | Privata o "consorzio"         | Ristretta ad un gruppo di utenti autorizzati                 | Utenti autorizzati    | Tutti o una parte di utenti autorizzati | Registro condiviso fra 2 banche                              |
| **CHIUSA** | Privata con permessi          | Privata o ristretta ad un piccolo gruppo di nodi autorizzati | Operatori del network | Operatori del network                   | Registro di una banca esterna condiviso con un'azienda       |

<br>

### **Blockchain aperte, pubbliche e senza autorizzazione**

Le caratteristiche di questa tipologia di blockchain, come quella di Bitcoin, sono:

+ Chiunque può entrare e uscire dal network.
+ Chiunque può mantenere una copia dell'intera blockchain e operare come _full-node_.
+ La blockchain è pubblica, disponibile a tutti.
+ Non c'è bisogno di credenziali per entrare.
+ Per entrare nel network basta scaricare un software.
+ Non c'è bisogno di conoscere l'identità degli altri nodi.

Le più famose blockchain che cadono in questa tipologia sono **Bitcoin** (2009), **Litecoin** (2011), **Monero** (2014) ed **Ethereum** (2015).

Ognuna di queste blockchain ha la propria valuta, bitcoin per Bitcoin, ether per Ethereum e così via.

Usano tutte il Proof of Work; [nel 2022 Ethereum ha lanciato l'ultima versione del suo Proof of Stake](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/).

<br>

### **Blockchain aperte, pubbliche e con autorizzazione**

Le caratteristiche di questa tipologia di blockchain sono:

+ Non tutti possono entrare nel network.
+ Le credenziali o l'autorizzazione sono fornite ad un gruppo identificato di partecipanti nel network.
+ Questo requisito aggiunge un ulteriore livello di sicurezza, dove nei casi in cui manca un robusto algoritmo per il consenso risulta molto utile.
+ Ogni nodo è riconosciuto dagli altri nodi all'interno del network.

In alcuni casi in questo tipo di blockchain si possono anche definire i _ruoli_ per ogni nodo presente nel network. Ad esempio si può definire:

+ Chi può operare come nodo.
+ Chi può validare le transazioni.
+ Chi può modificare il sistema.
+ Ecc...

> Un esempio di blockchain con autorizzazione è **Ripple**

<br>

### **Blockchain a consorzio (private)**

Questo tipo di blockchain viene utilizzato da aziende e da organizzazioni che hanno come fine quello di scambiare transazioni all'interno di una cerchia ristretta di partecipanti.

> **Hyperledger**, **Corda** e **Quorum** sono 3 esempi di blockchain a consorzio

<br>

---

<br>

## **Principali algoritmi per il consenso**

Ci sono vari algoritmi per il consenso oltre al Proof Of Work, quello usato da Bitcoin.

Possono variare in base a varie caratteristiche:

- Performance
- Velocità delle transazioni
- Scalabilità
- Governance
- Privacy

| Algoritmo                       | I partecipanti devono                                                                                                | Decentralizzazione                                                                                                                           |
| :------------------------------ | :------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------- |
| Proof of Work (PoW)             | Investire in energia e macchinari appositi per il mining (queste non sono richieste per i non-mining node)           | È l'algoritmo più testato; la decentralizzazione completa è possibile e dipende dall'accessibilità delle risorse energetiche e dell'hardware |
| Proof of Stake (PoS)            | Investire denaro e _tenere in stake_ una significante quantità di coins di quella determinata blockchain             | Con un'equa distribuzione dello stake diventa totalmente decentralizzata                                                                     |
| Delegated Proof of Stake (DPoS) | Come il PoS ma c'è un meccanismo di votazioni per delegare il potere decisionale ad un nodo rispetto che ad un altro | È il meno usato e testato ma permette una decentralizzazione più facile rispetto al PoS                                                      |

<br>

---

<br>

## **La blockchain di Ethereum e gli Smart Contracts**

La blockchain di Ethereum è aperta, pubblica e senza autorizzazione come quella di Bitcoin.

**Ethereum** è stato proposto nel `2013` da Vitalik Buterin. Dopo 2 anni, il `30 Luglio 2015` il newtork andò online, descritto come una _piattaforma rivoluzionaria_ per le applicazioni decentralizzate.

Le nuove features di Ethereum sono:

- Un linguaggio di programmazione ad oggetti chiamato Solidity per facilitare la creazione delle applicazioni decentralizzate e degli smart contracts.
- La sua valuta nativa chiamata _ether_ che può essere tracciata all'interno della blockchain ed è usata più come _fuel_ per fare transazioni che come valuta.

### Caratteristiche della blockchain di Ethereum

- Con il _genesis block_ nel 2015, sono stati generati `72 milioni` di ETH. Ad oggi ci sono `120 milioni` di ETH in circolazione e non esiste un tetto massimo come per Bitcoin.
- La capitalizzazione di mercato di ETH supera i `200$ miliardi`, marzo 2023.
- Il tempo di generazione di un blocco è di `~13 secondi`.
- I nodi devono validare più informazioni rispetto ai soli pagamenti (come per Bitcoin). Il peso di un blocco è mediamente di `100KB (kilobytes)`. Nel 2020 era di soli 30KB.

### I più importanti aggiornamenti di Ethereum

- **Frontier** `30 Luglio 2015`
- **Homestead** `15 Marzo 2016`
- **Metropolis** `16 Ottobre 2017`
- **Istanbul** `8 Dicembre 2019`
- **Serenity** `1 Dicembre 2020`





