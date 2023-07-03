Elastic Block Storage is an #AWSService attached storage service for EC2; it stores up to 16 TiB and supplies up to 64,000 IOPS.


## Constraints
It is locked to an Availability Zone (AZ). The volume and instance must be in the same AZ.  To move the volume, it needs to be snapshot first. Two EBS volumes can be attached to an EC2 instance in the same AZ.

The root EBS volume is deleted upon termination. #UseCase You can preserve root volume when an instance is terminated but checking **preserve root volume on termination**.  

---
### EBS Encryption

 #Question  How can you ensure that all of the new EBS volumes restored from the unencrypted snapshots are automatically encrypted

Enable **EBS Encryption By Default** for the [[Region]].

![[EBS Region Encryption.png]]

- Data at rest is encrypted. Not all instance types support encryption.
- Data in flight between instance and volume is encrypted.
- All snapshots are encrypted.
- All volumes created from an encrypted snapshot are encrypted.
- Encryption and decryption are handled transparently with no intervention.
- KMS (AES-256).

#Question How do you encrypt an unencrypted EBS volume?

1. Create an EBS snapshot of the unencrypted volume.
2. Snapshot is unencrypted.
3. Copy the unencrypted snapshot with encryption enabled.
4. Copy of the snapshot is encrypted.
5. Create a new EBS volume from the encrypted copy of the snapshot.
6. Restore the encrypted snapshot copy to volume.




### EBS Multi-Attach
Amazon EBS Multi-Attach enables you to attach a single Provisioned IOPS SSD (`io1` or `io2`) volume to multiple instances that are in the same Availability Zone.
If it better to use [[EFS]] when required to span AZ as EBS is not a good solution for that. e.g. Web Servers that need to span AZs that use EBS for storage.



---

## EBS Snapshot

Dive into: [[EBS Snapshots]]

---

## EBS Volume Types

Dive into [[EBS Volume Types]]

---

## Quiz

#Q An EC2 instance can be resized if the root device for your instance is an EBS volume but not an instance store. True or false?
Answer: Resizing is impossible for the EC2 instance if the instance store is also the boot volume.

#Q A SysOps Administrator launched an EBS-backed On-Demand EC2 Instance to host a web application. However, the instance always terminates after going into the pending state.

This can happen if the EBS volume:
	- has reached it's limit
	- is encrypted and the key is not available to EC2

![[EBS Backed EC2 Instance lifecycle.png]]
Fig. EBS-backed [EC2] instances


#Q What [[RAID]] types does AWS  recommend for EBS?
(a) RAID 0
(b) RAID 1
(c) RAID 5
(d) RAID 6
Answer: Amazon EBS volumes are placed in a specific Availability Zone where they are automatically replicated to protect you from the failure of a single component. All EBS volume types offer durable snapshot capabilities and are designed for 99.999% availability. Given that, AWS only recommends RAID 0. [Details](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/raid-config.html) 

#Q You have launched an EC2 instance with two EBS volumes, the Root volume type and the other EBS volume type to store the data. A month later you are planning to terminate the EC2 instance. What's the default behavior that will happen to each EBS volume?
Answer: Upon termination, if there is no termination protection - the EBS volume that was the `root` type will be deleted.

#Q Non-root EBS volumes are preserved by default even when the EC2 instance is terminated. True or False?
Answer: True.