# Ownership and references 
Tornando all'esempio della lezione precedente: ma se presto il gioco a un mio amico il gioco rimane mio? Oppure diventa suo? Posso prestarlo a più persone contemporaneamente? E se un giorno bisogna buttarlo via perché occupa spazio nel solaio, chi se ne deve occupare?

Ovviamente e immancabilmente rust ha delle regole ferree (lol, questa era pessima) per gestire questi problemi, e nulla viene lasciato al caso.

# Ownership 
<div class="warning">
ATTENZIONE, SPESSO NON PRESENTE IN ALTRI LINGUAGGI.
</div>
Come dice il nome, di chi è l'oggetto?
Facciamo un esempio.

```rust
fn test(x: i32){
    // ho io la proprietà di x? forse
    print!("{}", x);
}
let mut x=3;
// adesso abbiamo chiaramente la proprietà di x
test(x);
// e dopo l'esecuzione della funzione ho ancora la proprietà di x?
```

Questo concetto è fondamentale in rust, perché quando finisce lo "scope" (blocco di esecuzioni di codice) tutte le variabili in mio possesso vengono liberate dalla ram (quindi non c'è bisogno di garbage collector o simili porcherie).
Nel esempio precedente test prende l'ownership di x, e pertanto sarà compito suo de-allocarla. Quindi se nel blocco di codice iniziale provo ad accedere a x, dopo l'esecuzione della funzione test, il compilatore si lamenterà che il valore non è più presente.

E invece, come faccio a "prestare" un oggetto in modo che la proprietà rimanga mia? Passandolo per reference. Tornando all'esempio di prima, il gioco rimane a casa mia, ma se il mio amico vuole accederci sa come entrare in casa e dove trovare il gioco. E ovviamente esistono le reference mutabili e quelle immutabili (guardare e non toccare).

l'esempio sopra riscritto diventa così:
```rust
fn test(x: &i32){
    // non ho l'ownership, ed inoltre non posso modificarlo
    print!("{}", x);
}

let mut x=3;
// proprietà di x
test(&x);
// ho ancora la proprietà, e pertanto posso farci altre operazioni
x=7;
```

Quante reference posso avere? Sono illimitate?
Le regole sono queste: 
- la mutabilità è sempre unica, non è possibile che ci siano 2 reference mutabili (se 2 persone modificano insieme cosa succede?)
- se "sacrifico" la mutabilità posso avere infinite reference immutabili (tutti guardano i dati, ma nessuno può modificarlo)
    (non può esistere una reference mutabile e una immutabile contemporaneamente. Cosa succederebbe se qualcuno modifica mentre qualcun'altro sta leggendo?)

## Esercizi
- scrivere una funzione "visualizza_numero" che prenda in input una reference immutabile (e provare a modificare il valore originario)
- scrivere una funzione "moltiplica per due" che non ritorni niente, ma prenda una reference come input
- provare a prendere due reference mutabili della stessa variabile
- cercare di capire chi ha l'ownership
