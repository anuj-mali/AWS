## Scalability & High Availability
### Scalability
> application / system can handle greater loads by adapting

#### Two Kinds
- Vertical Scalability
	- Increase the size of the instance
	- Common for non distributed system - Database
	- limit to vertical scale (hardware limit)
- Horizontal Scalability (= elasticity)
	- increase number of instances / system for the application
		- Auto scaling group
		- load balancer
	- this implies distributed systems
	- common for web / modern apps
	- easy to scale horizontally

### High Availability
- goes together with horizontal scaling
- it means running app / system in at least 2 AZs
- goal is to survive a data center loss

### Scalability vs Elasticity (vs Agility)
- **Scalability** : ability to accommodate a larger load by making the hardware stronger or adding nodes
- **Elasticity** : once a system is scalable, elasticity means that there will be some auto-scaling.
- **Agility** : new IT resources are only a click away.

## Load Balancing
- load balancers are servers that forward internet traffic to multiple servers downstream
![[Pasted image 20250215102656.png]]

#### Why use one?
- spread traffic across multiple downstream instances
- expose single point of access (DNS)
- seamlessly handle failures of downstream instances
- do regular health checks of instances
- provide SSL termination (HTTPS)
- high availability across zones

#### Why use Elastic Load Balancer?
- managed load balancer
- costs less to setup own load balancer but takes more effort
##### Kinds of Load Balancer
###### Application Load Balancer 
- (HTTP/HTTPS) 
- Layer 7
###### Network Load Balancer
- (ultra high performance, allows for TCP, UDP) 
- Layer 4
###### Gateway Load Balancer 
- Layer 3
![[Pasted image 20250215103351.png]]

### Auto Scaling Group
- In cloud, you can easily create and remove servers
- The goal of ASG is
	- scale out to match the increased load
	- scale in to match the decreased load
	- ensure min and max number of machines running
	- automatically register new instances to a load balancer
	- replace unhealthy instances
- Cost savings: only run at optimal capacity
![[Pasted image 20250215130304.png]]
![[Pasted image 20250215130335.png]]

#### Scaling Strategies
1. Manual Scaling : Update the size manually
2. Dynamic Scaling: Respond to changes on demand
	- Simple / Step scaling
		- when CloudWatch alarm is triggered (*example: CPU > 70%*), then add 2 units
		- When CloudWatch alarm is triggered (*example: CPU < 30%*), then remove 1
	- Target Tracking Scaling
		- *Example: I want the average ASG CPU to stay around 40%*
	- Scheduled Scaling
		- Anticipate a scaling based on known usage patterns
		- *Example: increase the min capacity to 10 at 5pm on Fridays*
	- Predictive Scaling
		- Uses ML to predict future traffic ahead of time
		- useful when load has predictable time-based patterns