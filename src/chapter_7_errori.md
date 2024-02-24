# Rust e la gestione degli errori

Durante l'esecuzione di un programma ci sono vari punti in cui possono verificarsi degli errori. È inevitabile, e se si costruisce il software assumendo che gli errori non esistano, ci si ritrova magari con qualcosa con la parvenza di funzionare ma che sotto sotto brulica di bug e vulnerabilità.

Ad esempio, immaginiamo di dover creare un programma con una casella di testo in cui l'utente deve inserire un numero. Mettiamo quindi un bel messaggio che dice "*inserire **solo** numeri qui*", così che l'utente sappia di non dover mettere altri caratteri, e poi nella programmazione del programma assumiamo che l'utente abbia effettivamente seguito l'istruzione. Una volta scritto il codice, testiamo il programma a mano, e confermiamo che va tutto bene, poichè inserendo numeri validi il programma fa le cose giuste. Purtroppo però un giorno arriva un utente che sbadatamente inserisce "1234 ", ovvero un numero *seguito da uno spazio*, nella casella di testo. In base al modo in cui abbiamo scritto la parte del codice che legge numeri dalla casella di testo, possono succedere due cose:
1. non aspettandosi il carattere "spazio", viene lanciata un'eccezione che fa crashare il programma, magari facendo perdere tutti i dati non salvati dell'utente
2. viene generato un errore silenzioso, ad esempio la conversione da testo a numero potrebbe ritornare `-1` per segnalare che c'è stato un errore, pertanto l'utente crede di aver inserito il numero `1234` ed invece il programma ha ricevuto un `-1`

Entrambi questi scenari non sono belli, e possono avvenire nonostante il programma funzioni perfettamente con input corretti. Rust è molto meticoloso su questo aspetto, per cui non esistono nè eccezioni lanciate in modo incontrollato e ingestibile, nè errori silenziosi. Esistono invece i tipi `Result<T, E>` e `Option<T>`, che garantiscono che possiamo ottenere il risultato effettivo di un'operazione se e solo se questa ha avuto successo (eliminando errori silenziosi), e che altrimenti siamo praticamente costretti a gestire l'errore correttamente (eliminando crash incontrollati).

## `Option<T>`

È un tipo che contiene:
- un risultato di tipo `T` se tutto è andato bene, e in tal caso si può costruire con `Some(valore di tipo T)`
- niente se qualcosa è andato storto, e in tal caso si può costruire con `None`

