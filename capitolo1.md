# Perché Bitcoin?

Prima di introdurre il concetto di Bitcoin è importante definire quali sono le proprietà e le funzioni di una valuta.

## Le 3 funzioni principali di una valùta

1. Mezzo di scambio
2. Unità di conto
3. Riserva di valore

### 1. Mezzo di scambio

È lo strumento _intermediario_ che viene usato per facilitare lo scambio di beni e servizi, ad oggi è la moneta / banconota nazionale (€, $, ¥, ...).

> Quali sono i punti chiave di un buon mezzo di scambio?

- **Durabilità**: capacità della valuta nel durare nel tempo senza rovinarsi (es. le _monete_).
- **Trasportabilità**: facilità del trasferimento della valuta (es. trasferimento di denaro _online_).
- **Divisibilità**: può una valuta essere divisa? Come? In quante parti? (10€ possono essere divisi in 2 da 5€; 1€ in 100 centesimi...).
- **Fungibilità**: il valore di una unità della valuta deve essere uguale al valore di una qualunque altra valuta dello stesso valore.
- **Autenticità**: una valuta deve essere difficilmente contraffabile.

### 2. Unità di conto

Il prezzo di un bene e/o servizio deve essere espresso in una valuta, nient'altro. In questo modo il prezzo indicherà il valore di ciò che si compra, questo cambia in ogni nazione.

_Se entro in un negozio per comprare un telefono, il prezzo di quest'ultimo sarà espresso in Euro (€) non in oro, mucche o cammelli._

> Cosa rende buona un'unità di conto?

- **Stabilità**: Nel breve-termine la valuta di ogni nazione è stabile, per ora più stabile delle cryptocurrencies.  
  Nel lungo termine ci sarà il problema dell'_inflazione_\*.  
  \* La valuta perde valore nel tempo quindi l'economia dovrà essere corretta in base all'aumento dell'inflazione.

### 3. Riserva di valore

È un _meccanismo_ secondo il quale la ricchezza può essere salvata nel lungo termine, prevedendo il valore della valuta nel futuro.  
Non esiste un asset che abbia una perfetta riserva di valore, dato che non si può determinare al 100% il valore futuro.

> Cosa spinge un asset a essere una riserva di valore?

- L'aspettativa della domanda di quella risorsa nel futuro
- L'aspettativa del supplemento / offerta di quella risorsa nel futuro

> Quali sono le migliori riserve di valore oggi?

- Metalli (**Oro**, argento, diamanti)
- Stocks, bonds, immobiliare
- Riserve della valuta nazionale

---

Come ci siamo arrivati ad usare il denaro come lo conosciamo oggi? Un piccolo riassunto della storia della moneta può essere utile.

## Dal baratto al Bitcoin

### **Cosa usare per lo scambio di beni e servizi?**

> I soluzione: il baratto

Nella storia per risolvere il problema dello scambio si risolse con il **baratto**.  
Il problema del baratto è che ci deve essere una _doppia coincidenza della domanda / offerta_: se ho bisogno di una mucca e possiedo solo grano, devo trovare qualcuno con una mucca e che allo stesso tempo abbia bisogno di grano.

> II soluzione: derivati della moneta

Per porre rimedio al problema della _doppia coincidenza di domanda_ si cominciò ad usare un derivato della futura moneta, come tabacco, conchiglie, mucche, grano.  
Il problema è che queste cose avevano una scarsa trasportabilità e durabilià.

> III soluzione: monete create con metalli preziosi

Si risolse così il problema della trasportabilità e della durevolezza ma si andò incontro al problema legato alla divisibilità, alla fungibilità (non tutte le monete erano perfettamente uguali) e all'autenticità (era difficile capire se il metallo utilizzato era prezioso o meno).

Più avanti si cominciarono a usare monete e banconote senza un valore effettivo che però erano esclusivamente legate al valore di un metallo prezioso tenuto nelle prime banche (es. una banconota valeva una quantità X di oro, che poteva essere riscattato nella propria banca).

> IV soluzione: valute FIAT

