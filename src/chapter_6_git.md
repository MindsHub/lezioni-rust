# Git
Non c'entra niente con rust ma lo abbiamo inserito a tradimento per darvi comunque una spolveratina (quando si lavora in più persone sullo stesso codice è fondamentale).

Quindi, git è un "software per il controllo delle versioni", e in particolare controlla le varie versioni dei file, e aiuta a invertire cambiamenti dannosi, e ad unire versioni diverse degli stessi file.

Esempio:
stiamo tutti insieme e allegramente lavorando all'orto, magari io e Fabio stiamo entrambi lavorando sullo stesso Cargo.toml. Fabio aggiunge una dipendenza e io ne aggiungo un altra. Ognuno di noi salva le proprie modifiche, e dopo un po' decidiamo di unirle (ad esempio io ho lavorato ai motori e lui al planner). Però ci sono due versioni diverse dello stesso file, come devono essere unite?

# Vocabolario
### Commit
salvataggio dei file allo stato attuale, particella elementare di git
### Branch
serie di commit (e quindi di modifiche).
Ad esempio su una repository possono esserci più branch, ognuno per una funzionalità che qualcuno sta implementando. Quando è soddisfatto dei risultati fa un merge
### Merge
Unire due branch in uno solo, risolvendo eventuali conflitti (auspicabilmente in automatico).
### Repository
Un insieme di branch, commit ecc. Può essere in locale o remota
### Github
Non è la stessa cosa di git. Git è "il come" vengono gestite le repository. Github è una piattaforma dove si possono pubblicare e gestire repository.

# Comandi
- `git clone <repository>` hey, scaricami questa repository git e mettimela in questa cartella
- `git add . ` guarda cosa ho modificato in questa cartella, e tienilo pronto per la prossima commit
- `git commit -m "messaggio"` prendi tutte le modifiche registrate, e salvale in una commit (fatelo spesso)
- `git pull` se ci sono modifiche sull'origine di questa repo, scaricale e cerca di unire alle mie modifiche locali
- `git push` carica le mie commit locali sul branch remoto
- `git checkout <branch>` cambia branch
- `git branch <nome branch>` crea nuovo branch
