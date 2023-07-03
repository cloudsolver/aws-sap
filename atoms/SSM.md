### Summary of Systems Manager
AWS Systems Manager, aka SSM, is the operations hub for your AWS applications and resources and a secure end-to-end management solution for hybrid cloud and multi-cloud environments that enable secure operations at scale. #AWSService 
See: [AWS SSM Home](https://aws.amazon.com/systems-manager/ )

### Systems Manager Capabilities

#Question What are the high-level capabilities of SSM?

![[ssm-aws-overview.png]]
Fig. SSM Capabilities


| Application             | Change             | Node                | Operations          |
| ----------------------- | ------------------ | ------------------- | ------------------- |
| [[SSM Parameter Store]] | Change Manager     | Compliance          | OpsCenter           |
| SSM App Config          | Automation         | Fleet               | Incident Management |
| SSM Application Manager | Change Calendar    | Inventory           | Explorer                    |
|                         | Maintenance Window | Session Manager     | CloudWatch Dashboard                    |
|                         |                    | [[SSM Run Command]] |                     |
|                         |                    | State Manager       |                     |
|                         |                    | [[SSM Patch Manager]]       |                     |
|                         |                    | Distributor         |                     |
|                         |                    | Hybrid Activations  |                     |
Table. SSM Capabilities

 
#### Quick Setup

#Question How can you easily set up SSM best practices for your organization?

SSM Quick Setup simplifies setting up services, including Systems Manager, by automating everyday or recommended tasks.

#### SSM Document

#Question What is an SSM Document?
SSM document defines the actions that the Systems Manager performs.
Includes Command documents.  State Manager, Run Command, and Automation runbooks utilize those.  Systems Manager Automation uses them as well.

#Question What are Automation Run Books?
 Automation: Run books are SSM docs that can take action on EC2 instances. e.g. snapshots of EBS. Integrates with [[Config]] - apply remediations that match findings.

### Patch Manager versus Run Command

#Question When should Run Command versus Patch Manager be used?

If you need to automate patching and compliance for your instances, you should use SSM Patch Manager. If you need to execute ad-hoc commands or scripts on your instances, you should use Run Command. #UseCase 

#Question How should `restricted-ssh` rule findings be invoked?

Use the `restricted-ssh` [AWS Config]-managed rule. Create a remediation action using an AWS System Manager **automation** document that revokes ingress rules that allow SSH traffic from the public.
The **compliance**  is a feature of System Manager that is used to scan your fleet of managed nodes for patch compliance and configuration inconsistencies. 
