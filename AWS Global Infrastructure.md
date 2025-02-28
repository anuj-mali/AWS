#### Why make a application global?
- global app => deployed in multiple geographical locations
- On AWS => Regions and/or Edge Locations
- Decreased Latency
	- apps deployed closer = decrease latency, better experience
- Disaster Recovery (DR)
	- if an AWS region goes down
	- can fail-over to another region
	- increase availability of application
- Attack Protection
	- distributed global infra is harder to attack

# Global AWS Infrastructure
**Reference**: [Global Infrastructure](https://infrastructure.aws)
##### Region
- for deploying applications and infrastructure
- made up of multiple [[#Availability Zones]]
##### Availability Zones
- made of multiple data centers
- redundant power, networking and connectivity
- isolated from each other
- connected with high bandwidth, ultra-low latency networking
##### Edge Locations
- Points of Presence
- for content delivery as close as possible to users
## Global Applications in AWS
### Global DNS: ==Route 53==
- great to route users to the closest deployment with least latency
- managed [[DNS]]
- most common records:
	- www.google.com => 12.34.56.78 == A record (IPv4)
	- www.google.com => 2001:0db8::7334 == AAAA record (IPv6)
	- search.google.com => www.google.com == CNAME (Canonical Name): hostname to hostname
	- example.com => AWS Resource == Alias
#### Diagram for A Record
![[Pasted image 20250218154643.png]] 

#### Routing Policies
##### Simple Routing Policy
![[Pasted image 20250218154806.png]] 
##### Weighted Routing Policy
![[Pasted image 20250218154826.png]] 
- redirects traffic based on the weight
- some kind of load balancing
- can use health checks
##### Latency Routing Policy
![[Pasted image 20250218155010.png]] 
- minimize the latency by connecting users to closest server based on latency
##### Failover Routing Policy
![[Pasted image 20250218155136.png]] 
- if primary instance fails, redirects to Failover
- helps with Disaster Recovery


### Global Content Delivery Network (CDN): ==CloudFront==
- replicate part of application / cache to AWS [[#Edge Locations]] - decrease latency
- cache common requests - improved user exp and decrease latency
- DDoS protection *(because worldwide), integration with Shield, AWS Web Application Firewall*
#### Origins
- S3 Bucket
	- for distributing files and caching them at the edge
	- enhanced security with CloudFront Origin Access Control (OAC)
	- CloudFront can be used as an ingress (to upload files to S3)
- Custom Origin (HTTP)
	- [[Elastic Load Balancing & Auto Scaling Groups#Application Load Balancer|Application Load Balancer]]
	- [[EC2|EC2 Instance]]
	- [[Amazon S3#Amazon S3 - Static Website Hosting|Static Website]]
	- any HTTP backend
#### CloudFront at a high level
![[Pasted image 20250219112019.png]] 

#### CloudFront S3 as an Origin
![[Pasted image 20250219112228.png]] 

#### CloudFront vs S3 Cross Region Replication
- CloudFront
	- Global Edge network
	- Files are cached for TTL (Time To Live)
	- great for static content
- S3 Cross Region Replication
	- must be setup for each region
	- updated near real-time
	- read only
	- great for dynamic content that needs to be available at low-latency in few regions

### ==S3 Transfer Acceleration==
- accelerate global uploads & downloads into [[Amazon S3]]
- increase transfer speed by transferring file to [[#Edge Locations]] which will forward the date into the [[Amazon S3#Buckets|S3 Bucket]] in the target region
![[Pasted image 20250219114544.png]]
### ==AWS Global Accelerator==
- improve global application availability and performance using AWS global network
- leverage the AWS internal network to optimize the route to application (*60% improvement*)
- 2 static Anycast IP are created for application and traffic is sent through [[#Edge Locations]]
![[Pasted image 20250219120251.png]]
![[Pasted image 20250219120353.png]]

#### AWS Global Accelerator vs CloudFront
- both use AWS global network and its [[#Edge Locations]]
- both integrate with AWS Shield for DDoS protection
- [[#Global Content Delivery Network (CDN) ==CloudFront==|CloudFront - CDN]]
	- content is served at the edge
	- improves performance for cacheable content
- [[#==AWS Global Accelerator==|Global Accelerator]]
	- no caching, proxy packets at the edge to applications running in one or more AWS Regions
	- improves performance for a wide range of apps over TCP or UDP
	- good for HTTP use cases that require static IP addresses
	- good for HTTP use cases that require deterministic, fast region failover

### AWS Outposts
> **server racks** that offer the same AWS infrastructure, services, APIs and tools to build own applications on on-premises similarly to the cloud
- business that use [[Cloud Computing#Hybrid Cloud|Hybrid Cloud]]
	- Two ways of dealing with IT systems:
		- One for AWS cloud (using console, CLI and APIs)
		- One for on-premises infrastructure
- AWS will setup and manage "Outposts Racks" within on-premises infrastructure and allows to leverage AWS services on-premises
- way to extend the cloud directly onto own on-premises system
- ==***the customer is responsible for Outposts Rack physical security***==
![[Pasted image 20250219135015.png]] 

#### Benefits
- low-latency access to on-premises system
- local data processing
- data residency => data lives within on-premises data centers
- easy migration from on-premises to the cloud
- fully managed service
### AWS WaveLength
> **WaveLength Zones** are infrastructure deployments embedded within the telecommunications providers' datacenters at the edge of 5G networks
- brings AWS services to the edge of 5G networks
- Example: [[EC2]], [[EC2#EBS Volume|EBS]], VPC...
![[Pasted image 20250219141051.png]]  
- Ultra low latency application through 5G networks
- traffic doesn't leave the Communication Service Provider's (CSP) network
- High bandwidth and secure connection to the parent [[#Region]]
- no additional charges or service agreements
- Use Cases
	- Smart cities
	- ML-assisted diagnostics
	- Connected Vehicles
	- Interactive Live Video Streams
	- AR/VR
	- Real-time gaming...
### AWS Local Zones
- places AWS compute, storage, database, and other selected AWS services closer to end users to run latency-sensitive applications
- **"Extension of AWS Region"** - Extend VPC to more locations
- Compatible with [[EC2]], [[Databases & Analytics#Amazon RDS|RDS]], [[Compute Services#ECS|ECS]], [[EC2#EBS Volume|EBS]], [[Databases & Analytics#Amazon ElastiCache|ElastiCache]], Direct Connect...
- Example:
	- **AWS Region**: N. Virginia (us-east-1)
	- **AWS Local Zones**: Boston, Chicago, Dallas, Houston, Miami,...
![[Pasted image 20250219141910.png]]

## Global Applications Architecture
![[Pasted image 20250219142535.png]]![[Pasted image 20250219142725.png]] 
# Summary
![[Pasted image 20250219142822.png]]
![[Pasted image 20250219142850.png]]