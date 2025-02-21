![[Pasted image 20250216154840.png]]
# S3
#### Use Cases
- Backup and storage
- Disaster recovery
- Archive
- Hybrid Cloud Storage
- Application Hosting
- Media Hosting
- Data lakes & big data analytics
- Software delivery
- Static Website

### Buckets
- store objects(*files*) in buckets(*directories*)
- must have globally unique name (**across all regions all accounts**)
- defined at region level
- Naming convention
	- No uppercase, no underscore
	- 3-63 characters long
	- not an IP
	- must start with lowercase letter or number
	- must not start with the prefix **xn--**
	- must not end with suffix **-s3alias**
### Objects
- have key
	- key = full path
		- s3://my-bucket/my_file.txt
	- composed of prefix + object name
- no concept of directories
- Values are content of body
	- max size 5TB
	- if uploading more than 5GB, must use multi-part upload
- Metadata
- Tags (up to 10) - useful for security/lifecycle
- version ID (if versioning enabled)

## Security
### User Based
 - IAM Policies
	 Which API calls should be allowed for specific user from IAM
### Resource Based
- Bucket Policies
	Bucket wide rules from the S3 console - allows cross account access
- Object ACL
	finer grain (can be disabled)
- Bucket ACL
	less common (can be disabled)

	*Note*: an IAM principal can access an S3 object if
	- The user IAM permissions **ALLOW** it ***OR*** the resource policy **ALLOWS** it
	- ***AND*** there's no explicit **DENY**

### Encryption
Encrypt objects in Amazon S3 using encryption keys

## S3 Bucket Policies
- JSON based policies
	- Resources: buckets and objects
	- Effect: Allow/Deny
	- Actions: Set of API to Allow or Deny
	- Principal: The account or user to apply the policy to
	![[Pasted image 20250216105516.png]]
- Use S3 bucket for policy to:
	- Grant public access to the bucket
	- Force objects to be encrypted at upload
	- Grant access to another account (Cross Account)
#### Example: Public Access - Use Bucket Policy
![[Pasted image 20250216110226.png]]

#### Example: User Access to S3 - IAM Permissions
![[Pasted image 20250216110302.png]]

#### Example: EC2 instance access - Use IAM Roles
![[Pasted image 20250216110343.png]]

#### *Advanced*: Cross-Account Access - Use Bucket Policy
![[Pasted image 20250216110502.png]]

### Bucket Settings for Block Public Access
![[Pasted image 20250216110643.png]]
- Created to prevent company data leaks
- leave on if bucket should never be public
- can be set at account level

## Amazon S3 - Static Website Hosting
- can host static websites accessible on the Internet
- **403 Forbidden** error if bucket does not allow for public reads

## Versioning
- enabled at bucket level
- same key overwrite will change the "version": 1,2,3...
- best practice to version buckets
	- protect against unintended deletes
	- easy roll back
*Note*: 
- any file that is not versioned prior to enabling versioning will have version "null"
- suspending versioning does not delete the previous versions

## Replication (CRR & SRR)

![[Pasted image 20250216135246.png]]
- must enable Versioning in source and destination buckets
- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)
- Buckets can be in different AWS Accounts
- copying is asynchronous
- must give proper IAM permissions

#### Use Cases:
- CRR - compliance, lower latency access, replication across accounts
- SRR - log aggregation, live replication between production and test accounts

## Storage Classes
- Classes
	- Amazon S3 Standard - General Purpose
	- Amazon S3 Standard-Infrequent Access (IA)
	- Amazon S3 One Zone-Infrequent Access
	- Amazon S3 Glacier Instant Retrieval
	- Amazon S3 Glacier Flexible Retrieval
	- Amazon S3 Glacier Deep Retrieval
	- Amazon S3 Intelligent Tiering
- Can move between classes manually or using S3 Lifecycle configurations

