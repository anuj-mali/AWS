# AWS Shared Responsibility Model
![[Pasted image 20250222145136.png]]
- AWS - Security **of** the cloud
	- protecting infrastructure
	- managed service like [[Amazon S3]], [[Databases & Analytics#DynamoDB|DynamoDB]], [[Databases & Analytics#Amazon RDS|RDS]], etc.
- Customer - Security **in** the cloud
	- For EC2 instance, customer is responsible for management of guest OS, firewall and network configuration, IAM
	- encrypting the data
- Shared controls
	- Patch management, configuration management, awareness & training
## Example: RDS
- AWS Responsibility
	- manage the underlying [[EC2|EC2 instances]], disable SSH access
	- automated DB patching
	- Automated OS patching
	- audit the underlying instance and disks & guarantee it functions
- Customer Responsibility
	- check the ports/IP/security group inbound rules in DB's SG
	- in-database user creation and permissions
	- creating a database with or without public access
	- ensure parameter groups or DB is configured to only allow SSL connection
	- data encryption settings
## Example: S3
- AWS responsibility:
	- guarantee unlimited storage
	- guarantee encryption
	- ensure separation of data between different customers
	- ensure AWS employees can't access data
- Customer responsibility
	- bucket configuration
	- bucket policy/public setting
	- IAM user and roles
	- Enabling encryption
# DDoS Protection on AWS
## Overview
- **AWS Shield Standard**: protects against [[DDoS]] attack for website and applications, for all customers at no additional costs
- **AWS Shield Advanced**: 24/7 premium [[DDoS]] Protection
- **AWS WAF**: filter specific requests based on rules
- [[AWS Global Infrastructure#Global Content Delivery Network (CDN) ==CloudFront==|CloudFront]] and [[AWS Global Infrastructure#Global DNS ==Route 53==|Route 53]]:
	- availability protection using global edge network
	- combined with AWS Shield, provides attack mitigation at the edge
- Being ready to scale - leverage [[Elastic Load Balancing & Auto Scaling Groups#Auto Scaling Group|Auto Scaling]]
## Sample Reference Architecture for DDoS Protection
![[Pasted image 20250222151317.png]]
## AWS Shield
### Shield Standard
- free service for all AWS users
- protection from attacks such as SYN/UDP Floods, Reflection attacks and other layer 3/4 attacks
### Shield Advanced
- optional DDoS mitigation service
- protect against more complex attacks on [[EC2]], [[Elastic Load Balancing & Auto Scaling Groups#Why use Elastic Load Balancer?|ELB]], [[AWS Global Infrastructure#Global Content Delivery Network (CDN) ==CloudFront==|CloudFront]], [[AWS Global Infrastructure#==AWS Global Accelerator==|Global Accelerator]] and [[AWS Global Infrastructure#Global DNS ==Route 53==|Route 53]]
- 24/7 access to AWS DDoS response team (DRP)
- protect against higher fees during usage spikes due to DDoS
## AWS WAF - Web Application Firewall
- protects web apps from common web exploits on Layer 7
- Layer 7 = HTTP
- since layer 7, it can only be deployed on HTTP friendly devices
- can be deployed on [[Elastic Load Balancing & Auto Scaling Groups#Application Load Balancer|ALB]], [[Compute Services#Amazon API Gateway|API Gateway]], [[AWS Global Infrastructure#Global Content Delivery Network (CDN) ==CloudFront==|CloudFront]]
- define Web ACL
	- rules in ACL can include IP addresses, HTTP headers, HTTP body or URI strings
	- Protects from common attack - SQL injection and Cross-Site Scription (XSS) 
	- can have size constraints and block countries using geo-match
	- for DDoS protection, can use Rate-based rules (to count occurrences of events)
# AWS Network Firewall
- protect entire [[VPC & Networking#VPC|VPC]]
- from layer 3 to 7 protection
- any direction
	- [[VPC & Networking#VPC|VPC]] to [[VPC & Networking#VPC|VPC]] traffic
	- outbound to internet
	- inbound from internet
	- to/from [[VPC & Networking#Direct Connect (DX)|Direct Connect]] & [[VPC & Networking#Site to Site VPN|Site-to-Site VPN]]
![[Pasted image 20250222160629.png]] 
# AWS Firewall Manager
- allows to manage security rules in all accounts of an AWS Organization
- Security Policy: common set of security rules
	- VPC Security Groups for [[EC2]], [[Elastic Load Balancing & Auto Scaling Groups#Application Load Balancer|ALB]], etc...
	- [[#AWS WAF - Web Application Firewall]] rules
	- [[#Shield Advanced]] rules
	- [[#AWS Network Firewall]]
- Rules are applied to new resources as they are created (*good for compliance*) across all and future accounts in you Organization
# Penetration Testing on AWS Cloud
- customer can carry out security assessment without prior approval for 8 services:
	- [[EC2]] instances
	- [[VPC & Networking#Internet Gateway & Nat Gateways|NAT Gateways]]
	- [[Elastic Load Balancing & Auto Scaling Groups#Why use Elastic Load Balancer?|ELB]]
	- [[Databases & Analytics#Amazon RDS|RDS]]
	- [[AWS Global Infrastructure#Global Content Delivery Network (CDN) ==CloudFront==|CloudFront]]
	- [[Databases & Analytics#Amazon Aurora|Aurora]]
	- [[Compute Services#Amazon API Gateway|API Gateway]]
	- [[Compute Services#AWS Lambda|AWS Lambda]] and Lambda Edge functions
	- [[Compute Services#Amazon Lightsail|Amazon Lightsail]] resources
	- [[Deployments & Managing Infrastructure#AWS Elastic Beanstalk|Elastic Beanstalk environments]]
- Prohibited Activities
	- [[DNS]] zone walking via [[AWS Global Infrastructure#Global DNS ==Route 53==|Route 53]] Hosted Zones
	- DoS, [[DDoS]], Simulated DoS, Simulated [[DDoS]]
	- port flooding
	- protocol flooding
	- request flooding (login request flooding, API request flooding)
# Encryption
## Data at rest vs Data in transit
- At rest: data stored or archived on a device
	- on a hard drive, RDS instance, S3 Bucket, etc.
- In transit: data being moved from one location to another
	- transfer from on-premises to AWS, EC2 to DynamoDB, etc.
	- mean data transferred on a network
- encrypt data in both states to protect it
- use encryption keys

## AWS KMS (Key Management Service)
- AWS manages the encryption keys for us.
- we just define who can access the keys
- Encryption Opt-in:
	- EBS volumes: encrypt volumes
	- S3 buckets: Server-side encryption of objects (SS3-S3 enabled by default, SSE-KMS opt in)
	- Redshift database: encryption of data
	- RDS database: encryption of data
	- EFS drives: encryption of data
- Encryption automatically enabled:
	- CloudTrail logs
	- S3 Glacier
	- Storage Gateway
## CloudHSM
- AWS provision encryption hardware
- keys are managed by customers unlike KMS
- Dedicated hardware (HSM = Hardware Security Module)
- HSM device is tamper resistant, FIPS 140-2 Level 3 compliance
![[Pasted image 20250222173133.png]]
### CloudHSM Diagram
![[Pasted image 20250222173250.png]]
## Types of Keys
- Customer Managed Key
	- create, manage and used by the customer, can enable or disable
	- possibility of rotation policy.
		*Example*: new key generated every year, old key preserved
	- possibility to bring-your-own-key
- AWS Managed Key
	- created, managed and used on the customer's behalf by AWS
	- used by AWS services (S3, EBS, Redshift)
- AWS Owned Key
	- collection of CMKs that an AWS service owns and manages to use in multiple accounts
	- AWS can use those to protect resources in account (customer cannot view the keys)
- CloudHSM Keys(custom keystore)
	- keys generated from own CloudHSM hardware device
	- cryptographic operations are performed within CloudHSM cluster
# AWS Certificate Manager (ACM)
- service to easily provision, manage and deploy SSL/TLS certificates
- used to provide in-transit encryption for websites (HTTPS)
- supports both public and private TLS certificates
- free of charge for public TLS certs
- automatic TLS cert renewal
- integrations with
	- ELB
	- CloudFront Distribution
	- APIs on API Gateway
![[Pasted image 20250223103046.png]] 
# AWS Secrets Manager
- for storing secrets
- can force rotation of secrets every X days
- automate generation of secrets on rotation (uses Lambda)
- Integration with Amazon RDS (MySQL, PostgreSQL, Aurora)
- encrypted using KMS
# AWS Artifact
- portal that provides customers with on-demand access to AWS compliance documentation and AWS agreements
- **Artifact Reports** - allows to download AWS security and compliance reports from third-party auditors, like AWS ISO certifications, Payment Card Industry (PCI), and System and Organization Control (SOC) reports
- **Artifact Agreements** - allows to review, accept, and track the status of AWS agreements such as the Business Associate Addendum (BAA) or the Health Insurance Portability and Accountability Act (HIPAA) for an individual account or in organization.
- can be used to support internal audit or compliance
# Amazon GuardDuty
- intelligent threat discovery to protect AWS Account
- uses ML algorithms, anomaly detection, 3$^{rd}$ party data
- one click enable (30 days trial), no need to install software
- input data includes
	- **CloudTrail Events Logs** - unusual API calls, unauthorized deployments
		- CloudTrail Management Events - create VPC subnet, create trail, ...
		- CloudTrail S3 Data Events - get object, list objects, delete object, ...
	- VPC Flow Logs - unusual internal traffic, unusual IP address
	- DNS Logs - compromised EC2 instances sending sending encoded data within DNS queries
	- Optional Features - EKS Audit Logs, RDS & Aurora, EBS, Lambda, S3 Data Events...
- can setup EventBridge rules to be notified in case of findings
- EventBridge rules can target AWS Lambda or SNS
- can protect against CryptoCurrency attacks as it has dedicated "finding" for it
![[Pasted image 20250223111942.png]] 
# Amazon Inspector
- automated security assessments
- For EC2 instances:
	- leveraging AWS System Manager (SSM) agent
	- analyze unintended network accessibility
	- analyze the running OS against known vulnerabilities
- For Container Images push to Amazon ECR
	- assessment of Container Images as they are pushed
- For Lambda Functions
	- analyzes software vulnerabilities in function code and package dependencies
	- assessment of functions happens as they are deployed
- reporting and integration with AWS Security Hub
- sending findings to Amazon EventBridge
![[Pasted image 20250223135405.png]]
## What does Amazon Inspector evaluate?
- continuous scanning of the infrastructure but does it intelligently so as to not have redundant scans
- package vulnerabilities (EC2, ECR & Lambda) using database of CVE (**Common Vulnerabilities and Exposures**)
- Network reachability (EC2)
- a risk score is associated with all vulnerabilities for prioritization
# AWS Config
- helps with auditing and recording compliance of AWS resources against defined rules
- helps record configurations and changes over time
- possibility of storing the configuration data into S3 (analyzed by Athena)
- Questions that can be solved by AWS Config:
	- is there unrestricted SSH access to my security groups?
	- do buckets have any public access?
	- how has ALB configurations changed over time?
- can receive alerts (SNS) for any changes
- is per-region service
- can be aggregated across regions and accounts
## AWS Config Resource
- view compliance of resource over time
	![[Pasted image 20250223142123.png]]
- view configuration of resource over time
	![[Pasted image 20250223142140.png]]
- view CloudTrail API calls if enabled
# Amazon Macie
- fully managed data security and data privacy service
- uses ML and pattern matching to discover and protect sensitive data in AWS
- helps identify and alert to sensitive data such as Personally Identifiable Information (PII)
![[Pasted image 20250223142750.png]]
# AWS Security Hub
- central security tool
- manage security across several AWS accounts
- automate security checks
- has integrated dashboards showing current security and compliance status to quickly take actions
- automatically aggregate alerts in predefined or personal findings formats from various AWS services & AWS partner tools
	- Config
	- GuardDuty
	- Inspector
	- Macie
	- IAM Access Analyzer
	- AWS Systems Manager
	- AWS Firewall Manager
	- AWS Health
	- AWS Partner Network Solutions
- must first enable the AWS Config Service
![[Pasted image 20250223145849.png]]
# Amazon Detective
- security findings might require deeper analysis to isolate the root cause and take action. 
- Amazon Detective analyzes, investigates and quickly identifies ==the root cause of security issues== or suspicious activities (using ML and graphs)
- automatically collects and processes events from VPC Flow Logs, CloudTrail, GuardDuty and create a unified view
- produces visualizations with details and context to get to the root cause
# AWS Abuse
- report suspected AWS resources used for abusive or illegal purposes
- abusive & prohibited behaviors are:
	- **Spam** - getting unwanted emails from AWS-owned IP address, websites & forums spammed by AWS resources
	- **Port scanning** - sending packets to ports to discover the unsecured ones
	- **DoS or DDoS attacks** - AWS-owned IP addresses attempting to overwhelm or crash servers/software
	- **Intrusion attempts** - unauthorized access
	- **Hosting objectionable or copyrighted content** - distributing illegal or copyrighted content without consent
	- **Distributing malware** - AWS resources distributing software to harm computers or machines
- contact AWS Abuse team
# Root User Privileges
- Root user = account owner
- complete access to all AWS services and resources
- **Recommended** - Lock AWS root user access keys
- should not use root user for everyday tasks, even administrative tasks
- Actions that can only be performed by root user:
	- **Change account settings** (account name, email address, root user password, root user access keys)
	- view certain tax invoices
	- **close AWS account**
	- restore IAM user permissions
	- **change or cancel AWS Support plan**
	- **register as a seller in the Reserved Instance Marketplace**
	- configure an Amazon S3 bucket to enable MFA
	- edit or delete an Amazon S3 bucket policy that includes an invalid VPC ID or VPC Endpoint ID
	- sign up for GovCloud
# IAM Access Analyzer
- service that is used to find out which resources are going to be shared externally
	- S3 buckets
	- IAM roles
	- KMS keys
	- Lambda functions and layers
	- SQS queues
	- Secrets Manager Secrets
- Define **Zone of Trust** = AWS Account or AWS Organization
- Access outside zone of trusts => reported as findings
![[Pasted image 20250223153337.png]]
# Summary
![[Pasted image 20250223154310.png]]
![[Pasted image 20250223154325.png]]
