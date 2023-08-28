Elastic File System #AWSService  - is a managed [[NFS]] - it can be mounted on many EC2 instances.
EFS works with [[EC2]] instances in multi-AZ.
Highly Available, scalable expensive (3x gp2) - pay per use.
#UseCase CMS, Web Serving, Data Sharing, Wordpress site.
Uses NFSv4.1 protocol, Security Group to control access to EFS.
Compatible with Linux and not Windows: standard file API and Portable Operating System Interface (POSIX).
Encryption at rest using [[KMS]]. #secure 
File-system will scale storage automatically.
Scale: 1000s of concurrent NFS clients, 10GB/second throughput. #performant 
Storage: Petabyte-scale NFS

### Performance Mode

#Question What step should the SysOps administrator perform to resolve the high PercentIOLimit metric on the file system?

Build a new EFS file system that is configured with Max I/O performance mode. Utilize AWS DataSync to migrate data to the newly created EFS file system. 

#Question What are the use cases for general purpose and max i/o file systems?
- General Purpose: latency-sensitive use cases, e.g. Web Server, CMS
- Max I/O: higher latency, high throughput, supports highly parallelized workloads. Exceptional use cases: media processing or higher latency.
- 
### Throughput Mode
- Bursting : 100MiBs, Elastic: scale based on workloads: #UseCase for unpredictable workloads.
- Provisioned/Enhanced: Set throughput regardless of storage size. 1 GiBs for 1 TB storage.



### Storage Class
- Standard: for frequently access files.
- IA: Infrequent Access. Lifecycle policy will trigger to move the file to a different tier. 90% savings
- One Zone and One Zone IA
	- Replaces data within a single AZ.
- Standard/Regional and Standard/Regional IA
	- Replicates data across multiple AZs.
- MAX 90 Days: age-off policy.

### Cost Optimization
- You can start saving on your storage costs by enabling EFS lifecycle management for your file system and choosing an age-off policy of 7,14, 30, 60, or 90 days.
- Amazon EFS offers Standard and One Zone storage classes for both frequently accessed and infrequently accessed files. Standard and One Zone storage classes are performance-optimized to deliver consistently low latencies. 
- The EFS Standard-IA and EFS One Zone-IA storage classes are cost-optimized for files accessed less frequently. Start saving on storage costs with EFS Lifecycle Management and an age-off policy (1, 7, 14, 30, 60, or 90 days). 
- Additionally, set a policy to automatically move accessed files from the cost-optimized infrequent access storage classes to the performance-optimized storage classes. With EFS Lifecycle Management, automatically move files between EFS Standard and EFS Standard-IA storage, or between EFS One Zone and EFS One Zone-IA storage, reducing costs up to 92%.

### On Prem
Amazon EC2 instances can access your file system across Availability Zones and Regions. By contrast, on-premises servers can access file systems using AWS Direct Connect or AWS Virtual Private Network (AWS VPN).

### Quirks, Limitations and Tradeoffs
- Amazon EFS does not support mounting from Amazon EC2 Windows instances.
-  File systems in the Max I/O mode can scale to higher levels of aggregate throughput and IOPS. The tradeoff is slightly higher latencies for file metadata operations.
- Using Provisioned Throughput mode, you can specify the throughput of your file system independent of the amount of data stored.


**References** 

[Amazon EFS Standard-Infrequent Access](https://aws.amazon.com/efs/features/infrequent-access/) 
[Amazon EFS One Zone-Infrequent Access](https://aws.amazon.com/efs/features/infrequent-access/)