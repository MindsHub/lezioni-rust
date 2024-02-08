# Perchè rust?
Ma chi ce lo fa fare? Cosa ha di così comodo? Perché c'è tutto questo hype?
Ecco una lista dei punti a favore di rust:
### Typed
Si, i tipi sono fantastici, almeno sai cosa contiene quella variabile senza che il programma lo scopra a runtime crashando miseramente. (guardo voi js e python)
### Compilato
Ci mette qualche secondo a compilare il codice, ma dopo puoi eseguirlo ovunque anche senza runtime (coff coff Java e python), con performance simili a C/C++ (hanno ottimizzazioni simili, a volte rust è più veloce, a volte C è più veloce). Inoltre può essere eseguito su qualsiasi cosa possa eseguire istruzioni (vedi arduini e simili) senza doversi reinventare un compilatore (come invece ha fatto micropython).
### Compilatore rompi... scatole
A volte può essere pedante, ma esegue molti controlli, e quando compila abbiamo la certezza che non crashi per stupidi errori ( vedi typesafe). Potete vederlo come più tempo speso nel progettare buon codice che può portare a minor sforzo nel mantere il codice.
### Type safe
I linguaggi non type safe rischiano di avere puntatori che non puntano a niente, vulnerabilità nel codice pronte a creare problemi in seguito. Un programma scritto solo in safe rust ha la garanzia di non avere questi problemi. Ovviamente è possibile generare codice typesafe anche da linguaggi non typesafe, ma il programmatore deve sapere cosa sta facendo (e la storia ci insegna che spesso non è così).
### Moderno
La libreria standard include già funzionalità moderne per supportare multithreading, codice asincrono, tcp/ip stack, programmazione funzionale e molto altro.
Inoltre già nel codice permette di descrivere documentazione, test, test della documentazione... E già appena scaricato si ha cargo con molti strumenti utili per aumentare la produttività (vedi il capitolo strumenti).
### Ricco ecosistema
Essendo più moderno di c non si può pretendere l'ecosistema sia altrettanto ricco e navigato (rust è nato nel 2015, c nel 1983...). In ogni caso c'è un gran sforzo da parte della community per portare a librerie sempre più solide e ricche di funzionalità (136554 librerie su crates.io, con più di 54 miliardi di download).
Un esempio potrebbe essere Bevy, un game engine scritto completamente in rust che ha una nuova versione ogni 4/5 mesi circa.

# Ok, tutto bello. Ma gli svantaggi?
Ovviamente ci sono svantaggi, come in tutte le cose.
### Beginner friendly
Non è di certo un linguaggio semplice per iniziare, ci sono grandi sforzi della community per rendere l'entrata a nuovi sviluppatori il più semplice possibile (vedi https://doc.rust-lang.org/book/ ). Questo libro è un tentativo di semplificare l'entrata a chi ha già un po' di dimestichezza nella programmazione.
### Compilazione
Quando il progetto cresce, anche i tempi di compilazione aumentano. Ci sono dei trucchi per tentare di arginare il problema, ad esempio usare linker più performanti, compilare solo il codice di cui si ha veramente bisogno ecc. Ovviamente il compilatore cerca di compilare in parallelo quando possibile, e si crea una cache delle dipendenze, in modo da non ricompilarle ogni volta tutte le librerie, ma almeno una volta vanno compilate.
Ovviamente uno svantaggio legato alla cache è che potenzialmente si può usare molto spazio sul disco (in caso di progetti grandi anche svariati GB)
### Nuovo
L'ecosistema e il compilatore sono in rapida crescita, ma non ancora maturi al 100%. Pertanto non sempre accade quello che ci si aspetta. In qualche anno questo problema dovrebbe arginarsi da solo.
### Pillola rossa o pillola blu
UNA VOLTA ASSAGGIATO IL FRUTTO PROIBITO NON SI TORNA PIU' INDIETRO (scherzo ovviamente)
