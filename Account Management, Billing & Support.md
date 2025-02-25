# AWS Organizations
![[Pasted image 20250224151605.png]]
- global service
- allows to manage multiple AWS accounts
- main account is the master account
- Cost benefits:
	- Consolidated Billing
		- all accounts paid by the master account
		- single payment method
	- Pricing benefits from aggregated usage
		- volume discount for EC2, S3, ...
	- Pooling of Reserved EC2 instances for optimal savings
		- reserved instances shared across all accounts
		- if one does not use the reserved instances, other accounts can
- **API is available to automate AWS account creation**
- **can restrict account privileges using Service Control Policies (SCP)**
## Multi Account Strategies
- can create accounts per department, per cost center, per dev/test/prod, based on regulatory restrictions (using SCP), for better resource isolation, to have separate per-account service limits, isolated account for logging
- Multi Account vs One Account Multiple VPC
- should use tagging standard for billing purposes
- should enable CloudTrail on all accounts, send logs to central S3 account
- should send CloudWatch Logs to central logging account
## Organizational Units (OU) - Examples
![[Pasted image 20250224151453.png]]
## Service Control Policies (SCP)
- allows to whitelist or blacklist IAM actions
- Applied at the OU or Account level
- does not apply to the Master Account
- is applied to all the Users and Roles of the Account, including Root
- Does not apply to service-linked roles
	- service-linked roles enable other AWS services to integrate with AWS Organizations and can't be restricted by SCPs
- must have an explicit Allow (does not allow anything by default)
- Use cases:
	- restrict access to certain services
	- enforce PCI compliance by explicitly disabling services
### Examples
#### Blacklist and Whitelist Strategies
![[Pasted image 20250224151954.png]]
## Consolidated Billing
- when enabled:
	- **Combined Usage**
		- combine the usage across all AWS accounts in AWS Organization to **share the volume pricing, Reserved Instances and Savings Plans discounts**
	- **One bill**
		- get one bill for all AWS Accounts in the AWS Organization
- the management account can turn off Reserved Instances discount sharing for any account in AWS Organization, including itself
![[Pasted image 20250224152519.png]]
# AWS ControlTower
- easy way to **set up and govern a secure and compliant multi-account AWS environment** based on best practices
- Benefits
	- automate the set up of environment in few clicks
	- automate ongoing policy management using guardrails
	- detect policy violations and remediate them
	- monitor compliance through an interactive dashboard
- AWS ControlTower runs on top of AWS Organizations:
	- automatically sets up AWS Organizations to organize accounts and implement SCPs
# AWS Resource Access Manager (RAM)
- share AWS resources owned by our account with other AWS accounts
- share  with any account or within our Organization
- avoid resource duplication
- supported resources
	- Aurora
	- VPC Subnets
	- Transit Gateway
	- Route 53
	- EC2 Dedicated Hosts
	- ...
![[Pasted image 20250224154315.png]]
# AWS Service Catalog
- users might create stacks not in line with the rest of the organization
- some users might just want a quick self-service portal to launch a set of authorized products pre-defined by admins *(pre-configured)*
- includes: virtual machines, databases, storage options, etc...
## Service Catalog diagram
![[Pasted image 20250225110000.png]]
# Pricing Models in AWS
## 4 Pricing Models
### Pay as you go
- pay for what is used
- remain agile
- responsive
- meet scale demands
### Save when you reserve
- minimize risks
- predictably manage budgets
- comply with long-term requirements
- available for
	- EC2 Reserved instances
	- DynamoDB Reserved Capacity
	- ElastiCache Reserved Nodes
	- RDS Reserved Instance
	- Redshift Reserved Nodes
### Pay less by using more
- volume based discounts
### Pay less as AWS Grows

## Free services & free tier in AWS
- IAM
- VPC
- Consolidated Billing
- Elastic Beanstalk
- CloudFormation
- Auto Scaling Groups
*Note: need to pay for resources created*
# Compute Pricing
## EC2
- only charged for what is used
- number of instances
- instance configuration
	- physical capacity
	- region
	- OS and software
	- instance type
	- instance size
- ELB running time and amount of data processed
- detailed monitoring
### On-demand instances
- minimum 60s
- pay per second (Linux/Windows) or per hour (other)
### Reserved Instances
- up to 75% discount compared to on-demand on hourly rate
- 1 or 3 years commitment
- all upfront, partial upfront, no upfront
### Spot Instances
- up to 90% discount compared to on-demand on hourly rate
- bid for unused capacity
### Dedicated Host
- on demand
- reservation for 1 or 3 years commitment
## Lambda
- pay per call
- pay per duration
## ECS
- EC2 Launch Type Model
	- no additional fees
	- pay for AWS resources stored and created in application
