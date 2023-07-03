AWS CloudFormation enables you to use a template file to create and delete a collection of resources as a single unit (a stack). #AWSService 

#UseCase for #CostOptimized dev environment.
- Delete templates at 5pm Friday and recreate at 8am Monday. This is also an excellent way to conserve the environment. #Sustainable #CostOptimized 
- Declarative programming is supported automatically.
- Leverage existing templates, and also diagrams are created!
- [[SAM]] sits on top of CF.
- [[CDK]] creates constructs that compile with type safety into the CloudFormation template.
- [[EB]] sits on top of CF.
---

#Question  What are the main components of CloudFormation?
See:
**Answer**:  Resources, Parameters, Mappings, Outputs, Conditionals, Metadata. Also, References and Functions as helpers.

| Component           | Description                                                                                 |
| ------------------- | ------------------------------------------------------------------------------------------- |
| Resources           | Mandatory declaration of resources.                                                         |
| Parameters          | Dynamic inputs to the template.                                                             |
| Mappings            | Static variables for your template.                                                         |
| Outputs             | References to what was created.                                                             |
| Conditionals        | Logic                                                                                       |
| Metadata            | Include arbitrary metadata in JSON or YAML                                                  |
| References (Helper) | Obtain the value of a specific attribute of a resource defined in the same or another stack |
| Functions (Helper)  | Manipulate values or perform calculations based on input parameters                                                                                            |

Table. CloudFormation

---

#Question How can CloudFormation ensure that the application within EC2 instances is ready to be used?

A CreationPolicy instructs CloudFormation to wait on an instance until CloudFormation receives the specified number of signals. This policy takes effect only when CloudFormation creates the model. 

[Blog](https://aws.amazon.com/blogs/devops/use-a-creationpolicy-to-wait-for-on-instance-configurations/)

---
#Question A CloudFormation has been How does CloudFormation update work?

You don't need to delete the CF stack. Update the existing stack with an upgraded instance type.

![[CloudFormation Update Process.png]]
Fig. Updates via CloudFormation

---


#Question  What are CF **Parameters**?
- Parameters allow you to pass values to your templates when creating or updating a stack. These values can include information such as instance sizes, key pair names, and database passwords. By using parameters, you can create more flexible and reusable templates that can be used for different environments or use cases.
`Fn::Ref` or simply `!Ref`. You don't know the value upfront.

#Question  Which section of a CloudFormation template does not allow for conditions?
- Parameters. This section is a declaration to be referenced later in the template.

#Question  What are **pseudo-parameters**?
Pseudo-parameters are predefined by CloudFormation and are available for use in all stacks. They provide information about the stack and its environment. Pseudo-parameters cannot be changed and their values are automatically populated by CloudFormation during stack creation or update. Examples of pseudo-parameters include `AWS::Region`, which returns the region in which the stack is being created or updated, and `AWS::StackName`, which returns the name of the stack.

---

#Q What are **Mappings** and how do you access them ?
Answer: This is hard-coded reference KV pairs. You know the values up front. Use `!FindInMap [MapName, FirstLevelKey, SecondLevelKey`

---

#Q What are **Outputs** ?
Cross stack references can be created so that experts in a company can create and maintain their portion of the cloud formation stacks. Outputs are a way to provide information about the resources that were created by the CloudFormation stack. They enable you to expose useful information about the resources that can be used by other stacks or applications.
`Fn::ImportValue` and `!ImportValue` are used to import the outputs into a cloud-formation thereby linking them.

---
#Q What are **Conditions**?
Logical controls that can execute based on logic.
![[CloudFormation Conditions.png]]

**Stacks**
- A single unit that includes all the resources build via the template.
- Nested Stacks are reused.
- Cross stacks use Output and are shared.
- Admin accounts create Stack Sets- these are across multiple accounts and regions.
**Change Sets**
While it does not tell us if it will succeed, it will give us a summary of proposed changes that can be generated before updating a running stack. e.g. renaming a database will delete the database (and the data) - good to know. `Fn::And`, 
![[cloudformation designer.png]]
Fig. CloudFormation Designer

I find it quite impractical. JSON is unusable, YAML is readable but it's super clunky.

#Question  How is CloudFormation rolled back handled with notifications?
Answer: CF needs [[SNS]] integration enabled. 
If CF fails, the stack will delete the resources, and the last known successful stack will be back.
![[CF-SNS Integration.png]]
Fig. Cloud Formation SNS Integration

#Question If the CF rollback process fails, what happens, and what needs to be done?
If the stack rollback fails, you must fix the issue manually then select `continue update rollback` to finish the rollback and revert to the previous state of the stack and the underlying resources.

---

#Q What are the limitations of CloudFormation?
Answer: It will not allow you to dynamically or programmatically generate resources. It is all declarative.  Almost all resource types are available, when they are not, you can use AWS Lambda Custom Resources.

---
#Q What is the quickest way to deploy a simple lambda function with CloudFormation?
Answer: Use the `ZipFile` parameter with inline code.
![[CF Lambda ZipFile.png]]
Fig. Lambda Function embedded with CloudFormation

---

#Question What does `cfn-init` do?
See: [CFN Helper Scripts](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-helper-scripts-reference.html)
**Answer**: Amazon's Linux AMIs have pre-installed Python helper scripts. 
- Fetch and parse metadata from CloudFormation
- Install packages
- Write files to disk
- Enable/disable and start/stop services

---

#Q A multi-region deployment partially failed with a stack instance from one region returning a status of "OUTDATED". Why?
Answer: Because it tried to create a duplicate global resource.

---