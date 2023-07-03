A low-cost option for archival and backup. Cost for object retrieval. Loading data directly into Amazon S3 Glacier is almost only possible with a lifecycle policy. 

--- 

#Question Is it possible to push data directly into Glacier?
**See**: [Glacier CLI](https://docs.aws.amazon.com/amazonglacier/latest/dev/uploading-an-archive-single-op-using-cli.html)
**Answer**: Yes. Pushing data to Glacier via [[Storage Gateway]] Tape Volumes and CLI is possible but not through the Console. 
- Archives are items stored up to 40TB
- Archives live in Glacier Vaults 
- [[SNS]] notifications can be set up in Vaults.

#Question Is it possible to directly upload to Glacier from Snowball edge devices?
It is not possible. You must upload to S3 and then use a lifecycle policy to move to Glacier.
See: [AWS Blog](https://aws.amazon.com/blogs/storage/using-aws-snowball-to-migrate-data-to-amazon-s3-glacier-for-long-term-storage/)

---

#Question What are Vault Policies?
See: [Resource Based Glacier Policy](https://docs.aws.amazon.com/amazonglacier/latest/dev/security_iam_resource-based-policy-examples.html)
**Answer**: 1. Access 2. Lock
![[assets/Glacier Vault Policy.png| 256]]
Fig. Glacier Vault Policies
- Vault Lock ID is provided; once you lock a vault - it can never be changed.
### Glacier Select
- 400% faster, 80% cheaper
- Retrieve less data by performing server-side filtering as opposed to client-side filtering.
## 3 Glacier Options
- Instant, flexible, and deep archive.

### Instant Retrieval
- Millisecond retrieval, minimum storage duration 90 days.
- Quarterly instantaneous retrieval. #UseCase 

### Flexible Retrieval
- Expedited (1-5 mins)
- Standard (3-5 hrs)
- Bulk (5-12 hrs): Free
- Minimum 90 days storage.
### Deep Archive
- Minimum 180 days, retrieval 12 hours

### Quiz
#Q A user is trying to create a vault in AWS Glacier. The user wants to enable notifications. In which of the below-mentioned options can the user allow the notifications from the AWS console?
(a) Glacier does not support the AWS console.
(b) Archival upload complete
(c) Vault upload job complete
(d) Vault Inventory Retrieval Job Complete
Answer: You can use the AWS Console to configure Vault Notifications (See this)[https://docs.aws.amazon.com/amazonglacier/latest/dev/configuring-notifications-console.html]. You cannot upload directly to Glacier - therefore options (b) and (c) are invalid. S3 Glacier defines events specifically related to job completion (`ArchiveRetrievalCompleted`, `InventoryRetrievalCompleted`).

