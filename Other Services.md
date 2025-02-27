# Amazon WorkSpaces
- managed Desktop as a Service (DaaS) solution to easily provision Windows or Linux desktops
- Great to eliminate management of on-premises VDI (Virtual Desktop Infrastructure)
- fast and quickly scalable
- Secured data - integrated with KMS
- pay-as-you-go service with monthly or hourly rates
![[Pasted image 20250225194723.png]]
## Multiple Regions
- deploy workspaces as close to the user as possible
![[Pasted image 20250225194807.png]]
# Amazon AppStream 2.0
- Desktop Application Streaming Service
- deliver to any application, without acquiring, provisioning infrastructure
- application is delivered from within a web browser
![[Pasted image 20250225195109.png]]
## AppStream vs WorkSpaces
- WorkSpaces
	- fully managed VDI and desktop available
	- users connect to VDI and open native or WAM applications
	- WorkSpaces are on-demand or always on
- AppStream 2.0
	- stream a desktop application to web browsers
		- no need to connect to a VDI
	- works with any device that has a web browser
	- allow to configure an instance type per application type
		- CPU
		- RAM
		- GPU
# AWS IoT Core
- allows to easily connect [[IoT]] devices to AWS Cloud
- serverless, secure & scalable to billions of devices and trillions of messages
- act as pub/sub to allows the devices to communicate
- applications can communicate with devices even when they are not connected
- integrates with AWS Services such as Lambda, S3, SageMaker, ...
- allows to build IoT applications that gather, process, analyze and act on data
![[Pasted image 20250225195817.png]]
# Amazon Elastic Transcoder
- used to convert media files stored in S3 to media files in formats required by consumer playback devices (phones, etc...)
- Benefits:
	- easy to use
	- Highly scalable - can handle large volumes of media files and large file sizes
	- Cost Effective - duration based pricing model
	- Fully managed & secure
	- pay for what you use
![[Pasted image 20250225200505.png]]
# AWS AppSync
- to build backend for mobile and web application
- store and sync data across mobile and web apps in real-time
- makes use of GraphQL
- Client code can be generated automatically
- integrations with DynamoDB / Lambda
- real-time subscriptions
- offline data synchronization
- fine grained security
- AWS Amplify can leverage AppSync in the background
# AWS Amplify
- set of tools and services that helps you develop and deploy scalable full stack web and mobile applications
- can manage Authentication, Storage, API (REST, GraphQL), CI/CD, PubSub, Analytics, AI/ML Predictions, Monitoring, Source Code from AWS, GitHub, etc...
- *can be viewed as Elastic Beanstalk for web and mobile applications*
![[Pasted image 20250225204110.png]]
# AWS Infrastructure Composer
- visually design and build serverless applications quickly on AWS
- deploy AWS infrastructure code without needing to be expert in AWS
- can configure how resources interact with each other
- generates IaC using CloudFormation
- ability to import CloudFormation / SAM templates to visualize them
# AWS Device Farm
- fully managed service
- tests web and mobile apps against desktop browsers, real mobile devices and tablets
- run tests concurrently on multiple devices
- ability to configure device settings (GPS, language, Wi-Fi, Bluetooth, ...)
- can send logs, screenshots and reports
- can interact with devices
![[Pasted image 20250227104907.png]]
# AWS Backup
- fully managed service
- centrally manage and automate backups across AWS services
- on-demand and scheduled backups
- supports PITR (Point-in-time Recovery)
- Retention Periods, Lifecycle Management, Backup Policies, ...
- Cross-Region Backup
- Cross-Account Backup (backed by AWS Organization)
![[Pasted image 20250227105155.png]]
# Disaster Recovery Strategies
![[Pasted image 20250227105927.png]]
## Backup and Restore
- cheapest
- data is backed up in the cloud
- restored in case of a disaster
- since no app is running and just data is being backed up, cost is minimal
![[Pasted image 20250227105505.png]]
## Pilot Light
- runs just the core functions in the cloud. For example: database
- minimal critical functions of the app are in the cloud at minimal setup
![[Pasted image 20250227105634.png]]
## Warm Standby
- full app in the cloud at minimal size
- just need to increase the size of the app during disaster recovery
![[Pasted image 20250227105735.png]]
## Multi-Site / Hot-Site
- full version of the app at full size on the cloud
- maximum costs
![[Pasted image 20250227105817.png]]
# AWS Elastic Disaster Recovery (DRS)
- allows to quickly and easily recover physical, virtual and cloud-based servers into AWS
- Example: protect most critical databases, enterprise apps (SAP), protect data from ransomware attacks, ...
- continuous block-level replication of servers
![[Pasted image 20250227110830.png]]
# AWS DataSync
- allows to move large amounts of data from on-premises to AWS
- can synchronize to: Amazon S3(any storage classes), Amazon EFS, Amazon FSx for Windows
- replication tasks can be scheduled hourly, daily, weekly
- replication tasks are *incremental* after the first full load
![[Pasted image 20250227111337.png]]
# Cloud Migration Strategies
![[Pasted image 20250227112043.png]]
## Retire
- turn off things we don't need (maybe as a result of re-architecting)
- helps reducing the surface areas for attacks (more security)
- save cost, maybe up 10% to 20%
- focus attention on resources that must be maintained
## Retain
- do nothing for now
- security, data compliance, performance, unresolved dependencies
- no business value to migrate, mainframe or mid-range and non-x86 Unix apps
## Relocate
- move apps from on-premises to Cloud version
- move EC2 instances to a different VPC, AWS account or AWS Region
- **Example**: transfer servers from VMWare Software-defined Data Center (SSDC) to VMware Cloud on AWS
## Rehost
- lift and shift
- simple migrations by re-hosting on AWS
- migrate machines (physical, virtual, another Cloud) to AWS Cloud
- no cloud optimizations being done, applications migrated as it
- could save as much as 30% on cost
- **Example**: migrate using AWS Application Migration Service
## Replatform
- lift and reshape
- **Example**: migrate database to RDS
- **Example**: migrate application to Elastic Beanstalk
- not changing the core architecture, but leverage some Cloud optimizations
- save time and money by moving to a fully managed service or Serverless
## Repurchase
- drop and shop
- moving to a different product while moving to the Cloud
- often move to SaaS platform
- expensive in short term but quick to deploy
- **Example**:CRM to Salesforce.com, HR to Workday, CMS to Drupal
## Refactor/Re-architect
- reimagining how the application is architected using Cloud Native features
- driven by need of the business to add features and improve scalability, performance, security and agility
- break monolithic applications to micro-services
- **Example**: move app to Serverless architecture, use AWS S3 to store data
# AWS Application Discovery Service
- plan migration projects by gathering information about on-premises data centers
- scan servers and gather information about server utilization data and dependency mapping which are important for migrations to understand how and what to migrate first
- Two types of migration that can be done:
	- **Agentless Discovery (AWS Agentless Discovery Connector)**
		> gives information around VMs, configuration, and performance history such as CPU, memory and disk usage

	- **Agent-based Discovery (AWS Application Discovery Agent)**
		- gives more updates and information from VMs, such as system configuration, system performance, running processes and details of the network connections between systems