#### S3 Durability and Availability
- Durability
	- High durability (99.999999999%, *11 9's*) of objects across multiple AZ
	- Same for all storage classes
- Availability
	- Measures how readily available a service is
	- varies depending on storage class

### S3 Standard - General Purpose
- 99.99% availability
- used for frequently accessed data
- low latency and high throughput
- sustain 2 concurrent facility failures
- Use Cases
	- Big data analytics
	- mobile & gaming applications
	- content distribution

### S3 Storage Classes - Infrequent Access
- for data that is less frequently accessed
- rapid access when needed
- lower cost than S3 Standard
- **Amazon S3 Standard-Infrequent Access (S3 Standard-IA)**
	- 99.9% availability
	- Use Cases
		- Disaster Recovery, Backups
- **Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA)
	- high durability (*11 9's*) in a single AZ
	- data lost when AZ destroyed
	- 99.5% availability
	- Use Cases
		- Storing secondary backup copies of on-premise data
		- re-creatable data
### Amazon S3 Glacier Storage Classes
- Low cost object storage for archive/backup
- Pricing: price for storage + object retrieval cost
- **Amazon S3 Glacier Instant Retrieval**
	- millisecond retrieval
	- great for data accessed once a quarter
	- minimum storage duration 90 days
- **Amazon S3 Glacier Flexible Retrieval** *(formerly Amazon S3 Glacier)*
	- 3 Flexibility levels
		- Expedited (1 to 5 minutes)
		- Standard (3 to 5 hours)
		- Bulk (5 to 12 hours) - Free
	- minimum storage duration of 90 days
- **Amazon S3 Glacier Deep Archive** - for long term storage
	- 2 Tiers of retrieval
		- Standard (12 hours)
		- Bulk (48 hours)
	- minimum storage duration 180 days

### S3 Intelligent-Tiering
- small monthly monitoring and auto-tiering fee
- moves objects automatically between tiers based on access frequency
- no retrieval charges
- Access tiers
	- *Frequent Access tier (automatic)*: default tier
	- *Infrequent Access tier (automatic)*: objects not accessed for 30 days
	- *Archive Instant Access tier (automatic)*: objects not accessed for 90 days
	- *Archive Access Tier (optional)*: configurable from 90days to 700+ days
	- *Deep Archive Access Tier (optional)*: configurable from 180days to 700+ days
![[Pasted image 20250216144842.png]]


## S3 Encryption
 ![[Pasted image 20250216151346.png]]
## IAM Access Analyzer for S3
- ensure only intended people have access
- Example: publicly accessible bucket, bucket shared with other AWS account...
- evaluates S3 bucket policies, ACLs, Access Point policies
- Powered by IAM Access Analyzer
Using this we can review the policies and make changes if unintended changes are detected.

## Shared Responsibility Model for S3

| **AWS**                                                                                                    | **Customer**                           |
| ---------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| infrastructure (global security, durability, availability, sustain concurrent data loss in two facilities) | S3 Versioning                          |
| configuration and vulnerability analysis                                                                   | S3 Bucket Policies                     |
| compliance validation                                                                                      | S3 Replication Setup                   |
|                                                                                                            | Logging and Monitoring                 |
|                                                                                                            | S3 Storage Class                       |
|                                                                                                            | Data encryption at rest and in transit |

# AWS Snow Family
- highly-secure, portable devices to collect and process data at the edge
- migrate data into and out of AWS
![[Pasted image 20250216152318.png]]

## Data Migrations with AWS Snow Family
![[Pasted image 20250216152537.png]]

### Diagrams
 - Direct upload to S3
	 ![[Pasted image 20250216152634.png]]
- With Snow Family
	![[Pasted image 20250216152812.png]]
	- offline data transfer

### Snow Family - Usage Process
1. Request Snowball device from AWS console for delivery
2. Install snowball client / AWS OpsHub on our servers to transfer data
3. Connect snowball to the servers and copy files using the client
4. Ship the device back to AWS
5. Data will be loaded into an S3 bucket
6. Snowball is completely wiped

## Edge Computing
- process data while it's being created on an edge location
- the edge locations might have limited internet and no access to computing power
- we setup Snowball Edge / Snowcone device to do edge computing
	- Snowcone: 2CPUs, 4GB of memory, wired or wireless access
	- Snowball Edge Compute Optimized (*dedicated for that use case*) & Storage Optimized
	- Run EC2 Instances or Lambda functions at the edge
- Use cases: preprocess data where created, ML where data is created, transcoding media while being shipped back to AWS

## Snowball Edge Pricing
- pay for device usage and data transfer out of AWS
- Data transfer **IN** to S3 is $0.00 per GB
- 2 Pricing Strategies:
	- **On-Demand**
		- one-time service fee per job which includes
			- 10 days usage for Snowball Edge Storage Optimized 80TB
			- 15 days usage for Snowball Edge Storage Optimized 210TB
		- shipping days are *NOT* counted towards the included 10 or 15 days
		- pay per day for any extra days
	- **Committed Upfront**
		- pay in advance for monthly, 1-year and 3-years of usage (**Edge Computing**)
		- up to 62% discounted pricing

# Hybrid Cloud for Storage
- AWS is pushing for "hybrid cloud"
- This can be due to
	- Long cloud migrations
	- Security requirements
	- Compliance requirements
	- IT Strategy
- S3 is a proprietary storage technology (unlike EFS/NFS). So to expose, we have to use **Amazon Storage Gateway**. 


## AWS Storage Gateway
- bridge between on-premise data and cloud data in S3
- Hybrid storage service to allow on-premises to seamlessly use the AWS Cloud
- Use Cases
	- Disaster Recovery
	- Backup and Restore
	- Tiered Storage
#### Types
1. File Gateway
2. Volumes Gateway
3. Tapes Gateway
	![[Pasted image 20250216155120.png]]

# Summary
![[Pasted image 20250216155932.png]]
