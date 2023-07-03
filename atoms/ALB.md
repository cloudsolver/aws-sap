Application Load Balancer is an OSI Layer 7 fully managed [[ELB | Elastic Load Balancer]] that supports HTTP, HTTPS, and WebSocket.
See: [RTFM](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancers.html)

---

### IP Address Considerations

#Question How can you assign a fixed IP address to an ALB?

ALBs get a Fixed hostname, e.g., xyz.region.elb.amazonaws.com, but no fixed IP address. Remember you CANNOT assign an Elastic IP address directly to an ALB. **An Application Load Balancer cannot be assigned an Elastic IP address** (static IP address). However, a Network Load Balancer can be assigned one Elastic IP address for each Availability Zone. 
If you need a static IP address for your Application Load Balancer, it's a #BestPractice to **register the Application Load Balancer behind a Network Load Balancer**. The static IP address assigned to a Network Load Balancer doesn't change, providing a fixed entry point for your Application Load Balancer. 


| NLP                                                                                                                | Global Accelerator                                          |
| ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------- |
| Front an ALB with a Network Load Balancer. Assign the [[NLB]] an Elastic IP or use a BYOIP (Bring your own IP). | A global accelerator provides a fixed IP address to an ALB. |
|                                                                                                                    |                                                             |


#### ALB Security
#Question  How does ALB authenticate users?

 OIDC-compliant IdP. Must use HTTPS to set `authenticate-oidc` and `authenticate-cognito`. On authenticated, it can allow or deny.
![[ALB IdP Architecture.png]]
Fig. ALB IdP Architecture

#Question How do you protect an ALB from attacking Internet IPs?

Use Web ACL from [[WAF]] in the same region can be attached for protection. 

---

#### ALB Target Groups

See: [[ALB Target Groups]]


### Quiz

#Q An application is deployed with an Application Load Balancer and an Auto Scaling Group. Currently, you manually scale the [[ASG]] and would like to define a Scaling Policy to ensure the average number of connections to your EC2 instances is around 1000. Which Scaling Policy should you use?
(a) Simple Scaling Policy
(b) Step Scaling Policy
(c) Target Tracking Policy
(d) Scheduled Scaling Policy
Answer: Target Scaling Policy.

#Q A company must capture all client connection information from its Application Load Balancer every five minutes. This data will be used to analyze traffic patterns and troubleshoot the application. 
(a) Enable CloudTrail for the ALB
(b) Enable access logs on the ALB
(c) Install CloudWatch agent on the ALB
(d) Enable CloudWatch logs
Answer: This is a good question. The keyword is "client connections." You need to see access logs, so you need to enable that.