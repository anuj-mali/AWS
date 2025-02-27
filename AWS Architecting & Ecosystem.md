# Well Architected Framework
## General Guiding Principles
- stop guessing capacity needs
	> instead use auto scaling based on the actual demand on the system is going to be
- Test systems at production scale
- automate to make architectural experimentation easier
	> CloudFormation - IaC
	> PaaS - Beanstalk
- allow for evolutionary architectures
	> design based on changing requirements
- Drive architectures using data
	> look at actual usage, patterns and queries.
	> Drive the architecture and use the right services based on data
- improve through game days
	> simulate applications for flash sale days which stress the system.
## AWS Cloud Best Practices - Design Principles
- **Scalability**: vertical & horizontal
- **Disposable Resources**: servers should be disposable & easily configured
- **Automation**: serverless, IaaS, Auto Scaling ...
- **Loose Coupling**
	- *Monolith* are applications that do more and more over time, become bigger
	- break it down into smaller, loosely coupled components
	- change or failure in one component should not cascade to other components
- **Services, not Servers**
	- Do not just use EC2
	- use managed services, databases, serverless, etc!
## Well Architected Framework 6 Pillars
==They are not something to balance, or trade-offs, they're a synergy==
### Operational Excellence
- ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures
#### Design Principles
- **Perform operations as code**
	> Infrastructure as Code
- **Make frequent, small, reversible changes**
	> so that in case of any failure, changes can be reversed easily
- **Refine operations procedures frequently**
	> also ensure that team members re familiar with it
- **Anticipate failure**
- **Learn from all operational failures**
- **Use managed services**
	> reduce operational burden
- **implement observability for actionable insights**
	> performance, reliability, cost...
#### AWS Services
- Prepare
	- CloudFormation
	- Config
- Operate
	- CloudFormation
	- Config
	- CloudTrail
	- CloudWatch
	- X-Ray
- Evolve
	- CloudFormation
	- CodeBuild
	- CodeCommit
	- CodeDeploy
	- CodePipeline
### Security
- ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies
#### Design Principles
- **Implement a strong identity foundation**
	> Centralize privilege management and reduce (or even eliminate) reliance on long-term credentials
	> Principle of least privilege
	> IAM
- **Enable traceability**
	> integrate logs and metrics with system to automatically respond and take action
- **Apply security at all layers**
	> edge network, VPC, subnet, load balancer, every instance, OS and application
- **Automate security best practices**
	> security is mostly done well when it's automated
- **Protect data in transit and at rest**
	> Encryption, tokenization, and access control
- **Keep people away from data**
	> reduce or eliminate the need for direct access or manual processing of data
- **Prepare for security events**
	> run incident response simulations
	> use tools with automation to increase speed for detection, investigation and recovery
#### AWS Services
- Identity and Access Management
	- IAM
	- AWS STS
	- MFA Token
	- AWS Organizations
- Detective Controls
	- Config
	- CloudTrail
	- CloudWatch
- Infrastructure Protection
	- CloudFront
	- VPC
	- Shield
	- WAF
	- Inspector
- Data Protection
	- KMS
	- S3
	- ELB
	- EBS
	- RDS
- Incident Response
	- IAM
	- CloudFormation
	- CloudWatch Events
### Reliability
- ability of a system to recover from infrastructure or service disruptions
- dynamically acquire computing resources to meet demand
- mitigate disruptions such as misconfigurations or transient network issues
#### Design Principles
- **Test recovery procedures**
	> use automation to simulate different failures or to recreate scenarios that led to failure before
- **Automatically recover from failure**
	> anticipate and remediate failures before they occur
- **Scale horizontally to increase aggregate system availability**
	> distribute requests across multiple, smaller resources to ensure that they don't share a common point of failure
- **Stop guessing capacity**
	> maintain the optimal level to satisfy demand without over or under provisioning
	> use Auto Scaling
- **manage change in automation**
	> use automation to make changes to infrastructure
#### AWS Services
- Foundations
	- IAM
	- VPC
	- Service Quotas
	- Trusted Advisor
- Change Management
	- Auto Scaling
	- CloudWatch
	- CloudTrail
	- Config
- Failure Management
	- Backups
	- CloudFormation
	- S3
	- S3 Glacier
	- Route 53
### Performance Efficiency
- ability to use computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technologies evolve
#### Design Principles
- **Democratize advanced technologies**
	> advance technologies become services
	> hence we can focus more on product development
- **Go global in minutes**
	> Easy deployment in multiple regions
- **Use serverless architectures**
	> avoid the burden of managing servers
