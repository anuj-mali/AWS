#ec2 #storage
> An EBS (Elastic Block Store) volume is a network drive that can be attached to instances
- Can persist data even after instance is terminated
- Bound to specific AZ
- **Analogy**: network USB Stick
- Network Drive
	- there might be a bit of latency during communication
	- can be detached from one EC2 instance and attached to another 
- Can use snapshots to move volume across AZ
- Need to provision capacity (size in GB, and IOPS) in advance
	- Can increase capacity over time
## EBS Snapshots
- backup at a point in time
- not necessary to detach but recommended
## Features
- EBS Snapshot Archive
	- Move to `archive tier` that is 75% cheaper
	- Takes 24 to 72 hours to restore from archive
- Recycle Bin for Snapshots
	- Setup rules to retain deleted snapshots so as to recover later
	- Specify retention (from 1 day to 1 year)