# Comandi base

## Sudo 

Incontreremo spesso il comando `sudo`, sempre seguito da altro. Questo comando permette di eseguire un comando con permessi di amministratore, e sarà necessario usarlo per fare operazioni più avanzate sul sistema.

Se abbiamo una password impostata sul nostro utente allora la prima volta che usiamo `sudo` ci verrà richiesta, poi per un certo tempo potremo utilizzarlo senza doverla reinserire.

## Manuale

Nella maggior parte dei sistemi Unix è disponibile un manuale integrato, che documenta l'utilizzo di tutti i comandi presenti nel sistema. Possiamo accederci usando `man`

```bash
man <manual_page>
```

La pagina di manuale può essere un qualunque comando di cui vogliamo, `man` incluso

```bash
man man
```

Ci mostrerà il manuale che ci spiega come usare il manuale.

## Spegnimento e riavvio

Possiamo spegnere il nostro server con il comando `poweroff`

```bash
sudo poweroff
```

Questo è in realtà una scorciatoia per il più complesso comando `shutdown`. Per ottenere lo stesso risultato dovremmo scrivere

```bash
sudo shutdown -h now
```

Possiamo riavviare il sistema utilizzando invece

```bash
sudo restart
```

## Aggiornamento e installazione pacchetti

Su Ubuntu, e più in generale sui sistemi basati su Debian, il gestore dei pacchetti è `apt`. Esistono dei repository che contengono un elenco di tutti i pacchetti disponibili e le loro versioni. 

Possiamo controllare il contenuto dei repository usando il comando l'opzione `update`

```bash
sudo apt update
```

Nel caso `apt` trovi degli aggiornamenti possiamo installarli eseguendo un `upgrade`

```bash
sudo apt upgrade
```

Ci verrà poi chiesta conferma, a cui possiamo rispondere digitando `y` e poi premendo invio.

In modo simile, possiamo usare l'opzione `install` seguita dal nome del pacchetto che vogliamo installare per installarlo

```bash
sudo apt install <package>
```

## Orientarsi nel file system

Il comando `ls` ci permette di elencare tutti i file presenti in una cartella

```bash
ls
```

Ci mostrerà tutti i file e le cartelle presenti nella cartella in cui ci troviamo. Possiamo spostarci nelle cartelle usando il comando `cd`

```bash
cd <folder_path>
```

Al comando `cd` possiamo sia passare il semplice nome della cartella, ma possiamo anche accedere a sottocartelle separando con `/`. Se non viene passato nessun percorso allora ci porterà nella cartella del nostro utente. Alternativamente per andare nella cartella del proprio utente

```bash
cd /home/<user>
```

Una scorciatoia per indicare la cartella dell'utente corrente è il carattere `~`, che possiamo usare in tutti i comandi e non solo in `cd`

```bash
cd ~
```

Altre scorciatoie utili sono `.` che indica la cartella corrente e `..` che indica la cartella superiore a quella corrente.

Possiamo elencare i file in una cartella utilizzando 

```bash
ls <folder_path>
```

Il comando `ls` ha molte opzioni utili: per esempio aggiungendo `-a` ci mostrerà anche i file nascosti

```bash
ls -a <folder_path>
```

Per ricevere più informazioni sui file possiamo usare l'opzione `-l`, ed abbinarla a `-h` per trasformare le unità in modo che siano più leggibili (`-h` indica human readable)

```bash
ls -l -h <folder_path>
```

## Aprire e modificare file

Una volta localizzato il file che ci interessa con `ls` e `cd` possiamo visualizzarne il contenuto con il comando `cat`

```bash
cat <file_path>
```

Nel percorso possiamo usare tutte le scorciatoie che abbiamo visto precedentemente.

Per modificare un file esistono diversi editor, i più popolari sono `vi`, `emacs` e `nano`. I primi due sono i più vecchi (1976!) ed avanzati, mentre l'ultimo è più recente ed intuitivo da utilizzare. Possiamo modificare un file con `nano` scrivendo

```bash
nano <file_path>
```

Si aprirà un'interfaccia dove possiamo muoverci e scrivere liberamente. Sono scritte in basso le scorciatoie per utilizzare il programma, in particolare per salvare e chiudere il file premiamo `ctrl+x` e poi invio.

Nel caso di file di sistema sarà necessario anteporre il comando `sudo` a `nano` per poter salvare le modifiche.

# Rete

## Informazioni sulla rete

Il modo più semplice per verificare se abbiamo accesso alla rete è utilizzando il comando `ping`, che serve a misurare il tempo che impiega uno specifico tipo di pacchetto (chiamato ICMP) a raggiungere un altro dispositivo nella rete e tornare indietro. Questo ci permette di capire se la comunicazione tra i due dispositivi funziona ed anche se questa è stabile.

```bash
ping <destination>
```

La destinazione può essere sia un nome di dominio (e.g. www.example.org) che un indirizzo IP (e.g. 127.0.0.1).

Per trovare l'indirizzo del nostro dispositivo (o macchina virtuale) nella rete possiamo usare il comando `ip`

```bash
ip addr
```