Le valute FIAT (quelle che si usano tutt'oggi in tutto il mondo) risolsero tutti i problemi precedenti.

Le valute FIAT sono definite come _valuta_ dalla legge governativa di una nazione e non sono sostenute dal valore di un bene fisico (come l'oro).

_Se sei interessato a conoscere più in dettaglio la storia della moneta puoi visitare questa pagina:
[Approfondimento: Storia della moneta](https://en.wikipedia.org/wiki/History_of_coins)_

### **Chi tiene traccia delle transazioni?**

Senza nessuno che abbia un registro delle transazioni tra persone e/o servizi si andrebbe incontro a molti problemi.

> Soluzione: le banche

La banca è un ente di terze parti sicuro che tiene traccia delle transazioni tra due persone / servizi tramite il _ledger_.

**Ledger**: registro di tutte le transazioni.

Grazie a questo registro si possono prevenire problemi come il _Double spending problem_.

### Double spending problem

Esempio: Joe vuole inviare 10€ a Chris.

```
Conto di Joe: 10€
Conto di Chris: 0€
```

Quando Joe invierà i soldi a Chris, il ledger registrerà la transazione e aggiorenrà il saldo di entrambi.

```
Joe => Chris
Conto di Joe: 0€ [-10€]
Conto di Chris: 10€ [+10€]
- transazione accettata ✅ -
```

Se il nuovo saldo di Joe sarà inferiore all'ammontare che vorrà inviare nel futuro, la transazione verrà bloccata.

```
Joe => Marco
Conto di Joe: 0€
- transazione bloccata ❌ -
```

I principali problemi che si hanno con le banche sono 2:
+ **Tempo**: il tempo totale della transazione dipende al 100% dalle banche di Joe e di Chris.
+ **Tracciabilità**: non è sempre facile tenere traccia delle transazioni, che potrebbero venire manomesse.

---

## Bitcoin come valuta?


Il _bitcoin_ (BTC) è una moneta digitale che utilizza la _blockchain_ per facilitare le transazioni finanziarie.  

\* **B**itcoin: ci si riferisce all'ecosistema intorno alla moneta digitale e alla blockchain.  
\* **b**itcoin: fa riferimento alla moneta.
 
### **Perché usare Bitcoin?**

Parametri principali:
+ **Privato**: non è rilasciato da un'autorità ufficiale.
+ **Decentralizzato**: non c'è un ente centralizzato per il controllo / rilascio delle monete, che sono invece rilasciate da un gruppo decentralizzato di utenti nel mondo.
+ **Digitale**: è completamente digitale, non esistono monete o banconote fisiche.
+ **Anti-contraffazione**: è quasi impossibile contraffarre una transazione grazie a un mix di _crittografia_ e di _game theory_.

### **La blockchain**

La più importante innovazione è il concetto di **blockchain**, un ledger pubblicamente accessibile che contiene la registrazione di ogni singola transazione di bitcoin, senza avere un operatore centralizzato.  

Bitcoin funge da mezzo di scambio nel network.


### **Politiche monetarie di Bitcoin**

+ **Supplemento fisso**: il supplemento totale di Bitcoin è regolamentato dal suo stesso protocollo che impone il limite a `21.000.000 bitcoin (BTC)`.
+ **Programma di emissione decrescente**: vengono generati (ad oggi, gennaio 2023) `6.25 BTC` ogni ~10 minuti.  
Questo valore viene dimezzato ogni ~4 anni (il prossimo dimezzamento a `3.125 BTC` avverrà a Marzo 2024).
+ **Policy trasparenti**: queste regole sono accessibili da chiunque e possono essere esaminate e verificate, grazie al protocollo _open-source_ di Bitcoin.
+ **Guidato dal "consenso"**: ogni può accettare le regole proposte dal protocollo e proporne di nuove (che verranno poi verificate ed accettate dai developers del Bitcoin Core). Le caratteristiche / regole principali possono essere modificate solo quando la maggioranza darà il proprio consenso.

### **Bitcoin come mezzo di scambio**

Messo a paragone con i mezzi di scambio del passato.

+ Durevole: la blockchain ha un backup copiato su migliaia di computer in tutto il mondo.
+ Portatile: non ci sono intermediari.
+ Fungibile: ogni BTC ha lo stesso valore. Oggi però ci sono dei registri in cui sono segnalati i BTC _sporchi_, cioè quelli usati e ricavati da attività illecite.
+ Divisibile: ogni BTC può essere diviso fino a 100 milioni di unità. La più piccola unità del bitcoin si chiama **satoshi**.
+ difficile da contraffare: ogni BTC è assegnato a un specifico indirizzo e questo può essere verifricato da tutti i nodi all'interno della blockchain.

Nel [prossimo capitolo](/capitolo2.md) approfondiremo l'importanza del ledger e di come il creatore di Bitcoin, Satoshi Nakamoto, trovò il modo per renderlo decentralizzato.