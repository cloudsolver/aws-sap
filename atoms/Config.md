#Question What is AWS Config used for?
It is an #AWSService that acts as a configuration auditor.

Assess, audit, and evaluate the configuration of your resource. 
Does not prevent policy violations - only detects, audits, notifies, and remediates.
For example,
- Is there unrestricted SSH access to my security groups?
- Do my buckets have any public access?
- How has my ALB configuration changed over time?


### Config Details
- Use the AWS Management Console, API, or CLI to obtain details of what a resource’s configuration looked like at any point in the past. It is a per-Region service.
- AWS Config will also automatically deliver a configuration history file to the Amazon Simple Storage Service (S3) bucket you specify.

#Question How can tags be standardized?
Set up the `require-tags` managed rule in AWS Config

> **Config Rules**
	Specify configuration rules and be notified when configuration changes don't meet the rules.
	Implement Policies in the Config Rules engine to implement the practice.

**Config Notification Solution**
AWS Config can send a non-compliance event to [[EventBridge]] which can invoke a [[Lambda]] for remediation. Notifications can be sent via [[SNS]].
*Avoid*: AWS Batch (overkill)
*Note*: AWS Config can only use [[SSM]] Automation documents as remediation actions.

### Config Remediation

#Question How are config findings remediated?
You can configure remediations to be automated.
Remediation Architecture
![[config_trigger_auto-remediation_context.png]]
Fig. Auto-Remediation

Create a custom [[SSM Parameter Store]] Document that triggers a Lambda function which takes the action.
![[config_eventbridge_trigger_context.png]]
Fig. EventBridge triggers Lamba *custom remediation*

### AWS Config Aggregator

#Question How to support multiple accounts?

- Config now supports organization-wide compliance view.
- Aggregate from multi-account multi-region out of the box. Integrates with AWS [[Organizations]]
- You can create a Config Aggregator in the Management Org - that way it won't be required to set up permissions

![[Config Aggregator.png]]
Fig. AWS Config Aggregator

> 
> **References for Config**
1.  https://aws.amazon.com/config/features/
2. https://docs.aws.amazon.com/pdfs/config/latest/developerguide/config-dg.pdf
3. Multi-region, multi-account config: https://youtu.be/5m8ljOghcWM
4. https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html

---
*Created on 2023-03-15 23:03*