Ad esempio, [la funzione `get()`](https://doc.rust-lang.org/std/primitive.slice.html#method.get) dei vettori (`Vec`) serve per ottenere il valore ad uno specifico indice del vettore, e ritorna un `Option` uguale a `Some(valore)` se esiste un elemento all'indice fornito, altrimenti ritorna `None`. Ad esempio:

```rust
fn main() {
    let vettore = vec![1,7,9];
    // vettore.get() ritorna Option<i32>, dato che il vettore contiene interi i32
    println!("{:?}, {:?}, {:?}", vettore.get(0), vettore.get(2), vettore.get(7));
    // Some(1), Some(9), None
}
```

## `Result<T, E>`

È un tipo che contiene:
- un risultato di tipo `T` se tutto è andato bene, e in tal caso si può costruire con `Ok(valore di tipo T)`
- o un errore di tipo `E` se qualcosa è andato storto, e in tal caso si può costruire con `Err(valore di tipo E)`

Ad esempio:

```rust
// questa funzione ritorna o un numero intero (i32),
// o se qualcosa è andato storto una stringa come errore
fn leggi_numero_da_casella_di_testo(testo: &str) -> Result<i32, String> {
    if testo.is_empty() {
        // costruiamo un Result contenente un errore e lo ritorniamo normalmente
        return Err("Una stringa vuota non puo' essere convertita in numero".to_string())
    }

    let mut numero_convertito = 0;
    for carattere in testo.chars() {
        if !carattere.is_digit(10) {
            // costruiamo un Result contenente un errore e lo ritorniamo normalmente
            return Err(format!("Il carattere non e' una cifra: '{carattere}'"))
        }

        // semplice conversione del testo in numero leggendo una cifra alla volta 
        numero_convertito *= 10;
        numero_convertito += carattere as i32 - '0' as i32;
    }

    // la conversione ha avuto successo
    return Ok(numero_convertito)
}

println!("Numero senza spazio: {:?}", leggi_numero_da_casella_di_testo("1234")); // Ok
println!("Numero con spazio: {:?}", leggi_numero_da_casella_di_testo("1234 ")); // Err
println!("Stringa vuota: {:?}", leggi_numero_da_casella_di_testo("")); // Err
```

## Come gestire gli errori

Per estrarre il valore che ci serve da un `Result` o da un `Option` abbiamo varie opzioni disponibili.

### `.unwrap()`

`.unwrap()` è l'opzione peggiore, e non andrebbe **mai** usata. In pratica estrae il risultato se esiste, e altrimenti fa crashare il programma!

### `if let`

Il costrutto `if let` serve per controllare il contenuto e gestire il caso di successo:

```rust
#fn leggi_numero_da_casella_di_testo(testo: &str) -> Result<i32, String> {
#    if testo.is_empty() {
#        // costruiamo un Result contenente un errore e lo ritorniamo normalmente
#        return Err("Una stringa vuota non puo' essere convertita in numero".to_string())
#    }
#
#    let mut numero_convertito = 0;
#    for carattere in testo.chars() {
#        if !carattere.is_digit(10) {
#            // costruiamo un Result contenente un errore e lo ritorniamo normalmente
#            return Err(format!("Il carattere non e' una cifra: '{carattere}'"))
#        }
#
#        // semplice conversione del testo in numero leggendo una cifra alla volta 
#        numero_convertito *= 10;
#        numero_convertito += carattere as i32 - '0' as i32;
#    }
#
#    // la conversione ha avuto successo
#    return Ok(numero_convertito)
#}

// qui il numero viene convertito correttamente
if let Ok(numero_convertito) = leggi_numero_da_casella_di_testo("1234") {
    println!("Bravo, hai inserito il numero {numero_convertito}");
} else {
    println!("Oh no...");
}

// qui verrà scritto "Il vettore non ha un quinto elemento!"
let vettore = vec![1,7,9];
if let Some(elemento_del_vettore) = vettore.get(4) {
    println!("Il quinto elemento del vettore e' {elemento_del_vettore}");
} else {
    println!("Il vettore non ha un quinto elemento!");
}
```

### `match`

Il costrutto `match` è più potente di `if let` ed è in particolare utile quando vogliamo spacchettare sia risultato che errore:

```rust
#fn leggi_numero_da_casella_di_testo(testo: &str) -> Result<i32, String> {
#    if testo.is_empty() {
#        // costruiamo un Result contenente un errore e lo ritorniamo normalmente
#        return Err("Una stringa vuota non puo' essere convertita in numero".to_string())
#    }
#
#    let mut numero_convertito = 0;
#    for carattere in testo.chars() {
#        if !carattere.is_digit(10) {
#            // costruiamo un Result contenente un errore e lo ritorniamo normalmente
#            return Err(format!("Il carattere non e' una cifra: '{carattere}'"))
#        }
#
#        // semplice conversione del testo in numero leggendo una cifra alla volta 
#        numero_convertito *= 10;
#        numero_convertito += carattere as i32 - '0' as i32;
#    }
#
#    // la conversione ha avuto successo
#    return Ok(numero_convertito)
#}

// scrive "Errore: Il carattere non e' una cifra: 'a'"
match leggi_numero_da_casella_di_testo("abc") {
    Ok(numero_convertito) => println!("Bravo, hai inserito il numero {numero_convertito}"),
    Err(errore) => println!("Errore: {errore}"),
}
```

### L'operatore `?`

Quando ci sono troppe cose che possono ritornare `Option` o `Result`, l'operatore `?` può aiutarci a propagare l'errore da una funzione a quella chiamante in modo pratico.

Scrivere `let risultato_ok = oggetto?;` equivale a scrivere
```rust,ignore
let risultato_ok = match oggetto {
    Ok(res) => res, // res viene assegnato alla variabile risultato_ok
    Err(errore) => return errore, // l'errore viene ritornato dalla funzione corrente
};
```

## Esercizi

- Scrivere un programma che legge due numeri dalla console (ovvero da `stdin`) e scrive la somma in output, assicurandosi di gestire tutti gli errori accuratamente. Nota: non usare la funzione `leggi_numero_da_casella_di_testo` descritta sopra, ma usa invece [String::parse()](https://doc.rust-lang.org/std/string/struct.String.html#method.parse).
- Sperimenta con le varie funzioni utili per le [Option](https://doc.rust-lang.org/std/option/enum.Option.html) e i [Result](https://doc.rust-lang.org/std/result/enum.Result.html) descritte nella documentazione.