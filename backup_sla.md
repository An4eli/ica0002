Backup services SLA


This SLA describes the backup approach for services in the infrastructure:
Web services (Nginx), App services (Agama), Database services (MySQL, InfluxDB),
DNS service (Bind9), Monitoring services (Prometheus, Grafana, Telegraf, Pinger, Bind9 exporter, MySQL exporter, Nginx exporters, Node exporters, Rsyslog), Additional services (Ansible, uWSGI)


Backup coverage
Backup service covers only database services, such as MySQL and InfluxDB, because they contain user provided information or some log information tath cannot be restored by any other means. Other services sush as Nginx, AGAMA, Grafana, Bind do not store any data produced by themselves so they can be re-created from scratch using Ansible service.


Backup RPO (recovery point objective)
Backup RPO for MySQL and InfluxDB would be 4 weeks (28 days). There will be two types of backups: full and incremential. Full backup contains all the backed up data and can be used to restore required data or service. It is done every Saturday at 00:40 (UTC). 
Incremental backup stores only the difference in the data between previous incremental backup and are done every day (except Saturday) at 00:40 (UTC).


Versioning and retention
Database services backups are retained for 4 weeks, so totally there 28 backups: 4 full ones and 24 incremental. Every Monday at 01:40 (UTC) backups thar are older than 28 days are deleted.


Usability
Usability of the last backup is checked every 7 days and tested in  virtual environment setup, simulating real infrastructure.


Restoration criteria
Backup should be restored if it is known that stored data was lost or deleted.


Backup RTO (recovery time objective)
Backup service should take not more than 3 hours to fully recover the data.  
