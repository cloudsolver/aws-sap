RDS offers snapshot backup and restores from S3; Aurora offers database cloning that is faster and more cost-effective.
See [RDS Backup](https://aws.amazon.com/rds/features/backup/)

### Backups, PITR, and Retention

#Question What is the RPO and retention offered by AWS RDS?
- 5 Minutes RPO
- Data is backed up every 5 minutes. 
- Retention can be anywhere from 0-35 days.
- Daily full backups of the database. #resilient 

#Question How can you optimize the cost of data storage for databases that will not be used?
- Snapshot a database you don't want to use for long.
- Restore when needed.
- RDS will charge you for storage. #tip #CostOptimized

#Question How can an RDS database be moved to another account?

- Snapshots can be copied across Amazon accounts, regions and and within a region. 
- Restore a full database from a snapshot.
- 
#Question How do RDS backups compare to Aurora?
- Aurora Backups
	- Cannot be disabled as RDS can.
	- Manual DB Snapshots.
- Restoring RDS/Aurora backup or a snapshot to create a new DB.
- Restoring MySQL RDS database from S3 is simple.
- Restoring MySQL Aurora RDS requires Percona XtraBackup to restore to a new Aurora cluster.
- Aurora Database Cloning 
	- is an alternative to snapshot and restore
	- faster and more cost-effective. #CostOptimized 
	- useful to create a 'staging' database without impacting prod. #UseCase 

