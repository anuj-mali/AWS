#ec2
- customization of an EC2 Instance
	- can add own software, configuration, OS ...
	- faster boot / config time
- build for specific region (can be copied to other regions)
- Can launch EC2 instances from:
	- A public AMI: AWS Provided
	- Own AMI: make and maintain ourselves
	- AWS Marketplace AMI: made (and sold) by someone else
## AMI Process (from EC2 Instance)
- Start and EC2 instance and customize
- stop the instance (*for data integrity*)
- Build an AMI (*this also creates EBS Snapshots*)
- launch other instances from AMI

## EC2 Image Builder
- used to automate the creation of VM or container images
- Automate the creation, maintain, validate and test EC2 AMIs
![[Pasted image 20250214160249.png]]

- can be run on a schedule
- Free service (only pay for underlying resources)