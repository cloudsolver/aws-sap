#Question What are Target Groups, and how are they associated with an ALB?

See: [UG](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html)

![[ALB Target Groups.png]]
Fig. Load Balancer

A target can belong to more than one target group.
- Target Groups
	- EC2 Instances (can be managed by an [[ASG]] - HTTP
	- EC2 tasks (managed by [[ECS]]) - HTTP
- [[Lambda]] functions - HTTP request is translated into JSON event.
- IP address - must be private IPs.
- ALB can route to multiple target groups.
- Health checks at the Target Group level.


---

#Question What is a listener and what are listener rules?

A listener is a process that checks for connection requests using the port and protocol you configure. The rules you define for a listener determine how the load balancer routes request to its registered targets.

**Required:** You must add at least one listener before an ALB can be used.


#Question How can client IP addresses be inspected by EC2 within Target Groups behind an ALB?

The underlying EC2 instances only see the ALB IP and do not see the client's IP directly.

ALB injects the following headers:
- `X-Forwarded-For` 
- `X-Forwarded-Port` 
- `X-Forewarded-Proto`

Routing rules can direct different target groups based on the following:
- path in URL
- hostname in URL
- query strings
- headers