## Fargate
- Fargate Launch Type Model
	- pay for vCPU and memory resources allocated to application in containers
# Storage Pricing
## S3
- **Storage Class**: S3 Standard, S3 Infrequent Access, S3 One-Zone IA, S3 Intelligent Tiering, S3 Glacier and S3 Glacier Deep Archive
- Number and size of objects: price can be tiered (based on volume)
- number and type of requests
- data transfer OUT of S3 region
- S3 Transfer Acceleration
- Lifecycle transitions
## EFS
> similar to S3
## EBS
- volume type (based on performance)
- storage volume in GB per month provisioned
- IOPS:
	- General Purpose SSD: included
	- Provisioned IOPS SSD: provisioned amount in IOPS
	- magnetic: number of requests
- Snapshots:
	- added data cost per GB per month
- Data transfer
	- outbound data transfer are tiered for volume discounts
	- inbound is free
# Database Pricing
## RDS
- per hour billing
- Database characteristics
	- Engine
	- Size
	- memory class
- purchase type
	- on-demand
	- reserved instance (1 or 3 years) with required up-front
- Backup Storage
	> no additional charge for backup storage up to 100% of total database storage for a region
- additional storage (per GB per month)
- number of input and output requests per month
- Deployment Type (storage and I/O are variable)
	- Single AZ
	- Multiple AZs
- Data Transfer
	- outbound data transfer are tiered for volume discounts
	- inbound is free
# Content Delivery
## CloudFront
- pricing different across different geographical regions
	![[Pasted image 20250225115110.png]]
