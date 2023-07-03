## Summary
A managed Redis or Memcached service. #AWSService 

## ElastiCache Detail
- In-memory databases with high performance and low latency. #performant 
- Reduce load off of databases for read-intensive workloads. #OperationallyExcellent 
- Requires application code changes to use the cache.
### Solution Architecture
- Application will attempt to fetch data from the cache, if `cache miss` it will fetch from RDS, write to cache. #UseCase 
- Sticky session can be eliminated from ALB by using a distributed cache - ensuring stateless infrastructure.
### ElastiCache Technology

#Question Which underlying technologies does ElastiCache support?
Answer:
- [[Redis]]
- [[Memcached]]
 
### Security
- IAM Authentication for Redis
- IAM policies on ElastiCache are only used for AWS API-level security
![[CredentialsReport]]
#### Memcached
- Supports [[SASL]]-based authentication.
### Design Patterns
- Lazy Loading: Cache is loaded on demand.
- Write Through: Data is written to cache first, persistence occurs after.
- Session Store: Store temporary session data in cache with a TTL.
- 
## References

1.