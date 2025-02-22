## IP Address
###### Elastic IP
- attach a fixed public IPv4 address to EC2 instance

# VPC & Subnets Primer
![[Pasted image 20250222093918.png]]
## VPC
private network to deploy resource (regional resource)
## Subnet
- part of VPC
- allows to partition network inside VPC (AZ resource)
- to define access to the internet and between subnets, **Route Tables** are used
## VPC Diagram
![[Pasted image 20250222094005.png]]

## Internet Gateway & Nat Gateways
- **Internet Gateway** helps VPC instances to connect to the Internet
- Public subnets have route to the internet gateway
- NAT Gateways (AWS-managed) & NAT Instances (self-managed) allows instances in Private Subnets to access the internet while remaining private
![[Pasted image 20250222094247.png]] 
# Network ACL & Security Groups
## NACL (Network ACL)
- firewall at subnet level
- can have ALLOW and DENY rules
- rules only include IP addresses
## Security Groups
- virtual firewall at resource/instance level
- can only have ALLOW rules
- rules include IP addresses and other security groups
![[Pasted image 20250222100856.png]] 
## Difference
![[Pasted image 20250222100924.png]] 

# VPC Flow Logs
- log of all the IP traffic going into the interfaces
	- VPC Flow Logs
	- Subnet Flow Logs
	- Elastic Network Interface Flow Logs
- monitor and troubleshoot connectivity issues
	*Examples*:
	- subnets to internet
	- subnets to subnets
	- internet to subnets
- captures network information from AWS managed interfaces as well like [[Elastic Load Balancing & Auto Scaling Groups#Why use Elastic Load Balancer?|ELB]], [[Databases & Analytics#Amazon ElastiCache|ElastiCache]], [[Databases & Analytics#Amazon RDS|RDS]], [[Databases & Analytics#Amazon Aurora|Aurora]], etc...
- VPC Flow logs data can go to [[Amazon S3]], [[Cloud Monitoring#CloudWatch Logs|CloudWatch Logs]], and [[Cloud Integration#Kinesis Data Firehose|Kinesis Data Firehose]]
# VPC Peering
- connect two [[#VPC]], privately using AWS network
- make them behave as part of same network
- must **not** have overlapping CIDR (IP address range) => *cannot establish VPC Peering connection if overlap*
- not transitive => must be established for each VPC that needs to communicate with one another
	*in the diagram, VPC C and VPC B cannot communicate as they are not linked directly.* They should be linked together by another VPC Peering connection
![[Pasted image 20250222120418.png]] 
# VPC Endpoints
- allows to connect to AWS Services using a private network instead of the public www network
- provided better security and lower latency to AWS Services as request do not need to go through network hops
- ***VPC Endpoint Gateway***: [[Amazon S3]] & [[Databases & Analytics#DynamoDB|DynamoDB]]
- ***VPC Endpoint Interface***: rest of the services
![[Pasted image 20250222122024.png]] 

## AWS PrivateLink
- most secure & scalable way to expose a service to 1000s of VPCs
- allows direct and private connection between VPCs
- Does not require [[#VPC Peering]], Internet Gateway, NAT, route tables...
- internet traffic goes through private network
![[Pasted image 20250222122444.png]] 
# Site to Site VPN & Direct Connect
==for hybrid cloud==
![[Pasted image 20250222122826.png]] 
## Site to Site VPN
- connect on-premises VPN to AWS
- connection automatically encrypted
- goes over the public internet 
- To establish a connection:
	1. on premises must use a **Customer Gateway (CGW)**
	2. on AWS side, a **Virtual Private Gateway (VGW)** is needed
	![[Pasted image 20250222123701.png]]
## Direct Connect (DX)
- establish physical connection between on-premises and AWS
- connection is private, fast and secure
- goes over private network
- more expensive and takes longer to establish

# AWS Client VPN
- connect from computer using OpenVPN to private network in AWS and on-premises
- allows to connect to EC2 instances over a private IP (just as if part of private VPC network)
- goes over public internet
![[Pasted image 20250222124054.png]] 
# Transit Gateways
![[Pasted image 20250222124204.png]]
> network topology on AWS can be complicated if we have large infrastructure on AWS as shown in image above.
- to solve this, Transit Gateway service was created.
- for having a transitive peering between thousands of VPC and on-premises with a hub-and-spoke (star) connection
- one single gateway to provide this functionality
- works with [[#Direct Connect (DX)]], VPN connections
![[Pasted image 20250222124520.png]] 
# Summary
![[Pasted image 20250222124603.png]] ![[Pasted image 20250222124625.png]]
