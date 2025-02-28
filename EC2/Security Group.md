#ec2 #security
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

## Referencing other security groups
![[Pasted image 20250214140802.png]]

Since *group 1* and *group 2* are attached, the EC2 instances can connect directly without thinking about the IP address.

## Ports to know
| Port | Protocol                      |
| ---- | ----------------------------- |
| 21   | FTP                           |
| 22   | SSH                           |
| 22   | SFTP *(Using SSH)*            |
| 80   | HTTP                          |
| 443  | HTTPS                         |
| 3389 | RDP (Remote Desktop Protocol) |