- **Experiment more often**
	> easy to carry out comparative testing
- **Mechanical sympathy**
	> be aware of all AWS Services
#### AWS Services
- Selection
	- Auto Scaling
	- Lambda
	- EBS
	- S3
	- RDS
- Review
	- CloudFormation
	- AWS News Blog
- Monitoring
	- CloudWatch
	- Lambda
- Tradeoffs
	- RDS vs Aurora
	- ElastiCache vs Real time 
	- Snowball vs Direct upload
	- CloudFront vs Real time
### Cost Optimization
- ability to run systems to deliver business value at the lowest price point
#### Design Principles
- **Adopt a consumption mode**
	> Pay only for what you use
- **Measure overall efficiency**
	> use CloudWatch
- **Stop spending money on data center operations**
	> AWS does the infrastructure part and enables customers to focus on organization projects
- **Analyze and attribute expenditure**
	> accurate identification of system usage and costs
	> helps measure ROI
	> *make sure to use tags*
- **Use managed and application level services to reduce cost of ownership**
	> as managed services operate at cloud scale, they can offer a lower cost per transaction or service
#### AWS Services
- Expenditure Awareness
	- Budgets
	- Cost and Usage Report
	- Cost Explorer
	- Reserved Instance Reporting
- Cost-Effective Resources
	- Spot Instances
	- Reserved Instances
	- S3 Glacier
- Matching supply and demand
	- Auto Scaling
	- Lambda
- Optimizing Over Time
	- Trusted Advisor
	- Cost and Usage Report
	- AWS News Blog
### Sustainability
- focuses on minimizing the environmental impact of running cloud workloads
#### Design Principles
- **Understand impact**
	> establish performance indicators
	> evaluate improvements
- **Establish sustainability goals**
	> set long-term goals for each workload
	> model ROI
- **Maximize Utilization**
	> right size for each workload to maximize the energy efficiency of the underlying hardware and minimize idle resources
- **Anticipate and adopt new, more efficient hardware and software offerings**
	> and design for flexibility to adopt new technologies over time
- **Use managed services**
	> shared services reduce the amount of infrastructure
	> managed services help automate sustainability best practices as moving infrequent accessed data to cold storage and adjusting compute capacity
- **Reduce the downstream impact of cloud workloads**
	> reduce the amount of energy or resources required to use services and reduce the need for customers to upgrade their devices
#### AWS Services
- EC2 Auto Scaling, Serverless Offering
- Cost Explorer, AWS Graviton 2, EC2 T instances, Spot Instances
- EFS-IA, Amazon S3 Glacier, EBS Cold HDD volumes
- S3 Lifecycle Configurations, S3 Intelligent Tiering
- Amazon Data Lifecycle Manager
- Read Local, Write Global
	- RDS Read Replicas
	- Aurora Global DB
	- DynamoDB Global Table
	- CloudFront
## AWS Well-Architected Tool
- free tool to review architecture against 6 pillars of Well-Architected Framework and adopt architectural best practices
- How does it work?
	- Select workload and answer questions
	- review answers against the 6 pillars
	- obtain advice
		- get videos and documentations
		- generate report
		- see results in dashboard
# AWS Customer Carbon Footprint Tool
- track, measure, review and forecast the Carbon emissions generated from our AWS usage
- helps to meet sustainability goals
# AWS Cloud Adoption Framework (AWS CAF)
- e-book / whitepaper
- helps build and then execute comprehensive plan for digital transformation through innovative use of AWS
- identifies specific organizational capabilities that underpin successful cloud transformations
- groups capabilities in 6 perspectives
	- Business
	- People
	- Governance
	- Platform
	- Security
	- Operations
## CAF Perspectives and Foundational Capabilities
### Business Capabilities
#### Business Perspective
> helps ensure that our cloud investments accelerate digital transformation ambitions and business outcomes
#### People Perspective
> serves as a bridge between technology and business, accelerating the cloud journey to help organizations more rapidly evolve to a culture of continuous growth, learning and where change becomes business-as-normal with focus on culture, organizational structure, leadership and workforce
#### Governance Perspective
> helps orchestrate cloud initiatives while maximizing organizational benefits and minimizing transformation related risks

![[Pasted image 20250227162350.png]]
### Technical Capabilities
#### Platform Perspective
> helps build enterprise-grade, scalable, hybrid cloud platform
> modernize existing workloads
> implement cloud-native solutions
#### Security Perspective
> helps achieve confidentiality, integrity and availability of data and cloud workloads
#### Operations Perspective
> helps ensure that cloud services are delivered at a level that meets the needs of business

