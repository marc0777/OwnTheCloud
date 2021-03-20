# Comandi base

## Sudo 

Incontreremo spesso il comando `sudo`, sempre seguito da altro. Questo comando permette di eseguire un comando con permessi di amministratore, e sarà necessario usarlo per fare operazioni più avanzate sul sistema.

Se abbiamo una password impostata sul nostro utente allora la prima volta che usiamo `sudo` ci verrà richiesta, poi per un certo tempo potremo utilizzarlo senza doverla reinserire.

## Manuale

Nella maggior parte dei sistemi Unix è disponibile un manuale integrato, che documenta l'utilizzo di tutti i comandi presenti nel sistema. Possiamo accederci usando `man`

```shell
man <manual_page>
```

La pagina di manuale può essere un qualunque comando di cui vogliamo, `man` incluso

```shell
man man
```

Ci mostrerà il manuale che ci spiega come usare il manuale.

## Spegnimento e riavvio

Possiamo spegnere il nostro server con il comando `poweroff`

```bash
sudo poweroff
```

Questo è in realtà una scorciatoia per il più complesso comando `shutdown`. Per ottenere lo stesso risultato dovremmo scrivere

```shell
sudo shutdown -h now
```

Possiamo riavviare il sistema utilizzando invece

```shell
sudo restart
```

## Aggiornamento e installazione pacchetti

Su Ubuntu, e più in generale sui sistemi basati su Debian, il gestore dei pacchetti è `apt`. Esistono dei repository che contengono un elenco di tutti i pacchetti disponibili e le loro versioni. 

Possiamo controllare il contenuto dei repository usando il comando l'opzione `update`

```shell
sudo apt update
```

Nel caso `apt` trovi degli aggiornamenti possiamo installarli eseguendo un `upgrade`

```shell
sudo apt upgrade
```

Ci verrà poi chiesta conferma, a cui possiamo rispondere digitando `y` e poi premendo invio.

In modo simile, possiamo usare l'opzione `install` seguita dal nome del pacchetto che vogliamo installare per installarlo

```shell
sudo apt install <package>
```

## Orientarsi nel file system

Il comando `ls` ci permette di elencare tutti i file presenti in una cartella

```shell
ls
```

Ci mostrerà tutti i file e le cartelle presenti nella cartella in cui ci troviamo. Possiamo spostarci nelle cartelle usando il comando `cd`

```shell
cd <folder_path>
```

Al comando `cd` possiamo sia passare il semplice nome della cartella, ma possiamo anche accedere a sottocartelle separando con `/`. Se non viene passato nessun percorso allora ci porterà nella cartella del nostro utente. Alternativamente per andare nella cartella del proprio utente

```shell
cd /home/<user>
```

Una scorciatoia per indicare la cartella dell'utente corrente è il carattere `~`, che possiamo usare in tutti i comandi e non solo in `cd`

```shell
cd ~
```

Altre scorciatoie utili sono `.` che indica la cartella corrente e `..` che indica la cartella superiore a quella corrente.

Possiamo elencare i file in una cartella utilizzando 

```shell
ls <folder_path>
```

Il comando `ls` ha molte opzioni utili: per esempio aggiungendo `-a` ci mostrerà anche i file nascosti

```shell
ls -a <folder_path>
```

Per ricevere più informazioni sui file possiamo usare l'opzione `-l`, ed abbinarla a `-h` per trasformare le unità in modo che siano più leggibili (`-h` indica human readable)

```shell
ls -l -h <folder_path>
```

## Aprire e modificare file

Una volta localizzato il file che ci interessa con `ls` e `cd` possiamo visualizzarne il contenuto con il comando `cat`

```shell
cat <file_path>
```

Nel percorso possiamo usare tutte le scorciatoie che abbiamo visto precedentemente.

Per modificare un file esistono diversi editor, i più popolari sono `vi`, `emacs` e `nano`. I primi due sono i più vecchi (1976!) ed avanzati, mentre l'ultimo è più recente ed intuitivo da utilizzare. Possiamo modificare un file con `nano` scrivendo

```shell
nano <file_path>
```

Si aprirà un'interfaccia dove possiamo muoverci e scrivere liberamente. Sono scritte in basso le scorciatoie per utilizzare il programma, in particolare per salvare e chiudere il file premiamo `ctrl+x` e poi invio.

Nel caso di file di sistema sarà necessario anteporre il comando `sudo` a `nano` per poter salvare le modifiche.