- resulting data can be viewed within AWS Migration Hub
# AWS Application Migration Service (MGN)
- lift-and-shift (rehost) solution which simplify migrating applications to AWS
- convert physical, virtual and cloud-based servers to run natively on AWS
- supports wide range of platforms, OS and databases
- minimal downtime
- reduced costs
![[Pasted image 20250227120645.png]]
# AWS Migration Evaluator
- helps build a data driven business case for migration to AWS
- provides clear baseline of what organization is running today
- Install Agentless Collector to conduct broad-based discovery of all our infrastructure
- take snapshot of on-premises foot-print, server dependencies, ...
- analyze current state, define target state, then develop migration plan
![[Pasted image 20250227121227.png]]
# AWS Migration Hub
- central location to collect server and application inventory data for assessment, planning and tracking of migrations to AWS
- helps accelerate migration to AWS
- automate lift-and-shift
- **AWS Migration Hub Orchestrator**
	> provides pre-built templates to save time and effort migrating enterprise apps (e.g. SAP, Microsoft SQL Server, ...)
- supports migration status updates from Application Migration Service (MGN) and Database Migration Service (DMS)
![[Pasted image 20250227134528.png]]
# AWS Fault Injection Simulator (FIS)
- fully managed service for running fault injection experiments on AWS workloads
- Based on [[Chaos Engineering]]
- helps you uncover hidden bugs and performance bottlenecks
- supports the following AWS services: EC2, ECS, EKS, RDS, ...
- can use pre-built templates that generate the desired disruptions
![[Pasted image 20250227135456.png]]
# AWS Step Functions
- way to build serverless visual workflow to orchestrate Lambda functions
- design a graph and at each step, define what to do next in case of success or failure.
- **Features**:sequence, parallel, conditions, timeouts, error handling, ...
- can integrate with EC2, ECS, on-premises servers, API Gateway, SQS queues, etc...
- possibility of implementing human approval feature
- **Use cases:** order fulfillment, data processing, web application, any workflow
![[Pasted image 20250227135904.png]]
# AWS Ground Station
- fully managed service that lets us control satellite communications, process data and scale satellite operations
- provides a global network of satellite ground stations near AWS regions
- allows to download satellite data to AWS VPC within seconds
- send satellite data to S3 or EC2 instance
- **Use cases**: weather forecasting, surface imaging, communications, video broadcasts
![[Pasted image 20250227140334.png]]
# Amazon Pinpoint
- scalable **2-way (outbound/inbound)** marketing communications service
- supports email, SMS, push, voice and in-app messaging
- ability to segment and personalize messages with the right content to customers
- possibility to receive replies
- scales to billions of messages per day
- **Use cases**: run campaigns by sending marketing, bulk, transactional SMS messages
- **Versus Amazon SNS or Amazon SES**
	- In SNS & SES, we manage each message's audience, content and delivery schedule
	- In Pinpoint, we create message templates, delivery schedules, highly-targeted segments and full campaigns
![[Pasted image 20250227140829.png]]
