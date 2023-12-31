The key management system is an #AWSService that automates encryption key management. #secure 

### KMS Details
- [KMS Key Concepts](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html)
- Centrally manage [[Encryption Concepts|encryption]] keys and define policies. Multi-region keys are not supported.
- AWS KMS solution uses an _envelope encryption_ strategy with _AWS KMS keys_. 
- Supports Asymmetric and Symmetric keys.
- AWS rotates keys once every year.
- AWS Encryption SDK library should be used from within applications.
- Validate [[Digital Signatures]] and perform signing operations using asymmetric digital keys.
- Message authenticity and integrity with [[HMAC]] (Hash-based Message Authentication Codes)

#Question What is Envelope Encryption?
See: [[Envelope encryption]]

#### Key Deletion

#Question What happens when a key is scheduled for deletion?
- Not possible to delete directly. The default wait time is 30 days; it can be reduced to 7 days.
- No cryptographic operations are permitted during the `pending delete` state.
- No KMS key material is rotated during the `pending delete` state.

#Question What needs to be done to delete multi-region keys?
- You must first delete all replica keys to delete a primary key. If you must delete a primary key from a particular Region without deleting its replica keys, change the primary key to a replica key by updating the primary Region.

Remember that the deletion of keys, once it happens, is final. There is also no way to track where the key has been used.

#### Monitoring

#Question  How does**KMS itself achieve Monitoring** ?

 KMS is monitored by [[CW]], and its usage is tracked by [[CloudTrail]].

#Question What services does KMS Seamless Integrate?
- KMS seamlessly integrates with [[EBS]], [[S3]], [[RDS]], [[SSM Parameter Store]]

#### Types of KMS Keys

|                    | AWS Managed           | Customer Managed |
| ------------------ | --------------------- | ---------------- |
| AWS Generated      | AWS Owned and Managed (annual rotation) | Created in KMS, annual rotation must be enabled.   |
| Customer Generated | Imported to AWS (symmetric only)        | Manual rotation only                |

- The following script will create a base64 encoded file that is encrypted with kms key.
	`aws kms encrypt --key-id alias/mykey --plaintext fileb://SecretFile.txt --output text --query CiphertextBlob --region us-east-1 > SecretFileEncrypted.base64` 
	echo 'SecretFileEncrypted.base64' | base64 --decode > 'SecretFileEncrypted' // this will decode the encrypted file.
to decrypt give a decrypt command with the ciphertext and the blob - it will return a decrypted base64 encoded file back.
`aws kms decrypt --ciphertext-blob fileb://SecretFileEncrypted --output text --query Plaintext ExampleFileDecrypted.base64`


#### CMK Types

![[KMS CMK Type Comparison.png]]
Fig. KMS CMK Types

---

#Question  What are the request limits of KMS?
See: [Throttling KMS](https://docs.aws.amazon.com/kms/latest/developerguide/throttling.html)
**Answer**: It varies by region. Symmetric CMK varies between 5500, 10K, and 30K. RSA and ECC are at 500 and 300, respectively. Exponential backoff, or caching keys, can be used when dealing with `Throttling` issues resulting in `Error 400`.

---

### Cross-Region

Keys created by the service AWS KMS are only transmitted within the AWS Region in which they were made. They can be used only in the Region in which they were created.

Plaintext keys are never written to disk and only ever used in volatile memory of the HSMs for the time needed to perform your requested cryptographic operation. This is true regardless of whether you request AWS KMS to create keys on your behalf, import them into the service, or create them in an AWS [[CloudHSM]] cluster using the custom key store feature. Keys created by the service AWS KMS are never transmitted outside of the AWS Region in which they were created. They can be used in only the Region in which they were created.

### Multi-Region KMS Keys

**Multi-Region KMS keys let you encrypt data in one AWS Region and decrypt it in a different AWS Region.**

- Identical KMS keys in different AWS Regions that can be used interchangeably
	- Active-active applications that span multiple Regions
	- DR - Disaster Recovery
	- Global Data Management
	- Global Client Side Encryption
	- Global DynamoDB
	- Global Aurora
	- Distributed signing applications
	- Encrypt in one region and decrypt in another region
- No need to re-encrypt or make cross-Region API calls
- 
  Very select use cases e.g. Global Tables
![[kms_replica_key_cross_region_context.png|512]]
Fig. Keys are managed independently
Architecture for multi-region key replication
![[kms_multi_region_key_context.png|384]]
Fig. Keys are replicated to support global tables

DBA cannot read KMS encrypted columns as they will not have permission to the KMS key. Only an application will be able to decrypt and encrypt.

#### S3 Cross Region Replication with Multi-Region KMS Key
There is currently no benefit to using Multi-Region Key to save time encryption with a multi-region key because they are treated as independent keys by S3. For the same bucket backed up in another region, the objects will be decrypted and then re-encrypted with the same key material in the other region.

### Copy EBS Snapshot Cross Account
#UseCase EBS Snapshot Encryption
An [[EBS]] snapshot in Region A with Key 1 needs to be re-encrypted into Region B with Key 2. Key 1 cannot be used in Region B.
An encrypted snapshot can be moved across accounts (and regions).

**Steps**
1. Attach a KMS Key Policy to authorize cross-account
```
{
	"Sid":"Allow key use to target account/role",
	"Effect":"Allow",
	"Principal":{
	"AWS":"arn:aws:iam:TARGET-ACCOUNT-ID:role/ROLENAME"
	},
	"Action":["kms:Decrypt","kms:CreateGrant"],
	"Resource":"*",
	"Condition":{"StringEquals":{
		"kms:ViaService":"ec2.REGION.amazonaws.com",
		"kms:CallerAccount":"TARGET-ACCOUNT-ID"
	}}
}
```
2. Share the encrypted EBS snapshot across to the [target account](https://aws.amazon.com/blogs/aws/new-cross-account-copying-of-encrypted-ebs-snapshots/).
3. Create a copy of the snapshot, encrypt it with a CMK in the target account.
4. Create a volume from the snapshot.

### Key Policies

#Question What should you use to control access to your KMS CMKs?
Use KMS Key Policies. Not KMS IAM Policy.


- Default Key Policy
	- Created automatically
	- Complete access to the key to the creator of the key policy and account root user = Entire AWS account
	- it does not allow other IAM users or roles to use the key by default
- Custom KMS Key Policy
	- Define users and roles that can access the KMS key.
	- Define who can administer the key.
	- Useful for cross-account access to the key.

#### Resources

1. https://aws.amazon.com/kms/
2. https://aws.amazon.com/kms/features/#AWS_Service_Integration
3. [KMS Cryptographic Details](https://docs.aws.amazon.com/kms/latest/cryptographic-details/intro.html)
4. [KMS Best Practices Whitepaper](https://d0.awsstatic.com/whitepapers/aws-kms-best-practices.pdf)