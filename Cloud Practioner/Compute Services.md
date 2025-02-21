# ECS
- ECS = Elastic Container Service
- Launch [[Docker]] containers on AWS
- need to provision & maintain the infrastructure ([[EC2]] instances)
- AWS takes care of starting / stopping container
- can be integrated with Application Load Balancer
![[Pasted image 20250217143901.png]] 

# Fargate
- launch [[Docker]] containers on AWS
- do not need to provision the infrastructure (no [[EC2]] instances to manage) => simpler
- serverless
- AWS runs containers based on the CPU/RAM needed
![[Pasted image 20250217144101.png]] 

# ECR
- Elastic Container Registry
- Private [[Docker]] Registry on AWS
- store [[Docker]] images so they can be run by [[#ECS]] or [[#Fargate]]
![[Pasted image 20250217144254.png]] 

# Amazon EKS
- EKS = Elastic Kubernetes Service
- allows to launch managed [[Kubernetes]] clusters on AWS
- Containers can be hosted on:
	- [[EC2]] instances
	- [[#Fargate]]
![[Pasted image 20250217144736.png]] 
- [[Kubernetes]] is cloud agnostic => can be used in any cloud - Azure, GCP, ...

# AWS Lambda
![[Pasted image 20250217163300.png]] 

## Benefits
- Easy Pricing
	- pay per request and compute time
	- Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time
- Integrated with whole AWS suite of services
- **Event-Driven** - functions get invoked by AWS when needed
- Supports many programming languages
	- Node.js (JavaScript)
	- Python
	- Java
	- C# (.Net Core) / Powershell
	- Ruby
	- Custom Runtime API (community supported, Rust or Golang)
- Easy monitoring through AWS CloudWatch
- Easy to get more resources per function (up to 10GB of RAM)
- Increasing RAM will also improve CPU and Network quality
- Lambda Container Image
	- container image must implement Lambda Runtime API
	- ECS / Fargate is preferred for running Docker images
## Example
### Serverless Thumbnail creation
![[Pasted image 20250217163916.png]] 

### Serverless CRON Job
- Cron allows to define a schedule such as every hour, every Monday, ...
- based on the schedule, it runs a script
- By default: run on Linux AMI
- In AWS, use CloudWatch Events EventBridge
![[Pasted image 20250217164159.png]] 

## Pricing
[AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/)

# Amazon API Gateway
 - **Example**: building a serverless API
 - fully managed service to easily create, publish, maintain, monitor and secure APIs
 - serverless and scalable
 - supports RESTful  and WebSocket APIs
 - support for security, user authentication, API throttling, API keys, monitoring...
 ![[Pasted image 20250218110545.png]]
# AWS Batch
- fully managed batch processing at any scale
- efficiently run 100,000s of computing batch jobs
- Batch dynamically launches EC2 instances or Spot Instances
- provisions the right amount of compute / memory
- submit or schedule batch jobs and AWS handles the rest
- Batch jobs are [[Docker]] images and run on [[#ECS]] 
- helpful for cost optimizations and focusing less on the infrastructure

#### Example
![[Pasted image 20250218111044.png]]

### Batch vs Lambda

| **Lambda**                   | **Batch**                                                                                   |
| ---------------------------- | ------------------------------------------------------------------------------------------- |
| Time limit                   | no time limit                                                                               |
| limited runtimes             | any runtime as long as packed as [[Docker]] image                                           |
| limited temporary disk space | Rely on [[EC2#EBS Volume\|EBS]] / [[EC2#EC2 Instance Store\|Instance Store]] for disk space |
| [[Serverless]]               | managed service that relies on [[EC2]]                                                      |
# Amazon Lightsail
- virtual servers, storage, databases and networking
- Low & predictable pricing
- simpler alternative to [[EC2]], [[Databases & Analytics#Amazon RDS|RDS]], [[Elastic Load Balancing & Auto Scaling Groups#Why use Elastic Load Balancer?|ELB]], [[EC2#EBS Volume|EBS]], Route 53...
- for people with little cloud experience
	- don't want to learn how the services work in detail
- can setup monitoring and notification of Lightsail resorces
- Use Cases:
	- Simple web apps (has templates for LAMP, Nginx, MEAN, Node.js...)
	- Websites (templates for WordPress, Magento, Plesk, Joomla)
	- Dev / Test environment
- high availability but no auto-scaling, limited AWS integrations

# Summary
![[Pasted image 20250218112018.png]]

## Lambda Summary
![[Pasted image 20250218112149.png]]