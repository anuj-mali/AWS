# CloudFormation
- declarative way of outlining AWS infrastructure, for any resources (most are supported)
- Infrastructure as Code (IaC)
- For example: within a CloudFormation template:
	- I want a security group
	- I want two EC2 instances using this security group
	- I want an S3 bucket
	- I want a [[Elastic Load Balancing & Auto Scaling Groups#Load Balancing|Load Balancer (ELB)]] in front of these machines
- Then CloudFormation creates these for us, in the order and configuration we specify
- define in YAML or JSON format

## Benefits
- Infrastructure as Code
	- No resources are manually created
	- changes to the infrastructure are reviewed through code
- Cost
	- each resources within the stack is tagged with an identifier
	- estimate the costs of resources using CloudFormation template
	- savings strategy: *Example* => cloud automate deletion of templates at 5 PM and recreated at 8 AM
- Productivity
	- ability to destroy and re-create an infrastructure on the cloud
	- automated generation of Diagram for templates
	- Declarative programming
- Don't re-invent the wheel
	- leverage existing templates on web
	- leverage the documentation
- Supports (almost) all AWS resources
	- can use *custom resources* for resources that are not supported

## CloudFormation + Infrastructure Composer
![[Pasted image 20250218114417.png]] 

# AWS Cloud Development Kit (CDK)
- define cloud infrastructure using a familiar programming language:
	- JavaScript / TypeScript
	- Python
	- Java
	- .NET
- code is *compiled* into [[#CloudFormation]] template (JSON/YAML)
- so we can deploy infrastructure and application runtime code together
	- great for [[Compute Services#AWS Lambda|Lambda]] functions
	- Great for [[Docker]] containers in [[Compute Services#ECS|ECS]] / [[Compute Services#Amazon EKS|EKS]]
![[Pasted image 20250218120426.png]] 

#### Example
![[Pasted image 20250218120512.png]]

# AWS Elastic Beanstalk
## Typical architecture: Web App 3-tier
![[Pasted image 20250218120936.png]] 

## Overview
- managed service
	- instance configuration / OS
	- Deployment strategy is configurable
	- capacity provisioning
	- load balancing & auto scaling
	- application health-monitoring and responsiveness
- developer centric view of deploying application on AWS
- just the application code is responsibility of the developer
- Uses various components [[EC2]], [[Elastic Load Balancing & Auto Scaling Groups#Auto Scaling Group|ASG]], [[Elastic Load Balancing & Auto Scaling Groups#Why use Elastic Load Balancer?|ELB]], [[Databases & Analytics#Amazon RDS|RDS]], etc...
- all in one view
- full control over the configuration
- PaaS
- is free but need to pay for underlying instances
- Support for many platforms:
	- Go
	- Java SE
	- Java with Tomcat
	- Node.js
	- .NET on Windows Server with IIS
	- PHP
	- Python
	- Ruby
	- Packer Builder
	- Single Container Docker
	- Multi-Container Docker
	- Preconfigured Docker

## Three Architecture Models
- Single Instance Deployment: good for dev
- LB + ASG: for production or pre-production web apps
- ASG only: for non-web apps in production

## Health Monitoring
- Health agent pushes metrics to CloudWatch
- Checks for app health, publishes health events

# AWS CodeDeploy
- automatic deployment
- Works with EC2 instances
- Works with On-Premises Servers
- *Hybrid* Service
- Servers / Instances must be provisioned and configured ahead of time with CodeDeploy Agent

# AWS CodeCommit
- discontinued for new users
- AWS alternative for GitHub
- Benefits
	- fully managed
	- scalable and highly available
	- private, secured, integrated with AWS

# AWS CodeBuild
- code building service
- compiles source code, run tests and produces packages that are ready to be deployed
![[Pasted image 20250218144939.png]] 
- Benefits
	- fully managed
	- serverless
	- continuously scalable and highly available
	- secure
	- pay as you go pricing - only pay for build time
# AWS CodePipeline
- orchestrate different sets to have code automatically pushed to production
	- code=>build=>test=>Provision=>Deploy
	- Basis of CI/CD
![[Pasted image 20250218145233.png]] 
- Benefits
	- fully managed
	- compatible with [[#AWS CodeCommit]], [[#AWS CodeBuild]], [[#AWS CodeDeploy]], [[#AWS Elastic Beanstalk]], [[#CloudFormation]], GitHub and custom plugins
	- fast delivery & rapid updates

# AWS CodeArtifact
- software packages depend on each other to be built (*code dependencies*)
- **Artifact management** = store and retrieve dependencies
- CodeArtifact = secure, scalable and cost-effective artifact management
- Works with common dependency management tools:
	- Maven
	- Gradle
	- npm
	- yarn
	- twine
	- pip
	- NuGet
 - Devs and [[#AWS CodeBuild]] can directly retrieve dependencies from it
# AWS Systems Manager (SSM)
- helps to manage fleet of EC2 and On-Premises systems at scale
- Hybrid AWS Service
- get operational insights about state of infra
- suite of 10+ products
	- Some features
		- Patching automation for enhanced compliance
		- run commands across an entire fleet of servers
		- store parameter configuration with SSM Parameter Store
- Works with Linux, Windows, MacOS and Raspberry Pi OS (Raspbian)

## How SSM works
- need to install SSM agent on the system
- installed by default on Amazon Linux AMI & some Ubuntu AMI
- if instance can't be controlled by SSM, probably an issue with SSM agent
- can run commands, patch & configure our servers
![[Pasted image 20250218150617.png]]
## SSM Session Manager
- allows to start secure shell on EC2 and On-Premises servers
- No SSH access, bastion hosts or SSH keys required
- No port 22 needed *(better security)*
- supports Linux, Windows and MacOS
- send session log data to S3 or CloudWatch logs
![[Pasted image 20250218150823.png]] 

## Systems Manager Parameter Store
- secure storage for configuration and secrets
- API keys, passwords, configuration...
- serverless, scalable, durable, easy SDK
- control access permissions using IAM
- Version tracking
- encryption (optional)
![[Pasted image 20250218151432.png]] 

# Summary
## Deployment Services
![[Pasted image 20250218151713.png]] 

## Developer Services
![[Pasted image 20250218151803.png]]