#Question What checks does Trusted Advisor perform?
It is an #AWSService that provides recommendations to follow AWS Best Practices. #WellArchitected 
- Cost Optimization
- Performance
- Security
- Fault Tolerance
- Service Limits
![[Trusted Advisor Categories.png]]
Fig. Trusted Advisor Checks

In 2022, new Fault Tolerance checks were introduced that check for single-AZ architectures and recommend Multi-AZ to enable HA.

#Question How does Trusted Advisor a
Trusted Advisor publishes metrics about check results to [[CW | CloudWatch]]. Alarms from CloudWatch follow.

---

#Question What are the seven core checks supported by Developer and Basic plan?

1. [[S3]] Bucket permissions
2. MFA on root users
3. [[IAM]] - one IAM user minimum
4. [[EBS]] - public snapshots
5. [[RDS]] - public snapshots
6. Service Limits - AWS limits
7. [[SG | Security Groups]] -  specific ports unrestricted.


#Question What are the additional checks when you upgrade to Enterprise Support?

- Access to Support API.
- Ability to set [[CW]] Alarms when limits are reached.
- Full Checks available on the 5 categories.

---
