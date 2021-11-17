Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml


Restore MySQL data from the backup:
---

Make sure that dump was cerated
- ls -la /home/backup/mysql

Make sure backup was cretaed
- ssh an4eli@backup (from backup user)
- bash
- ls

Check mysql/agama.sql and later restore/agama.sql

- Download backup as a backup user:
duplicity --no-encryption restore rsync://An4eli@backup.boom.io//home/An4eli/ /home/backup/restore/

- To restore run this command as a root user:

    mysql agama < /home/backup/mysql/agama.sql




Restore InfluxBD data from the backup:
---

- Download backup as a backup user:

    duplicity --no-encryption restore rsync://An4eli@backup.boom.io//home/An4eli/ /home/backup/restore/


- To restore run this commands as a root user:
service telegraf stop
influx -execute 'DROP DATABASE telegraf'
influxd restore -portable -database telegraf /home/backup/restore
service telegraf start
