# Tool
Per iniziare, rustup è difficile che lo utilizzeremo, perché la versione del compilatore è già abbastanza recente se lo avete installato nello scorso anno.
per i più avanzati è possibile installare un compilatore "nightly", con parecchie funzionalità in più, ma non ancora stabilizzate. Inoltre è possibile impostare override per alcuni progetti con particolari versioni del compilatore...

Invece `Cargo` sarà il nostro migliore amico, lo useremo tantissimo, serve per gestire le dipendenze di un progetto, compilare i progetti, eseguire test, installare eseguibili...
Partiamo dalle basi, con un terminale navigate dove volete creare un progetto di test, ed eseguite `cargo new lezione-1`, verrà creata una cartella con tutto l'occorrente per poter iniziare. Apritela con l'ide e avrete un progetto già funzionante.
Se eseguiamo cargo run in un qualunque punto all'interno del progetto dovremmo vedere un Hello, world! comparire nel terminale.
Analizziamo la struttura del `crate` (potete vederlo come una sorta di progetto completo, d'ora in poi useremo questo termine)
- `Cargo.toml` file dove descriviamo le dipendenze del nostro crate e alcune flag di compilazione
- `Cargo.lock` generato in automatico da cargo, serve per tenere traccia delle dipendenze ma non lo useremo mai
- `src` Cartella dove è contenuto tutto il codice del nostro progetto
    - `main.rs` ecco il punto di entrata del nostro programma, da qui partirà la compilazione e l'esecuzione 
- `target` dove vengono compilati i nostri programmi (sempre in automatico), in caso di progetti grandi può diventare grandina (anche decine di GB), eseguite un `cargo clean` e verrà ripulita (a discapito dei tempi di compilazione successivi)

Ora possiamo guardare il file main.rs in dettaglio e iniziare a scrivere in rust!

# Studiamo Hello World!
```rust
fn main() {
    println!("Hello, world!");
}
```
Ah, forse è più semplice del previsto.
- `fn main()` è l'entry point (come il main in C/C++ o di tipo il 90% dei linguaggi)
- `{}` le grafe rappresentano un blocco di codice, e servono per raggruppare più istruzioni insieme
- le virgolette definiscono una `str` di rust, ne parleremo più in dettaglio più avanti, ma per ora basta vederle come stringhe semplici (e possono contenere unicode 😉)
- `println!()` funzione per la formattazione e la scrittura della stringa sul terminale, al momento prendetela per buona (anche il punto esclamativo è importante, ne parleremo in qualche lezione più avanzata, comunque sappiate che le normali funzioni di rust non hanno bisogno del punto esclamativo, ma println supporta più parametri e pertanto è speciale).
- `;` bisogna metterlo dopo ogni linea di codice (amanti di python, c'è un buon motivo per questo, fidatevi)

### Esercizi
- Provate a modificare il messaggio
- Provate a mettere 2 println e vedere che succede
- Esiste anche print!, cosa fa di diverso? Provate

# Altri cargo
Ho preso un progetto bello grosso e ho aggiunto i tempi di esecuzione approssimativi per rendere l'idea. 

### cargo run ( 63s primo build, 11.37s dal secondo in poi)
Compila ed esegue il crate

### cargo build ( 63s primo build, 11.37s dal secondo in poi)
Compila il crate senza eseguirlo

Aggiungerei che la prima compilazione è tendenzialmente più lenta rispetto a quelle successive, perché compila tutte le dipendenze, mentre nelle altre ricompila solo quello che cambia.

Questo è uno dei processi più lenti in rust, perché il compilatore deve fare molti controlli, generale molto codice, e applicare ottimizzazioni spinte. Questo accelera l'esecuzione (velocità quasi identiche a C/C++, quindi almeno un 100 di volte più veloce di python).


### cargo check ( 30s primo check, 0.28s dal secondo in poi)
Non compila, ma esegue tutti i controlli come se stesse compilando
La differenza è che è mooolto più veloce di una compilazione, molto utile

### cargo fmt (0.45s)
Prende tutti i file rs presenti nel nostro crate e sistema la formattazione, seguendo le linee guida di rust (aggiungendo spazi, andando a capo quando serve...)
Molto comodo, usatelo quando potete

### cargo clippy (0.45s)
Vi ricordate clippy nella suite office di microsoft? ![Plugin](chapter_2_imgs/Clippy.webp)
Ci guidava e ci consigliava su come creare dei documenti nel modo corretto. Allo stesso modo `cargo clippy` controlla il nostro codice con dei controlli aggiuntivi, dandoci dei consigli su come migliorare il nostro codice (e spesso ci azzecca). Se volete migliorare il vostro codice controllatelo ogni tanto.

### cargo test ( 35s primo test, 1s dal secondo in poi)
Compila i test presenti nel nostro crate, e controlla che vengano eseguiti correttamente (e in parallelo). Importantissimo per non fare dei "breaking changes" con refactor o simili.

### cargo add
Serve per aggiungere delle dipendenze al nostro progetto.
Ad esempio `cargo add rand` aggiunge "rand" al nostro progetto. Le dipendenze sono spesso scaricate da [crates.io](https://crates.io/)

# Errori
Con la vostra esperienza con rust, potrebbe sembrare che il compilatore sia piuttosto capriccioso e pedantico (e in alcuni casi lo è), ma cercate di vederlo come un alleato.
Infatti quasi sempre nel messaggio di errore vi dirà quale è il codice dell'errore, una rapida descrizione, delle indicazioni di solito dettagliate su cosa stia succedendo e a volte un indizio su come risolvere il problema (e come approfondire l'argomento).
Se del codice in safe rust compila, strutturalmente abbiamo la certezza che non ci saranno crash imprevisti (niente stack overflow o simili)
Un consiglio che posso dirvi è di vederla in questo modo: "sto impiegando più tempo a scrivere il codice perché rust mi obbliga a riflettere alle varie eccezioni che possono triggerarsi, ma una volta compilato ho la certezza matematica che questi problemi non accadranno mai (e quindi codice più facilmente mantenibile)"

# Commenti
Ovviamente come in tutti i linguaggi è possibile scrivere commenti, ma in rust non tutti i commenti sono uguali...
Per i più temerari lascio questo [link](https://doc.rust-lang.org/reference/comments.html) dove è possibile visionare le varie alternative, ma in generale useremo questi commenti:
```rust
// commento su una linea
/*
    commento multilinea
*/
/// commento per la documentazione su una linea, deve essere immediatamente sopra a una funzione/ struttura
# struct Hidden;
/**
    commento per la documentazione multilinea, anche lui deve essere immediatamente sopra a una funzione/ struttura
*/
# struct Hidden2;
```