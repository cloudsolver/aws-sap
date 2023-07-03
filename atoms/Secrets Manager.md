### Summary of Secrets Manager
Centrally manage the lifecycle of secrets. #AWSService Primarily for RDS and API keys, DR and secrets compliance. Service offer compares to [[SSM Parameter Store]] with advanced parameters. #secure 

### Secrets Manager Details
- Force rotation of secrets every X days to support compliance 
- Automate generation of secrets of rotation *lambda*
- Integration with Amazon [[RDS]] #UseCase 
- Encryption with [[KMS]]
- Replicate secrets across regions to support [[DR]] #UseCase 
- Read replica secret can be promoted to a standalone secret
- Deleting a Secret causes a 30 day wait period to allow time for cancelling the deletion if required. 

![[Credentials for Services.png|512]]
Fig. Options for Secrets Manager

---

### HA for Secrets

#Question How is an HA for secrets accomplished?
Alternating Users Rotation: Use two secrets - one for the user, the other for the admin. Alternating users rotation is a rotation strategy where Secrets Manager clones the user and then alternates which user's credentials are updated. This strategy is a good choice if you need high availability for your secret, because one of the alternating users has current credentials to the database while the other one is being updated. 

See: 
- [Alternating Users Rotation](https://docs.aws.amazon.com/secretsmanager/latest/userguide/tutorials_rotation-alternating.html)

---

#Question  How does [[CloudFormation]] leverage Secrets Manager?
See:
Answer: `ManageMasterUserPassword: true` - creates a password in SecretsManager and can output an `Arn`. 
![[SecretsManager CloudFormation.png]]
Fig. CloudFormation 
#Q How are multi-region keys supported for DR of Databases ?
See:
Answer: Read-replicas in another region are created and can be promoted in [[DR]] situations.
![[SecretsManager Cross Region Replica.png]]
Fig. Secrets Manager cross region.

---
> **References for Secrets Manager**
> 1. https://aws.amazon.com/secrets-manager/faqs/ 
> 
 
*Created on 2023-03-20 09:30*