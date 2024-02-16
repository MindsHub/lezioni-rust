# Torneo: Il dilemma del tradimento

Sono sparite le ultime patatine di MindsHub, e i possibili colpevoli sono 2, te e un tuo amico. Siete stati entrambi imprigionati "da voi sapete chi" nella stanza della parkside. Potete decidere se incolpare l'amico oppure no, e avrete come punizione i seguenti secondi di penalità:

1. se entrambi vi incolpate a vicenda: 5s a testa
2. se A incolpa B ma B non incolpa A 0s e B 7s (e viceversa)
3. se nessuno si incolpa avrete 1 s di penalità a testa.

Visto che "voi sapete chi" non si fida di voi ripeterà la domanda ALMENO 1000 volte, e sommerà le penalita acquisite.
L'obbiettivo è minimizzare la penalità.

Seguite le seguenti istruzioni per fare una sottoposizione:
- Clonate la repo https://github.com/MindsHub/torneo-1
- Create il vostro crate con il comando: `cargo new --lib <nome>`, possibilmente per nome mettete il vostro nome o simili. L'importante è che sia unico e valido.
- eseguite questo comando: `cargo add -p <nome> --path ./template-torneo` (aggiunge il template come dipendenza del vostro crate)
- eseguite questo comando: `cargo add -p runner-torneo --path ./<nome>` (aggiunge la dipendenza a runner-torneo)
- registrate il vostro crate dentro il file `runner-torneo/main.rs` (troverete le indicazioni dentro il file)
- all'interno del vostro lib.rs dovrete implementare la seguente funzione (potete copiarlo da qua sotto):
    ```rust, ignore
    use template_torneo::LogTradimento;

    /// Scegliete quando incolpare il vostro avversario e quando no. Che vinca il migliore!!
    pub fn devo_incolparlo(_me: &LogTradimento, _other: &LogTradimento) -> bool {
        todo!()
    }
    ```
- Quando siete convinti del vostro risultato potete eseguire in locale il grader con cargo run.  Infine pushate sulla repo. (ripetere a piacere)

### Regole
Pls non modificate il runner. In ogni caso alla fine verrà testato con il grader originale (o migliorato), ma potreste ostacolare il testing agli altri.
allo stesso modo non fate crashare il vostro codice.

Ogni strumento/libreria/stratagemma è valido, potete aggiungere dipendenze o simili. Se il vostro crate fa qualcosa di lesivo verso la competizione viene semplicemente disattivato.
Ognuno può sottoporre fino ad un massimo di 5 crate (rivedibile se me lo argomentate bene).



<!---
- La giungla di MindsHub (per un altra volta)

    c'è un ecosistema sotto l'orto. E c'è uno scontro tra ragni (carnivori), cimici asiatiche (erbivore), e rapanelli.
    Attraverso l'evoluzione di Cyberorto 27.5 riusciamo a comandare la voracità delle specie animali attraverso impulsi psionici in 5G. Il problema è che per generare l'impulso Abbiamo bisogno di 2 antenne diverse (un po' senzienti, e indipendenti). Il vostro compito è scrivere un "intelligenza artificiale" per gestire il sensore. Visto che non deve in nessun modo morire l'ecosistema, in caso che un antenna spinge una specie a mangiare l'ultimo esemplare dell'altra specie perde. Gli animali muoiono spontaneamente, e fertilizzano l'erba. Però a causa dell'inquinamento del 2050 crescono sempre meno rapanelli...
    ```rust
    ///deve ritornare quanta erba/ cimici la nostra specie deve mangiare. Se il numero è >= del numero disponibile si perde. Se si ritorna 0 si perde.
    fn gestisci_antenna(controlli_ragni: bool, numero_ragni: usize, numero_cimici: usize, numero_erba: usize)->usize{
        0
    }
    ```

-->