#Question What are ElastiCache Redis Features?
Answer:
- Multi-AZ with Auto-Failover #resilient 
- Read replicas scale reads #resilient #performant 
- Data durability using [[AOF]] persistence #resilient 
- Backup and restore.
- Supports sets and sorted sets.
- Gaming Leaderboards with guaranteed uniqueness and element ordering, and real time ranking through Redis Sorted Sets. #UseCase 

---

#Question What are the various modes of cluster scalability?
Answer: 


| #        | Online | Offline |
| -------- | ------ | ------- |
| Vertical | No       | Yes        |
| Horizontal| Yes  |  Yes      |

Online - can serve load.
Offline - cannot serve load.

---

#Question What are the common metrics to monitor?
Answer:
- `Evictions`:  Number of non-expired items.
- `CPUUtilization`: Host-level CPU utilization.
- `SwapUsage`: Should not exceed 50MB.  
- `CurrConnections`: Should not have high.
- `DatabaseMemoryUsagePercentage`: Amount of memory used
- `NetworkBytes/Packets In/Out`: Network activity
- `ReplicationBytes`: Volume of data replicated.
- `ReplicationLag`: Delay in replication.

---

#Question What is the maximum number of Read Replicas you can add in an ElastiCache Redis Cluster with Cluster-Mode Disabled?
Answer: Five.



## Security

- REDIS AUTH #secure 
- You can set a "password/token" when you create a Redis cluster.
- This is an extra level of security for your cache.
- Supports SSL in flight encryption. 
- Enable in-transit encryption. 