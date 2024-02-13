# Ownership and references 
Tornando all'esempio della lezione precedente: ma se presto il gioco a un mio amico il gioco rimane mio? Oppure diventa suo? Posso prestarlo a più persone insieme? E se un giorno bisogna buttarlo via perché occupa spazio, chi se ne deve occupare?

Ovviamente e immancabilmente rust ha delle regole ferree (lol, questa era pessima) per gestire questi problemi, e nulla viene lasciato al caso.

# Ownership
Come dice il nome, di chi è l'oggetto?
Facciamo un esempio.
```rust
fn test(x: i32){
    // ho io la proprietà di x? forse
    print("{}", x);
}
let x=3;
// adesso abbiamo chiaramente la proprietà di x
test(3);
// e dopo l'esecuzione della funzione ho ancora la proprietà di x?
```
Questo concetto è fondamentale in rust, perché quando finisce lo "scope" (blocco di esecuzioni di codice) tutte le variabili in mio possesso vengono liberate dalla ram (quindi non c'è bisogno di garbage collector o simili porcherie).
Nel esempio precedente test prende l'ownership di x, e pertanto sarà compito suo de-allocarla. Quindi se nel blocco di codice iniziale provo ad accedere a x, dopo l'esecuzione della funzione test, il compilatore si lamenterà che il valore non è più presente.


