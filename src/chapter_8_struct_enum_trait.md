# Structs
Che dire, ne abbiamo fatta di strada. ma di certo mancano ancora alcuni elementi fondamentali per una programmazione completa.
Infatti se devo salvare più dati tutti insieme? Ad esempio un membro di Mindshub è descrivibile con
nome, cognome, ambito di preferenze (elettronica, informatica, stampa 3d...) e tanti altri parametri.

Se cercassimo di tenere tutti questi dati in variabili separate in un attimo il codice diventerebbe illeggibile, ad esempio:
```rust
fn main(){
    let nome_persona_1 = "Alessio";
    let nome_persona_2 = "Fabio";
    let cognome_persona_1 = "Zeni";
    let cognome_persona_2 = "Giovanazzi";
    let preferenze_persona_1 = "Informatica, Stampa 3d";
    let preferenze_persona_2 = "Informatica, Elettronica";
    //... e tanta altra roba
}
```
Esiste un modo per fare un po' di ordine? Per raggruppare più variabili tutte insieme? E magari descrivere dei comportamenti complessi legati a questa struttura? Ma certo che si:
```rust
/// le strutture possiamo vederle come un insieme di variabili "attaccate insieme"
struct MembroMindshub{
    nome: String,
    cognome: String,
    preferenze: String,
}
fn main(){
    // in questo modo stiamo inizializzando una struttura, quindi <nome struttura>{campo: valore, ...}
    let persona_1 = MembroMindshub{
        nome: "Alessio".to_string(),
        cognome: "Zeni".to_string(),
        preferenze: "Informatica, Stampa 3d".to_string(),
    };
    let persona_2 = MembroMindshub{
        nome: "Fabio".to_string(),
        cognome: "Giovanazzi".to_string(),
        preferenze: "Informatica, Elettronica".to_string(),
    };
    //per accedere ai campi basta usare la sintassi <variabile>.<campo>
    println!("Io sono {} {}", persona_1.nome, persona_1.cognome);
    println!("Io sono {} {}", persona_2.nome, persona_2.cognome);
}
```
Direi che è molto più ordinato il codice, e abbiamo appena iniziato!!
Possiamo anche aggiungere metodi e funzioni associate, ad esempio:
```rust
struct MembroMindshub{
    nome: String,
    cognome: String,
    preferenze: String,
}
// i blocchi impl servono per definire delle funzioni/metodi per la struttura.
//Possiamo vederli come funzioni speciali che descrivono come si comporta la struttura
//quindi qui abbiamo impl <nome struttura>
impl MembroMindshub{
    // la funzione new è un tipico esempio di funzione associata. Prende dei valori e costruisce la struttura da quei valori
    fn new(nome: &str, cognome: &str, preferenze: &str)->Self{ //Self (ATTENZIONE CON LA S GRANDE) è una scorciatoia per definire la struttura che stiamo implementando
        //una normale inizializzazione come nel blocco precedente
        MembroMindshub{
            nome: nome.to_string(),
            cognome: cognome.to_string(),
            preferenze: preferenze.to_string(),
        }
    }
    //questo invece è un metodo, e in questo caso prende una reference immutabile alla struttura (e quindi non può modificarne i campi)
    //riflettendoci in questo caso ha senso. Quando una persona saluta non cambia il nome all'anagrafe...
    fn saluta(&self){
        //possiamo accedere sempre ai campi con <self>.<campo> (ATTENZIONE, s piccola) 
        println!("Ciao. Io sono {} {}", self.nome, self.cognome);
    }
}

fn main(){
    // inizializzazione con la funzione associata new (per indicarla ci vogliono i ::)
    let persona_1 = MembroMindshub::new("Alessio", "Zeni", "Informatica, Stampa 3d");
    let persona_2 = MembroMindshub::new("Fabio", "Giovanazzi", "Informatica, Elettronica");

    // facciamo salutare queste strutture, per farlo chiamiamo il metodo saluta (con il . )
    persona_1.saluta();
    persona_2.saluta();
}
```
Direi che la situazione si sta facendo interessante, abbiamo ridotto la funzione main da 10 righe disordinate a 4 righe ordinate!!!
Anche l'esperienza di chi utilizzerà la nostra libreria è mooolto migliore.

# Traits

Talvolta serve poter definire dei comportamenti condivisi per struct diverse. Ad esempio, ogni animale può fare il proprio verso:
```rust
trait Animale{
    /// Un qualsiasi oggetto che implementa `Animale` dovrà essere in grado
    /// di fare un verso, ovvero, dovrà implementare questa funzione
    fn fai_verso(&self);
}

struct Maiale {};
impl Animale for Maiale {
    fn fai_verso(&self){
        println!("Oink Oink");
    }
}

struct Mucca {};
impl Animale for Mucca {
    fn fai_verso(&self){
        println!("Mouuu");
    }
}

struct Coccodrillo {};
impl Animale for Coccodrillo {
    fn fai_verso(&self){
        // Il coccodrillo come fa?
    }
}
```

Usando i `trait` quindi si possono descrivere dei comportamenti condivisi, e poi fare in modo che varie `struct` li implementino e espongano appunto questi comportamenti condivisi. Questo è particolarmente utile in casi tipo:
- Voglio poter interagire con dispositivi di un certo genere indipendentemente dalla loro marca, e quindi creo un'interfaccia standard che mi permetta di interagire con i dispositivi in modo generico, *astraendo* i dettagli implementativi. Ad esempio, per un sensore di temperatura si creerebbe un `trait` con una funzione `leggi_temperatura`, e poi una `struct` diversa per ogni possibile sensore di temperatura che si usa.
- Voglio poter stampare i contenuti di una particolare `struct` per vederne il contenuto e aiutarmi a debuggare il programma. Per questo la libreria standard di Rust contiene il `trait Display` che viene implementato da varie `struct` della libreria standard, e che grazie a questa interfaccia comune possiamo stampare con `println!("{:?}", qualsiasi_cosa_che_implementi_display)`.
- Ho un videogioco con varie entità presenti nel mondo (ad es. animali, appunto), e voglio che il giocatore possa interagire con ogni entità in un modo comune (ad es. facendogli fare il verso).

La descrizione dei `trait` fatta in questa pagina è piuttosto introduttiva, e ci sono varie sintassi che non abbiamo trattato per implementare i casi qui sopra. Comunque sappiate che con Cyberorto avremo taaaante interfacce, e implementarle e descriverle sarà necessario, per cui imparerete facendo.

# Enums
Cosa succede se ho dei dati opzionali? Ad esempio un Mindshubber può essere interessato solo a un determinato set di interessi. Oppure se voglio enunciare dei colori:
```rust
enum Colori{
    Rosso,
    Verde,
    Blu
}

```