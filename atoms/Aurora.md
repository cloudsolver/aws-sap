Aurora is a Cloud Optimized RDS. It is HA out of the box with read scaling and offers global reads, and serverless. The underlying storage volume automatically grows. #AWSService 

## About


#Question How does Aurora support HA?

The Aurora Cluster consists of a primary instance and up to 15 Replicas. The replicas support reader endpoints; however, when the primary fails, any read replica can be automatically promoted to be the primary. The underlying storage architecture spans AZs within the region and is fault-tolerant by design.  

Writer, Reader, and Custom endpoints provide flexibility, scale, and high availability.
- 6 copies of your data across 3 AZs.
- Storage striped across 100s of volumes.
- Up to 15 read-only replicas in different AZs and Regions (with supported database).
- Reader Endpoint can auto-scale by adding additional replicas to the service.
- Writer Endpoint points to the primary server.
- Custom Endpoints can point to a cluster of more powerful replicas e.g. for analytical queries. You would typically define various endpoints for different read workloads.
- Underlying shared volume spans Writer and Reader Endpoints - auto expands from 10GB to 128TB.
- Automated patching with zero downtime. Advanced monitoring.
- Backtrack: restore data at any point in time without using backups.
- You can create a stored procedure or native function that invokes a [[Lambda]]. #UseCase User Registered (new row in user column).
- 
### Serverless
- Aurora Serverless has a pay-as-you-go model
### Multi-Master
- Every node does Read-Write to enable immediate failover.
### Global
* Read Replicas 
	* This set up is to enable DR by creating a read-replica in another region.
* Global Database
	* 1 Primary Region (Read and Write).
	* Up to 5 secondary Regions (Read-Only).
	* Replication lag is 1 second!
	* Promoting another region : [[RTO]] < 60 seconds.
### Machine Learning
-  Amazon [[SageMaker]] and Amazon [[Comprehend]]
- Fraud detection, ads targeting, sentiment analysis, product recommendations. #UseCase 

### Quiz
#Q A company runs a business-critical application in the us-east-1. The application hosts a large 2TB Aurora DB. [[DR]] to us-west-2 must be designed to have an RTO of 10 minutes and an RPO of 1 minute.
1. Create a multi-region Aurora MySQL DB cluster in us-east-1 and us-west-2. Use Route53 health check to monitor us-east-1 and failover to us-west-2 upon failure.
2. Create a cross-Region Aurora MySQL read replica in us-west-2. Configure the EventBridge rule that invokes a Lambda function that promotes the read replica in us-west-2 when failure is detected.
3. Recreate the db as an Aurora global db with the primary DB cluster in us-east-1 and a secondary DB cluster in us-west-2. Use the EventBridge rule that invokes the Lambda function to promote the DB cluster in us-west-2 when failure is detected.
4. Recreate the database as an Aurora multi-master cluster across the us-east-1 and us-west-2 regions with multiple writers to allow read/write capabilities from all database instances.
Answer: To plan for a Disaster - we do not need to have an active-active with a multi-master. Neither can we depend on a read replica and hope that is synchronized up to the minute. Only reasonable option is to recreate the db as a global db.

#Q What should be done to separate read requests from write requests in a multi-AZ Aurora deployment?
1. Create a second database and link to the primary.
2. Update the application to read from the replica.
3. Create a read replica and modify the application to use the appropriate endpoint.
4. Enable read-through caching on the database.
Answer: Aurora replicas are independent endpoints in an Aurora DB cluster, best used for scaling read operations and increasing availability. Up to 15 replicas can be distributed across AZ. There are already replicas in a multi-AZ deployment, so there is no need to create a read replica per se. Update the application to connect to the reader endpoint for `SELECT` statements. There is one underlying logical volume across writers and readers.

#Question How do you disable Aurora Automatic DB backups?
Answer: There is no way to prevent automated backups.

## References

1. https://aws.amazon.com/rds/aurora/