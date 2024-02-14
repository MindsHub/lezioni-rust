# Torneo
Abbiamo due versioni, scegliete quella che preferite che mentre voi lo scrivete noi creeremo il grader:
- La giungla di MindsHub

    c'è un ecosistema sotto l'orto. E c'è uno scontro tra ragni (carnivori), cimici asiatiche (erbivore), e rapanelli.
    Attraverso l'evoluzione di Cyberorto 27.5 riusciamo a comandare la voracità delle specie animali attraverso impulsi psionici in 5G. Il problema è che per generare l'impulso Abbiamo bisogno di 2 antenne diverse (un po' senzienti, e indipendenti). Il vostro compito è scrivere un "intelligenza artificiale" per gestire il sensore. Visto che non deve in nessun modo morire l'ecosistema, in caso che un antenna spinge una specie a mangiare l'ultimo esemplare dell'altra specie perde. Gli animali muoiono spontaneamente, e fertilizzano l'erba. Però a causa dell'inquinamento del 2050 crescono sempre meno rapanelli...
    ```rust
    ///deve ritornare quanta erba/ cimici la nostra specie deve mangiare. Se il numero è >= del numero disponibile si perde. Se si ritorna 0 si perde.
    fn gestisci_antenna(controlli_ragni: bool, numero_ragni: usize, numero_cimici: usize, numero_erba: usize)->usize{
        0
    }
    ```

- Il dilemma del tradimento

    Sono sparite le ultime patatine di MindsHub, e i possibili colpevoli sono 2, te e un tuo amico. Siete stati entrambi imprigionati "da voi sapete chi" nella stanza della parkside. Potete decidere se incolpare l'amico oppure no, e avrete come punizione i seguenti secondi di penalità:
        1. se entrambi vi incolpate a vicenda: 5s a testa
        2. se A incolpa B ma B non incolpa A: A 0s e B 10s
        3. se nessuno si incolpa avrete 1 s di penalità a testa.
    Visto che "voi sapete chi" non si fida di voi ripeterà la domanda ALMENO 1000 volte, e sommerà le penalita acquisite.
    L'obbiettivo è minimizzare la penalità.
    ```rust
    /// 
    fn incolpi_o_no(numero_caso_1: usize, numero_caso_2: usize, numero_caso_3: usize)->bool{
        false
    }
    ```