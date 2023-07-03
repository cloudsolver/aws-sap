Service Catalog is an #AWSService that enables organizations to create and manage catalogs of approved IT services for AWS. These IT services can include everything from virtual machine images, servers, software, databases, and more to complete multi-tier application architectures.

#Question How should administrators standardize tags?
To allow administrators to manage tags on provisioned products easily, AWS Service Catalog provides a TagOption library. A TagOption is a key-value pair managed in AWS Service Catalog. 
See: [UG - Tag Options](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/tagoptions.html)
![[Service Catalog Tag Options Library.png]]
**Fig. Tag Options Library**

#Question How do you ensure that tags are consistently applied?

Tags must be consistently applied when your resources are created in AWS across all accounts. Use Service Catalog TagOptions for portfolios and products. Also, use [[CloudFormation]] Resource Tags property and finally, use [[Config]] to alert on resources that don't have tags.