Nell'output di questo comando l'indirizzo IP sarà preceduto dalla scritta `inet`, e `inet6` per l'indirizzo IPv6. Sono presenti diverse informazioni per ogni interfaccia ma soprattutto più interfacce: in genere quella che ci interessa ha un nome simile a `enp0s1` o `eth0`. 
È sempre presente anche un'interfaccia di loopback, indicata con `lo` con (solitamente) indirizzo IP 127.0.0.1. Questo dispositivo è il modo con cui un dispositivo vede sé stesso.

Possiamo trovare le stesse informazioni in modo meglio organizzato con il comando `ifconfig`, che però non sempre è presente e potrebbe essere necessario installarlo.

```bash
ifconfig
```

A volte può servirci sapere l'indirizzo IP corrispondente ad un nome di dominio. Per ottenerlo dobbiamo fare una richiesta DNS, ed il modo più semplice è tramite il comando `nslookup`

```bash
nslookup <domain_name> [<dns_server>]
```

Se non viene specificato un server DNS tramite il suo indirizzo IP il comando utilizzerà il server predefinito di sistema (solitamente quello indicato dal nostro operatore).

Per ricevere informazioni più dettagliate su una specifica interrogazione DNS possiamo utilizzare il comando `dig`

```bash
dig [@<dns_server>] <domain_name>
```

## Scaricare file

Il modo più semplice per scaricare un file da internet è utilizzando il comando `wget`

```bash
wget <file_url>
```

Il file verrà salvato nella cartella corrente. invece possiamo stampare il contenuto del file a schermo utilizzando `curl`

```bash
curl <file_url>
```

In realtà questi comandi sarebbero molto simili nell'utilizzo, ed entrambi possono svolgere entrambe le funzioni date le opportune opzioni, però per semplicità li useremo in questo modo.

# Operatori

Su Bash, la shell di Linux, sono presenti degli operatori per manipolare l'output dei comandi.

## Pipe - `|`

L'operatore pipe, indicato con il carattere `|`, serve per reindirizzare l'output di un comando all'input di un altro comando. Pensiamo ad esempio di voler leggere un file molto lungo: possiamo utilizzare `cat` ma il testo finirà poi fuori dallo schermo. Possiamo quindi combinare `cat` al comando `less`, che permette di navigare un testo tramite le frecce

```bash
cat file | less
```

## Redirect - `>`

Possiamo reindirizzare l'output di un comando ad un file utilizzando l'operatore di redirect, indicato con il simbolo `>`. 

```bash
curl example.org > out.txt
```

Così facendo il contenuto del file presente nella pagina `example.org`  verrà scritto sul file `out.txt`. Se il file esiste già verrà sovrascritto, altrimenti verrà creato.

Se non vogliamo sovrascrivere ma piuttosto aggiungere alla fine del file possiamo invece utilizzare `>>`

```bash
cat part2.txt >> part1.txt
```

# Scorciatoie da tastiera

L'utilizzo di alcune combinazioni da tastiera ci può semplificare molto la vita utilizzando la linea di comando. 

## `Tab`

In assoluto di maggiore importanza c'è il tasto `Tab`, che viene utilizzato per l'auto completamento. Premendolo anche solo dopo aver scritto una piccola porzione di un comando o del nome di un file potrebbe completarne una parte significante. Quando non ci sono abbastanza informazioni per finire l'auto completamente premendolo due volte ci verranno elencate tutte le opzioni: basterà allora aggiungere solitamente un carattere per poter completare di nuovo con `Tab`.

## Gestire l'esecuzione di un programma

### Chiusura

A volte capita che un programma si blocchi, o che abbiamo sbagliato qualcosa e vogliamo interromperlo. Per farlo solitamente è sufficiente premere `Ctrl-C`. 

Nel caso questo non funzioni probabilmente il programma ha bloccato questa scorciatoia e ne ha una propria: è questo il caso per l'editor di testo `vi` (`Esc` poi `:`, scrivere `q!`, poi `Enter`), il comando `screen` (`Ctrl-A` poi `D`), e l'interprete del linguaggio Python (scrivere `exit()`, poi `Enter`). 

Per i programmi che svolgono operazioni sul sistema, come ad esempio `apt` o `systemctl` è meglio evitare di usare `Ctrl-C`, o si potrebbe lasciare il sistema in uno stato inconsistente, che può creare problemi.

### Interruzione

A volte può esserci utile interrompere solo temporaneamente l'esecuzione di un programma, magari perché dobbiamo controllare qualcos'altro. In questo caso possiamo premere `Ctrl-Z`, e ci troveremo di nuovo sulla linea di comando. Il programma non sarà però chiuso ma sospeso.

Per riprendere normalmente l'esecuzione ci basterà utilizzare il comando `fg`, che farà tornare di nuovo il programma visibile. Se invece vogliamo che questo continui a lavorare in background (ad esempio un download) possiamo invece utilizzare `bg`.

## Cronologia dei comandi

La shell di Linux tiene una cronologia dei comandi che eseguiamo. Per consultarla basta semplicemente premere i tasti freccia su e giù della tastiera, e potremo vedere in ordine i comandi che abbiamo eseguito di recente.

È possibile anche effettuare una ricerca nella cronologia dei comandi premendo `Ctrl-R`, e scrivendo una parte del comando che vogliamo trovare. Risulta molto utile soprattutto con comandi complessi di cui non sempre ci si ricorda tutte le opzioni.