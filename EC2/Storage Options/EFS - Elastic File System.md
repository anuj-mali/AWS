#ec2 #storage
- managed NFS (network file system)
- can be mounted to multiple EC2 instances at a time
- works only with Linux EC2 instances in multiple AZ
- highly scalable, available, expensive, pay per use, no capacity planning
	![[Pasted image 20250214160938.png]]

## [[EBS Volume|EBS]] vs EFS

| **[[EBS Volume\|EBS]]**                  | **EFS**           |
| ---------------------------------------- | ----------------- |
| same AZ<br>requires snapshots to move AZ | spans multiple AZ |
## EFS Infrequent Access (EFS-IA)
- cost-optimized for files not accessed every day
- up to 92% lower costs compared to EFS Standard
- files automatically moved to EFS-IA based on the last access time
- Enable with a Lifecycle Policy
	![[Pasted image 20250214161425.png]]
