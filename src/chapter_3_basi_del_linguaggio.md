
# Variabili
Non possiamo iniziare a programmare senza sapere come dichiarare e inizializzare le variabili!
Rust è un typed language (grazie a dio), e pertanto deve sempre sapere in ogni momento di che tipo è una variabile, e a meno che non gli diciamo altrimenti il tipo non cambia mai.
Per dichiarare una variabile basta scrivere
```rust 
let <nome_variabile>: <tipo> = <valore>;
```
Dove per un semplice intero possiamo scrivere i32 (intero a 32 bit), e assegnare un intero:
```rust 
let primo_intero: i32 = 3;
```
se volete sperimentare con altri tipi, quelli base sono:
- i8: intero a 8 bit
- i16: intero a 16 bit
- i32: intero a 32 bit
- u8: intero senza segno a 8 bit
- u16: intero senza segno a 16 bit
- u32: intero senza segno a 32 bit
- f32: float a 32 bit
- &str: stringhe
- String: stringhe più belle, ne parliamo più avanti

### Esercizi
- Provate a dichiarare una variabile e a visualizzarla nel println! (consiglio, cercate la documentazione online su come println funziona )
- Provate a fare un po' di aritmetica: sommare/dividere interi, e a visualizzare il risultato
- provate a sommare 2 stringhe (questo è un po' più difficile)

# If/Else
Ogni linguaggio ha un modo per definire se questa condizione è valida esegui questo codice. In rust esiste l'if:
```rust
// NB le parentesi grafe sono obbligatorie, mentre le parentesi tonde intorno alla condizione sono sconsigliate
if condizione{
    //se la condizione è vera
    //codice
}else{
    //se la condizione è falsa
    //codice
}
```
### Esercizi
- se un numero è uguale a 0 eseguo del codice altrimenti no
- TODO altri es 

# Cicli
E se volessimo ripetere del codice?
```rust
while condizione{
    //ripeti codice fino a quando la condizione è vera
    //codice
}


for i in range{
    //ripeti codice per ogni valore dentro a range
    // esempi di range:
    // 0..10 da 0 a 10 con 0 incluso e 10 escluso
    // 0..=10 da 0 a 10 con 0 e 10 inclusi
    //codice
}
loop{
    //ripeti questo codice all'infinito
}
//all'interno di ogniuno di questi cicli è possibile usare
break; //esci dal ciclo subito
continue; //salta alla prossima iterazione del ciclo
```
### Esercizi
- Incrementare un valore per 10 volte
- eseguire un ciclo fino a quando non viene verificata una condizione 

# Funzioni
Per chi non conoscesse il concetto delle funzioni, possiamo vederlo come un "insieme di comandi", che prende in input dei parametri e a volte da in output un valore.
In rust la sintassi è:
```rust

///questa funzione non da in output niente
fn nome_funzione(parametri){

}

///invece questa funzione da in output un intero
fn ritorno_per_due(val: i32)->i32{
    2*val
}

///invece questa funzione da in output un intero (stessa di sopra)
fn ritorno_per_due(val: i32)->i32{
    return 2*val;
}

//per chiamare una funzione basta passare i parametri, e leggere il risultato:
let risultato = ritorno_per_due(4);
///... faccio altro

// il valore di ritorno può essere semplicemente inserito come ultimo valore della funzione (SENZA ;) oppure con un return valore; (vedi esempi sopra)
```

### Esercizi
- Scrivere una funzione per visualizzare a schermo un testo, e richiamarla più volte
- Scrivere una funzione che prenda più parametri, e li combini insieme (ad esempio moltiplicazione tra 2 interi)
- Scrivere una funzione, che chiama altre funzioni, che chiamano altre funzioni... divertitevi
- (per chi conosce le funzioni) fare una funzione ricorsiva (ad esempio fibonacci ricorsivo)
- (difficile )provare a mutare un valore preso come argomento (vedi prossimo capitolo)
