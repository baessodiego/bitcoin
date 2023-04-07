# Crittografia, Transazioni e Mining

## Indice

1. [Crittografia in Bitcoin](#crittografia)
2. [Funzioni di hash](#funzioni-di-hash)
3. [Crittografia asimmetrica o "a chiave pubblica"](#crittografia-asimmetrica)
4. [Firme digitali](#firme-digitali-digital-signatures)

---

<br>

## Crittografia

L'ecosistema di Bitcoin usa una coppia di chiavi digitali _privata-pubblica_ (relazionate matematicamente), create usando la crittografia ellittica (**ECDSA**: [Elliptic Curve Digital Signature Algorithm](https://it.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm)).

### **Chiave Privata (Privkey)**

È essenzialmente un numero generato casualmente che deve essere mantenuto segreto. La Privkey viene usata per generare le firme digitali, confermare l'autenticità e autorizzare l'invio di bitcoins.

### **Chiave pubblica (Pubkey)**

Viene generata dalla chiave privata con l'utilizzo della crittografia ellittica. Quando si inviano e ricevono bitcoins, la chiave pubblica è rappresentata dall'[indirizzo bitcoin](#indirizzo-bitcoin).

_Immagina la chiave pubblica come il tuo numero del conto della tua banca e la chiave privata come il PIN per accederci che deve essere mantenuto segreto._

### **Indirizzo Bitcoin**

Un indirizzo Bitcoin è quello che identifica la destinazione dei pagamenti in bitcoin. Viene generato dalla chiave pubblica tramite un algoritmo e fa riferimento ad essa.

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

Le funzioni di hash sono ampiamente usate in Bitcoin: per gli indirizzi, negli script e nel PoW.

Quando una transazione viene condivisa con il network, la funzione SHA-256 viene usata per crittografare i dati durante il trasferimento.

Le funzioni di hash vengono utilizzate anche nella blockchain per verificare l'integrità dei blocchi e per stabilire l'ordine cronologico di ogni singolo blocco.

<br>

## Funzioni di hash

Abbiamo imparato che Bitcoin usa SHA-256 come funzione di hash.  
L'output di questa funzione è lunga 256 bits (32 bytes). \*

\* 1 byte = 8 bits

L'hash generato da SHA-256 è solitamente rappresentato da una stringa di 64 caratteri esadecimali, ciò significa che ogni byte è rappresentato da 2 caratteri esadecimali.

[Prova tu a crittografare la parola "Bitcoin" con SHA256](https://emn178.github.io/online-tools/sha256.html).  
Ricorda che i caratteri maiuscoli non generano lo stesso risultato dei minuscoli!

```
# SHA256 (sha256sum)

Bitcoin = b4056df6691f8dc72e56302ddad345d65fead3ead9299609a826e2344eb63aa4

bitcoin = 6b88c087247aa2f07ee1c5956b8e1a9f4c7f892a70e324f1bb3d161e05ca107b
```

## Crittografia asimmetrica

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

## Firme digitali (digital signatures)

In questo paragrafo parleremo delle firme digitali di tipo ECDSA (crittografia ellittica).

Quando un utente effettua una transazione in Bitcoin, questa viene firmata digitalmente utilizzando la chiave privata dell'utente. La firma digitale viene poi trasmessa insieme alla transazione sulla rete Bitcoin.

Una volta che la transazione viene inclusa in un blocco e aggiunta alla blockchain, gli altri nodi della rete Bitcoin utilizzano la chiave pubblica dell'utente per verificare la firma digitale della transazione. In questo modo, gli altri nodi possono confermare che la transazione è stata effettivamente autorizzata dall'utente che possiede la chiave privata corrispondente alla chiave pubblica utilizzata per firmare la transazione.

La verifica della firma digitale nella blockchain di Bitcoin è un processo critico per garantire l'integrità e la sicurezza della rete. Poiché la blockchain di Bitcoin è immutabile, una volta che una transazione è stata confermata e aggiunta alla blockchain, non può essere modificata o annullata.

- Per effettuare un pagamento, viene generata una transazione `T`.
- Un sottoinsieme delle informazioni `M` della transazione `T` viene _firmato_.

### **Firmare una transazione `T`**

1. La transazione `T` viene creata.
2. Si selezionano delle informazioni `M` riguardo alla transazione `T`, come l'ID della transazione, le istruzioni riguardo al trasferimento ecc...
3. Si calcola l'hash `H` delle informazioni `M` (`H = SHA256(M)`).
4. Si calcola la firma digitale `S` usando l'output di una funzione di hash `Fhash` usando come parametro la chiave privata `Kpriv` del mittente.
5. Si manda ai _miners_ sia la firma `S` che la chiave pubblica `Kpub` insieme alla transazione `T`.

$\ S = Fsign(Fhash(M), Kpriv) $

$Fhash$ = funzione che calcola l'hash `H` delle informazioni `M`;
$Fsign$ = funzione per firmare con parametri `(H, Kpriv)` che produrrà i valori `R` ed `S`;

### **Verificare una transazione `T`**

La verifica non è altro che la funzione inversa della firma.  
Per verificare una transazione bisognerà avere la _firma digitale_ (con i valori `R` ed `S`) e la _chiave pubblica_ per trovare il punto `P`, che è un punto che si trova sulla curva ellittica.

$\ P = (S^{-1} \times Fhash(M) \times G) + (S^{-1} \times R \times Kpub)$
