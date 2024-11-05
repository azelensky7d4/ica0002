# Backup SLA

## Coverage

We back up services that satisfy at least one of these criteria:
 - are primary source of truth for particular data
 - contain customer and/or client data
 - are not feasible (or very costly) to restore by other means

Services that are backed up:
 - MySQL
 - InfluxDB
 - Git repo


## Schedule

MySQL backups are created every 24 hours; it takes up to 1 minute to create and store the backup. The backups are made at 00:15 UTC.

InfluxDB backups are created every 24 hours; it takes up to 2 minutes to create and store the backup. The backups are made at 00:15 UTC.

All backups are started automatically by 03:00 UTC.

Backup RPO (recovery point objective) is:
 - 24 hours for MySQL
 - 24 hours for InfluxDB


## Storage

MySQL and InfluxDB backups are uploaded to the backup server.

Git repo is mirrored to the internal Git server.

Backup data from both servers will be synchronized to encrypted AWS S3 bucket in future (work in progress).


## Retention

MySQL backups are stored for 30 days; 30 versions (recovery points) are available to restore.

Influx backups are stored for 30 days; 30 versions are available to restore.

Git backups are stored for 180 days; 8 640 versions are available to restore.


## Usability checks

MySQL backups are verified every week by a specialized team.

InfluxDB backups are verified every week by an automatic script.

Git backups are verified every 30 minutes by an automatic script.


## Restore process

Service is recovered from the backup in case of an incident, and when service cannot be restored in any other way.

RTO (recovery time objective) is:
 - 30 minutes for MySQL
 - 30 minutes for InfluxDB
 - 15 minutes for Git

Detailed backup restore procedure is documented in the [backup_restore.md](./backup_restore.md).
