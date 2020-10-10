# backup script

Dieses Skript dient dazu alle wichtigen Daten auf dem Rechner zu sichern und diese auf den NAS Server zu schieben.

## Aktuelle Sicherungen

* documents Verzeichnis
  * Beeinhaltet Allgemeines, Projektideen, wichtige Verträge und alte Daten wie etwa aus dem Studium.

## Beispiel Implementierung

```bash
# Beispiel Implementierung 
#!/bin/bash

timestamp () {
  date +"%y%m%d%H%M%S"
}

LOG_PATH="/var/log/rsync_backup/"
DOCUMENT_LOG="${LOG_PATH}$(timestamp)-documents.log"

if [ ! -d $LOG_PATH ]; then
  mkdir $LOG_PATH
fi

rsync -au ~/Dokumente/ /mnt/Daten/ --log-file=$DOCUMENT_LOG
```

## Crontab

```bash
$ su - root
$ crontab -e
0 */2 * * * /home/daniel/bin/save-data
```