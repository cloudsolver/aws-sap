### Summary of WAF
Protect your web applications from common exploits. With AWS WAF, you can create security rules that control bot traffic and block common attack patterns such as SQL injection or cross-site scripting (XSS). #AWSService 

### WAF Details

![|384](https://docs.aws.amazon.com/images/whitepapers/latest/guidelines-for-implementing-aws-waf/images/waf-integrations.jpg)
Fig. WAF Integrations


- Layer 7 protection from common web exploits. #secure 
- Deployment Targets
	- [[ALB]]
	- [[API Gateway]]
	- [[CloudFront]]
	- [[AppSync]] GraphyQL API
	- [[Cognito]] User Pool
- Web ACLs are Regional (except CloudFront)
	- IP filtering
	- HTTP Headers
	- URI strings
	- Geo Match
	- Rate-based rules for DDOS protection
	- Works with [[Shield]], and [[Firewall Manager]] within the same UI too. 
- Get Global Accelerator to get a fixed IP address for an ALB - and attach WAF with Web ACLs
	- **An Application Load Balancer cannot be assigned an Elastic IP address** (static IP address). However, a Network Load Balancer can be assigned one Elastic IP address for each Availability Zone. 
#### Constraints
- Does not support TCP or Layer 4, e.g. [[NLB]]
---

## Resources

1. https://aws.amazon.com/waf/
2. [Guidelines for Implementation of WAF](https://docs.aws.amazon.com/whitepapers/latest/guidelines-for-implementing-aws-waf/guidelines-for-implementing-aws-waf.html)