![[Pasted image 20250227162637.png]]
## Cloud Transformation Value Chain
![[Pasted image 20250227162720.png]]
## Transformation Domains
- **Technology**
	> using cloud to migrate and modernize legacy infrastructure, applications, data and analytics platform...
- **Process**
	> digitizing, automating and optimizing business operations
	> leveraging new data and analytics platforms to create actionable insights
	> using ML to improve customer service experience...
- **Organization**
	> reimagining operation model
	> organizing teams around products and value streams
	> leveraging agile methods to rapidly iterate and evolve
- **Product**
	> reimagining business model by creating new value propositions (products & services) and revenue models
## Transformation Phases
- **Envision**
	> demonstrate how the Cloud will accelerate business outcomes by identifying transformation opportunities and create a foundation for digital transformation
- **Align**
	> identify capability gaps across the 6 AWS CAF Perspectives which results in an Action Plan
- **Launch**
	> build and deliver pilot initiatives in production and demonstrate incremental business value
- **Scale**
	> expand pilot initiatives to the desired scale when realizing the desired business benefits
# AWS Right Sizing
- EC2 has many instance types but choosing the most powerful instance type is not the best choice because the cloud is elastic and we can change the instance type whenever you want
- Right sizing is the process of matching instance types and sizes to workload performance and capacity requirements at the lowest possible cost
- scaling up is easy so always start small
- process of looking at deployed instances and identifying opportunities to eliminate or downsize without compromising capacity or other requirements, which results in lower costs
- Important to right size in
	- before cloud migration
	- continuously after cloud onboarding process
- CloudWatch, Cost Explorer, Trusted Advisor, 3${^{rd}}$ party tools can help
# AWS Ecosystem
##### Free Resources
- [AWS Blogs](https://aws.amazon.com/blogs/aws/)
- [AWS re:Post](https://repost.aws/)
- [AWS Whitepaper & Guides](https://aws.amazon.com/whitepapers)
- [AWS Solutions Library](https://aws.amazon.com/solutions/)
	- Vetted Technology Solutions for AWS Cloud
## AWS Marketplace
- digital catalog with thousands of software listings from independent software vendors
- Example:
	- Custom AMI
	- CloudFormation templates
	- SaaS
	- Containers
- if bought through Marketplace, it goes to our AWS bill
- can sell our own solutions
## AWS Training
- AWS Digital (online)
- Classroom Training (in-person or virtual)
- AWS Private Training (for organization)
- Training and Certification for U.S Government
- Training and Certification for Enterprise
- AWS Academy: helps universities teach AWS
# AWS Professional Services & Partner Network
- AWS Professional Services organization is a global team of experts
- work alongside our team and a chosen member of the APN
- APN = group of people that AWS knows are good with the Cloud
- **APN Technology Partners**
	> providing hardware, connectivity and software
 - **APN Consulting Partners**
	 > professional services firm to help build on AWS
 - **APN Training Partners**
	 > find who can help us learn AWS
- **AWS Competency Program**
	> AWS Competencies are granted to APN Partners who have demonstrated technical proficiency and proven customer success in specialized solution areas
- **AWS Navigate Program**
	> help Partners become better Partners
# AWS IQ
- quickly find professional help for AWS projects
- Engage and pay AWS Certified 3$^{rd}$ party experts for on-demand project work
- video-conferencing, contract management, secure collaboration, integrated billing
- **For Customers**
	![[Pasted image 20250227203341.png]]
- **For Experts**
	![[Pasted image 20250227203436.png]]
# AWS re:Post
- AWS-managed Q&A service offering crowd-sourced, expert-reviewed answers to technical questions about AWS
- part of AWS Free Tier
- Community members can earn reputation points to build up their community expert status by providing accepted answers and reviewing answers from other users
- **Questions from AWS Premium Support customers that do not receive a response from the community are passed on to AWS Support engineers**
- no intended to be used for questions that are time-sensitive or involve any proprietary information
## Knowledge Center
![[Pasted image 20250227203751.png]]
# AWS Managed Services (AMS)
- a team of people that provides infrastructure and application support on AWS
- **AMS offers a team of AWS experts** who manage and operate our infrastructure for security, reliability and availability
- helps organizations offload routine management tasks and focus on business activities
- fully managed service, so AWS handles common activities such as change requests, monitoring, patch management, security and backup services
- implements best practices and maintains AWS infrastructure to reduce operational overhead and risk
- 24/365
![[Pasted image 20250227204112.png]]