- aggregated for each edge location, then applied to your bill
- data transfer out (volume discount)
- number of HTTP/HTTPS requests
# Networking Costs in AWS per GB - Simplified
![[Pasted image 20250225115324.png]]
# Savings Plan
- commit a certain $ amount per hour for 1 or 3 years
- easiest way to setup long-term commitment on AWS
- setup from AWS Cost Explorer console
- [Estimate Pricing](https://aws.amazon.com/savingsplans/pricing/)
## EC2 Savings Plan
- up to 72% discount compared to on-demand
- commit to usage of individual instance families in a region
- all upfront, partial upfront, no upfront
- regardless of AZ, size, OS or tenancy
## Compute Savings Plan
- up to 66% discount, compared to on-demand
- regardless of Family, Region, size, OS, tenancy, compute options
- Compute options: EC2, Fargate, Lambda
## Machine Learning Savings Plan
> for services such as SageMaker
# AWS Compute Optimizer
- reduce costs and improve performance by recommending optimal AWS resources for workloads
- helps choose optimal configurations and right size workloads (over/under provisioned)
- uses ML to analyze resource configurations and their utilization CloudWatch metrics
- supported resources:
	- EC2 instances
	- EC2 Auto Scaling Groups
	- EBS volumes
	- Lambda functions
- Lower costs by up to 25%
- recommendations can be exported to S3
# Billing and Costing Tools
- Estimating costs in cloud
	- Pricing Calculator
- Tracking costs in the cloud
	- Billing dashboard
	- Cost Allocation Tags
	- Cost and Usage Reports
	- Cost Explorer
- Monitoring against costs plans
	- Billing Alarms
	- Budgets
## AWS Pricing Calculator
[Pricing Calculator](https://calculator.aws)
- estimate cost for solution architecture
## AWS Billing Dashboard
- shows all the costs for the month, forecast and month-to-date
- also get access to AWS Free Tier Dashboard on the same page to track free tier resources usage
## Cost Allocation Tags
- track AWS costs on detailed level and group them
- can use different tags
	- **AWS generated tags**
		- Automatically applied to resource
		- starts with prefix `aws:` (e.g. aws:createdBy)
	- **User-defined tags**
		- defined by the user
		- starts with prefix `user:`
### Tagging and Resource Groups
- tags are used for organizing resources
	- EC2: instances, images, load balancers, security groups...
	- RDS, VPC resources, Route 53, IAM users, etc...
	- resourced created by CloudFormation are all tagged the same way
- Free naming convention
	- common tags are: Name, Environment, Team...
- can be used to create **Resource Groups**
	- create, maintain and view a collection of resources that share common tags
	- manage tags using Tag Editor
## Cost and Usage Reports
- deeper dive into AWS costs and usage
- contains the most detailed set of AWS costs and usage data available, including metadata about AWS services, pricing and reservations
- lists AWS usage for each service category used, by an account and its IAM users in hourly or daily line items, as well as anu tags that has been activated for cost allocation purposes
- can be integrated with Athena, Redshift or QuickSight for analysis.
## Cost Explorer
- visualize, understand and manage AWS costs and usage over time
- can create custom reports that analyze cost and usage data
- analyze data at a high level
- total costs and usage across all accounts
- monthly, hourly, resource level granularity
- be able to choose an optimal **Savings Plan**
- forecast usage up to 12 months based on previous usage
#### Monthly Costs by AWS Service
![[Pasted image 20250225141717.png]]
#### Hourly & Resource Level
![[Pasted image 20250225141756.png]]
#### Savings Plan
> alternative to reserved instances
![[Pasted image 20250225141848.png]]
#### Forecast Usage
![[Pasted image 20250225141928.png]]
## Billing Alarms
- billing data metric is stored in CloudWatch us-east-1
- billing data are for overall worldwide AWS costs
- actual cost and not projected costs
- intended as a simple alarm
## AWS Budgets
- create budget
- send alarms when budget exceeded by cost or forecast
- 4 types of budgets: Usage, Cost, Reservation, Savings Plans
- For Reserved Instances (RI)
	- track utilization
	- supports EC2, ElastiCache, RDS, Redshift
- Up to 5 SNS notifications per budget
- can filter by: Service, Linked Account, Tag, Purchase Option, Instance Type, Region, Availability Zone, API Operation, etc...
- same options are AWS Cost Explorer
- 2 budgets free, then $0.02/day/budget
# AWS Cost Anomaly Detection
- continuously monitor cost and usage using ML to detect unusual spends
- learns unique, historic spending patterns to detect on-time cost spike and/or continuous cost increase 
- don't need to define thresholds
- monitors services, member accounts, cost allocation tags or cost categories
- sends anomaly detection reports with root-cause analysis
- get notified with individual alerts or daily/weekly summary (using SNS)
![[Pasted image 20250225143255.png]]
# AWS Service Quotas
- notifies when close to service quota value threshold
- can create CloudWatch alarms directly on the Service Quotas console
- *Example:* Lambda concurrent executions
- can request a quota increase from AWS Service Quotas or shutdown resources before limit is reached
![[Pasted image 20250225143532.png]]
# AWS Trusted Advisor
- high level AWS account assessment
- checks for few things and advises on them
	![[Pasted image 20250225143643.png]]
- analyze AWS account and provides recommendation on 6 categories
	- Cost Optimization
	- Performance
	- Security
	- Fault tolerance
	- Service limits
	- Operational Excellence
- free checks
	- part of security
	- service limits
- **Business & Enterprise Support plan**
	- Full set of checks
	- programmatic access using *AWS Support API*
# AWS Support Plans Pricing
![[Pasted image 20250225144525.png]]
## Basic Support
- **Customer Service & Communities**
	- 24x7 access to customer service, documentation, whitepaper and support forums
- **AWS Trusted Advisor**
	- access to 7 core checks 
	- guidance to provision resources following best practices to increase performance and improve security
- **AWS Personal Health Dashboard**
	- personalized view of health of AWS services, and alerts when resources are impacted
## Developer Support Plan
- all Basic Support Plan 
- **Business hours email access** to Cloud Support Associates
- unlimited cases / unlimited contacts
- **Case Severity / response times**
	- General guidance: < 24 business hours
	- System impaired: < 12 business hours
## Business Support Plan (24/7)
- intended to be used for **production workloads**
- **Trusted Advisor** - full set of checks + API access
- 24x7 phone, email, and chat access to Cloud Support Engineers
- unlimited cases / unlimited contacts
- access to Infrastructure Event Management for additional fee
- **Case Severity / response times**
	- General guidance: < 24 business hours
	- System impaired: < 12 business hours
	- Production system impaired: < 4 hours
	- Production system down: < 1 hour
## AWS Enterprise On-Ramp Support Plan
- intended for production or business critical workloads
- All of Business Support Plan
- access to a pool of **Technical Account Managers (TAM)**
- **Concierge Support Team** (for billing and account best practices)
- **Infrastructure Event Management, Well-Architected & Operation Reviews**
- **Case Severity / response times**
	- General guidance: < 24 business hours
	- System impaired: < 12 business hours
	- Production system impaired: < 4 hours
	- Production system down: < 1 hour
	- Business-critical system down: < 30 minutes
## AWS Enterprise Support Plan
- intended for mission critical workloads
- all of Business Support Plan
- access to a ==designated== **TAM**
- **Concierge Support Team** (for billing and account best practices)
- **Infrastructure Event Management, Well-Architected & Operation Reviews**
- Access to **AWS Incident Detection and Response** (for an additional fee)
- **Case Severity / response times**
	- General guidance: < 24 business hours
	- System impaired: < 12 business hours
	- Production system impaired: < 4 hours
	- Production system down: < 1 hour
	- Business-critical system down: < 15 minutes
# Summary
## Account Best Practices
![[Pasted image 20250225152813.png]]

## Billing and Costing Tools
![[Pasted image 20250225152847.png]]