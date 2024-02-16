# Mutabilità e visibilità
Vi è mai capitato di non voler prestare un gioco della playstation a un amico?
E se me lo rompe? E se non me lo restituisse? E se volessi tenere il mio tessssoro solo per me?
Ovviamente rust aiuta con questi problemi (digitalmente parlando), con due strumenti fondamentali.

## Mutabilità
Una variabile deve essere modificabile? Allora la dichiaro come modificabile, altrimenti una volta inizializzata è in sola lettura (default). La decisione di cosa deve essere modificabile deve essere fatta oculatamente per evitare il rischio di fare danni.
Un esempio: se passo dei soldi a una funzione (immaginate esista il tipo soldi), lascio l'utente della funzione modificarli a piacere? Ovviamente se è un proprietario della banca può vedere ma non toccare niente, e invece l'utente può solo aumentare o calare i soldi attraverso delle funzioni ben definite (ad esempio con un versamento).
Da una variabile non mutabile è impossibile creare una variabile mutabile (salvo in alcuni casi attraverso una definizione di una nuova variabile, o strutture particolari).

La mutabilità è riferita alle variabili.

## Visibilità
La funzione "aggiungi soldi al conto corrente" non deve essere chiamabile da chiunque, ma solo da alcuni specifici macchinari della banca (ad esempio i bancomat). Ecco che rust ci da uno strumento per decidere cosa e quando devono essere visibili le funzioni.
Ad esempio per generare una funzione pubblica è necessario aggiungere pub davanti alla dichiarazione:
```rust
pub fn sono_in_tv_mamma(mut io_sono_modificabile: i32, io_sono_immutabile: i32){
    println!("prima modifiche: {} {}", io_sono_modificabile, io_sono_immutabile);
    io_sono_modificabile=0;
    //io_sono_immutabile =3;
    //impossibile modificare una variabile immutabile, il compilatore si lamenta
    println!("dopo modifiche: {} {}", io_sono_modificabile, io_sono_immutabile);
}
sono_in_tv_mamma(4, 7);
```
A volte però ci interessa rendere delle funzioni visibili ma non troppo. Un modo per farlo è specificare dove deve essere visibile:
```rust
mod modulo{
    pub (crate) fn test(){}
    pub (self) fn test1(){}
    pub (super) fn test2(){}
    // pub(in crate::modulo) fn test3(){}
    // nel playground non compila, ma anche i path si possono usare
}
//ecc
```
Inoltre ci sono varie tecniche avanzate (re-exports e simili) per specificare bene come deve essere visibile. Le vedremo al bisogno

Le regole sulla visibilità valgono per moduli, strutture, funzioni, trait...

### Esercizi
- creare delle funzioni pubbliche, e vederle da un altro modulo.
- 