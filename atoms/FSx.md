Amazon FSx is a managed File System service for popular clustered distributed file systems. Support FSx file systems: NetApp ONTAP, OpenZFS, Windows File Server with [[AD]] support, and [[Lustre]] for [[HPC]]. #AWSService 
###  FSx Systems
![](FSx_file_systems.png)

#### FSx for Windows 
- Supports SMB, NTFS, AD integration, ACLs, user-quotas, and Linux mountable on EC2. Supports Microsoft's [[DFS]] and multi-AZ. Data is backed up to S3.
- Use Multi-AZ for high-availability

#### FSx for Lustre

#Q What are the use cases for FSx for Lustre?
- [Lustre](Lustre.md) is used for [[ML]], [[HPC]], Video processing, Financial Modeling or other sub-latency, high-throughput, scalable workloads. Seamless integration with [[S3]] - read and write to it from FSx. VPN and [[DX]] are support for [[Hybrid Cloud Architecture]]
	- Scratch File System: Performance over durability and availability. High **Bursts** 6x faster. No replication - only one copy. Short-term storage.
	- Persistent File System: Multi-AZ, files are restored in minutes; useful for long-term storage.
	#Q How is FSx for Lustre integrated with S3?
	- Seamless integration with [[S3]] - when a bucket is connected to it - objects on S3 show up as files on FSx. 
	- File updates are written back to S3.
	#Q How scalable is FSx?
	An FSx for Lustre file system is capable of delivering hundreds of gibibytes (GiB) per second of throughput and millions of IOPS.

#### FSx for NetApp ONTAP
- FSx for NetApp ONTAP support iSCSI for block storage, NFS protocol for POSIX-compliant access, and SMB protocol for Windows-compatible access.
- NetApp ONTAP is compatible with Linux, Windows, MacOS, VMWare Cloud on AWS, [[Workspaces]], [[AppStream]], [[EC2]], [[ECS]], and [[EKS]].
	- Supports [[NAS]], [[NFS]], [[SMB]], [[iSCSI]] 
	- Snapshots, replication, low-cost, compression and data de-duplication.
	- Point-in-time instantaneous cloning. Useful for testing new workloads. 
#### FSx for OpenZFS
Managed OpenZFS - implementation of Open Zettabyte File System (ZFS)
	- [[NFS]] compatible, millions of IOPS.
	- Point-in-time instantaneous cloning just liske [[#NetApp ONTAP]]. 
	- Move workloads running on ZFS to AWS. #UseCase 
![](FSx_comparison_table.png)

## Resources

1.[When to choose FSx](https://aws.amazon.com/fsx/when-to-choose-fsx/)
