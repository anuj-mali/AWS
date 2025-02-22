## EC2
- EC2 = Elastic Compute Cloud = IaaS
- Capabilities
	- Renting VM
	- Storing data ([[#EBS Volume|EBS]])
	- Distributing Load ([[Elastic Load Balancing & Auto Scaling Groups|ELB]])
	- Scaling services using [[Elastic Load Balancing & Auto Scaling Groups#Auto Scaling Group|ASG]]

### EC2 Sizing and Configuration
- OS: Linux, Windows, MacOS
- CPU
- RAM
- Storage
	- Network - [[#EFS - Elastic File System|EFS]], [[#EBS Volume|EBS]]
	- Hardware - [[#EC2 Instance Store|Instance Store]]
- Firewall rules: [[#Security Groups]]
- Bootstrap script: [[#EC2 User Data]]
- Network Card: speed of card, public IP address

#### EC2 User Data
- bootstrapping = launching commands when a machine starts
- used to automate boot tasks such as:
	- Install updates or software
	- download files
- Runs with root user

#### Instance Types

**Reference**: 
[EC2 Instance Types](https://aws.amazon.com/ec2/instance-types)
[Compare Instances](https://instances.vantage.sh)

###### Naming Convention
> m5.2xlarge
- m: instance class
- 5: generation
- 2xlarge: size

###### Types
- General Purpose
	1. Good for variety of workloads
	2. Balanced compute, memory and networking
	3. Starts with M, T and A
- Compute Optimized
	1. Optimized for compute optimized tasks
		- Batch processing workloads
		- media transcoding
		- high performance web servers
		- scientific modeling and machine learning
		- dedicated gaming servers
	2. Starts with the letter c
- Memory Optimized
	1. Fast performance for workloads that process large datasets in memory
	2. Use cases:
		- high performance databases
		- Caches
		- In-memory databases optimized for BI
		- Applications requiring real time processing of big unstructured data
	3. Starts with R, X1, High memory and Z
- Accelerated Computing
- Storage Optimized
	1. Great for storage intensive tasks that require high, sequential read and write for data stored in storage
	2. Use cases
		- High frequency OLTP
		- Relational and NoSQL databases
		- Cache for in-memory databases
		- Data warehousing apps
		- Distributed file systems
	3. Starts with i, D or H1
- HPC Optimized
###### Example
![[Pasted image 20250214122718.png]]

#### Security Groups
![[Pasted image 20250214140200.png]]
- only contain allow rules
- reference either by IP or another security group
- acting as "firewall" on EC2 Instances
- Regulate:
	1. Access to ports
	2. authorized IP ranges - IPv4 and IPv6
	3. Control of inbound network and outbound networks
- Can be attached to multiple instances
- Locked down to region / VPC combination
-  Lives outside the EC2
- If timeout, then a security group issue
- If connection refused, application error
- *All inbound blocked and all outbound authorized by default*
**Recommendation**: *maintain one separate security group for SSH access*

##### Referencing other security groups
![[Pasted image 20250214140802.png]]

Since *group 1* and *group 2* are attached, the EC2 instances can connect directly without thinking about the IP address.

###### Ports to know
| Port | Protocol                      |
| ---- | ----------------------------- |
| 21   | FTP                           |
| 22   | SSH                           |
| 22   | SFTP *(Using SSH)*            |
| 80   | HTTP                          |
| 443  | HTTPS                         |
| 3389 | RDP (Remote Desktop Protocol) |
#### Purchasing Options
##### On Demand
- Pay for what you use
	- Linux or Windows - per second, after first minute
	- All other operating systems - billing per hour
- highest cost but no upfront payment
- no long term commitment
- **Recommendation**: *for short-term and un-interrupted workloads* where you can't predict how the application will behave
##### Reserved Instances
- up to 72% discount compared to On Demand
- reserve a specific instance attribute (instance type, region, tenancy, OS)
- **Reservation Period** - 1 year (+discount) or 3 years (+++discount)
- **Payment Options** - No upfront (+), Partial Upfront (++), All Upfront (+++)
- **Scope** - Regional or Zonal
- **Recommended**: *steady-state usage applications* (database)
- *can buy and sell in the Reserved Instance Marketplace* if not needed anymore
- **Convertible Reserved Instance**
	- Can change the EC2 type, family, OS, scope and tenancy
	- Less discount (up to 66% of on demand price) than reserved instances
##### Savings Plans
- Get a discount based on long-term usage (up to 72%)
- Commit to a certain type of usage (*$10/hour for 1 or 3 years*)
- Any usage beyond is billed at On Demand rate
- Locked to a specific instance family and AWS Region
	- For example: m5 type of instance in us-east-1 region
- Flexible across:
	- instance size
	- OS
	- Tenancy
##### Spot Instances
- up to 90% discount compared to On Demand
- **can lose instance at any time**
- you define a max price you are willing to pay and if the spot price exceeds the max price, the instance might be lost
- most cost efficient instances
- not for critical jobs
- **Recommended**: *for workloads resilient to failure*
	- Batch jobs
	- Data analysis
	- Image processing
	- any distributed workloads
	- for workloads with flexible start and end time
##### EC2 Dedicated Hosts
- physical server with EC2 instance capacity fully dedicated to your use
- allows to address **compliance requirements**
- use your existing server bound software licenses
- **Purchasing Options**
	- On-demand - pay per second
	- Reserved - 1 or 3 years (No Upfront, Partial Upfront, All Upfront)
- The most expensive option
- Useful for software that have complicated licensing model (BYOL - Bring Your Own License)

##### EC2 Dedicated Instances
- Instances run on hardware dedicated to you
- may share hardware with other instances in same account
- no control over instance placement (can move hardware after stop/start)
![[Pasted image 20250214143758.png]]

##### EC2 Capacity Reservations
- Reserve On Demand instances capacity in a specific AZ for any duration
- Always have access to EC2 capacity when you need it
- No time commitment, no billing discounts
- Combine with Regional reserved instances and savings plans to benefit from billing discounts
- Charged at On Demand rate whether you run instances or not
- Suitable for short-term, uninterruptable workloads that need in specific AZ

## EC2 Instance Storage
### EBS Volume
> An EBS (Elastic Block Store) volume is a network drive that can be attached to instances
- Can persist data even after instance is terminated
- Bound to specific AZ
- **Analogy**: network USB Stick
- Network Drive
	- there might be a bit of latency during communication
	- can be detached from one EC2 instance and attached to another 
- Can use snapshots to move volume across AZ
- Need to provision capacity (size in GB, and IOPS) in advance
	- Can increase capacity over time
#### EBS Snapshots
- backup at a point in time
- not necessary to detach but recommended
##### Features
- EBS Snapshot Archive
	- Move to `archive tier` that is 75% cheaper
	- Takes 24 to 72 hours to restore from archive
- Recycle Bin for Snapshots
	- Setup rules to retain deleted snapshots so as to recover later
	- Specify retention (from 1 day to 1 year)

### AMI
- Amazon Machine Image
- customization of an EC2 Instance
	- can add own software, configuration, OS ...
	- faster boot / config time
- build for specific region (can be copied to other regions)
- Can launch EC2 instances from:
	- A public AMI: AWS Provided
	- Own AMI: make and maintain ourselves
	- AWS Marketplace AMI: made (and sold) by someone else
#### AMI Process (from EC2 Instance)
- Start and EC2 instance and customize
- stop the instance (*for data integrity*)
- Build an AMI (*this also creates EBS Snapshots*)
- launch other instances from AMI

#### EC2 Image Builder
- used to automate the creation of VM or container images
- Automate the creation, maintain, validate and test EC2 AMIs
![[Pasted image 20250214160249.png]]

- can be run on a schedule
- Free service (only pay for underlying resources)

### EC2 Instance Store
- when we need a high performance hardware disk
- attached physically
- better I/O performance
- ephemeral (temporary)
- **Good** for buffer / cache / scratch data / temporary content for short-term storage
- Risk of data loss if hardware fails
- Backups and replication are user's responsibility

### EFS - Elastic File System
- managed NFS (network file system)
- can be mounted to multiple EC2 instances at a time
- works only with Linux EC2 instances in multiple AZ
- highly scalable, available, expensive, pay per use, no capacity planning
	![[Pasted image 20250214160938.png]]

#### EBS vs EFS

| **EBS**                                  | **EFS**           |
| ---------------------------------------- | ----------------- |
| same AZ<br>requires snapshots to move AZ | spans multiple AZ |
#### EFS Infrequent Access (EFS-IA)
- cost-optimized for files not accessed every day
- up to 92% lower costs compared to EFS Standard
- files automatically moved to EFS-IA based on the last access time
- Enable with a Lifecycle Policy
	![[Pasted image 20250214161425.png]]

### Shared Responsibility 

| **AWS**                                             | **Customer**                                               |
| --------------------------------------------------- | ---------------------------------------------------------- |
| infrastructure                                      | setting up backup / snapshot procedures                    |
| replication for data for EBS Volumes and EFS drives | setting up data encryption                                 |
| replacing faulty hardware                           | responsibility of any data on the drives                   |
| ensuring the employees cannot access customer data  | understanding the risks associated with EC2 Instance Store |

### Amazon FSx
- launch third party high performance file systems on AWS
- fully managed service
- 3 offerings
	- Lustre
	- Windows File Server
	- NetApp ONTAP
#### Amazon FSx for Windows File Server
- built on Windows File Server
- a fully managed, highly reliable and scalable Windows native shared file system.
- Supports SMB protocol and Windows NTFS
- Integrated with Microsoft Active Directory
- can be accessed from AWS or on-premises infrastructure

#### Amazon FSx for Lustre
- fully managed, high performance, scalable file storage for HPC
- derived from "Linux" + "Cluster"
- Machine Learning, Analytics, Video Processing, ...
- Scales to 100s GB/s, millions of IOPS, sub-ms latencies
	![[Pasted image 20250214162343.png]]

### Summary
![[Pasted image 20250214162542.png]]
