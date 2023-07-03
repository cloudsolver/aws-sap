Amazon Machine Image is a regional image that instantiates an [[EC2]] instance.

## AMI Details

#Question What are AMIs used for?
Answer:
Amazon Machine Images are a customization of EC2 instances.
- Add your software, config, OS, monitoring etc.
- #UseCase pre-configured, faster initialization.
- AMIs are built for specific [[Regions]]. You can copy AMI across Regions.

## AMI Image Builder

#Question What is AMI Image Builder used for and how is compliance supported?
See: [AMI Image Builder UG](https://docs.aws.amazon.com/imagebuilder/latest/userguide/how-image-builder-works.html)
Answer: 
- AWS Task Orchestrator and Executor (AWSTOE) is a standalone application used by AWI Image Builder.
- Helps orchestrate complex workflows
- Modify system configurations, and 
- Test your systems with YAML-based script components.
- EC2 Image Builder uses Amazon [[Inspector]] to assess exposure, vulnerabilities, and deviations from best practices and compliance standards.

### Use Cases
#UseCase for creating an AMI
1. Start an [[EC2]] instance
2. customize it, 
3. stop the instance, 
4. build an AMI - 
5. this will create [[EBS]] snapshots
6. Launch instance.

![AMI Lifecycle](https://docs.aws.amazon.com/images/AWSEC2/latest/UserGuide/images/ami_lifecycle.png)

#UseCase  for sharing AMI encrypted via KMS*
1. Source Account uses [[KMS]] for [[Encryption Concepts]] of the AMI in the same region.
2. Source Account updates Launch Permission for the Target Account
3. Source Account gives permissions to use KMS key to target account
4. Target Account can decrypt the AMI and launch an instance. 
![[kms_cross_account_key.png]]
Fig. AMI sharing across Accounts

#Question How to create an AMI from an EC2 instance without shutting down the instance?
See: [EC2 UG](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html)
Answer: Use the `no reboot` option to take a snapshot.
![[AMI EBS Snapshots No Reboot.png]]
Fig. No Reboot Snapshots are supported

---

#Question How can you prevent unapproved AMIs from being launched?
See:
Answer: By tagging AMIs, then using IAM Policies to look for tags before launching. "Condition" and "StringEquals"

---
#Question  You can use an AMI in N.Virginia [Region](Region.md) us-east-1 to launch an [[EC2]] instance in any AWS [[Region]]. True or False? 
Answer: False. You must copy the AMI over to the new Region and AZ.


**References**

1. https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html