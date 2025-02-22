# CloudWatch Metrics
- provides metrics for *every* service in AWS
- **Metric** => variable to monitor
- Metrics have timestamps
- Can create CloudWatch dashboards of metrics

##### Example: CloudWatch Billing metric
![[Pasted image 20250220160913.png]] 

## Important Metrics
- **EC2 Instances**: CPU Utilization, Status Checks, Network *(not RAM)*
	- every 5 minutes by default
	- Detailed monitoring (\$\$\$): metrics every 1 minute
- **EBS volumes**: Disk read/writes
- **S3 Buckets**: BucketSizeBytes, NumberOfObjects, AllRequests
- **Billing**: Total estimated charge
- **Service Limits**: how much service API is being used
- **Custom metrics**: push you own metrics

# CloudWatch Alarms
- used to trigger notifications for any metric *after threshold*
- Alarm actions...
	- **Auto Scaling**: increase or decrease [[EC2]] instance count
	- **EC2 Actions**: stop, terminate, reboot or recover an [[EC2]] instance
	- **SNS notifications**: send a notification to an [[Cloud Integration#Amazon SNS|SNS]] topic
- Various options (sampling, &, max, min, etc...)
- can choose the period on which to evaluate an alarm
- *Example: create a **billing alarm** on the CloudWatch Billing metric*
- **Alarm States**: OK, INSUFFICIENT_DATA, ALARM

# CloudWatch Logs
- collect log from:
	- [[Deployments & Managing Infrastructure#AWS Elastic Beanstalk|Elastic Beanstalk]]: logs from application
	- [[Compute Services#ECS|ECS]]: from containers
	- [[Compute Services#AWS Lambda|Lambda]]: from function logs
	- CloudTrail based on filter
	- CloudWatch log agents: on [[EC2]] machines or on-premises servers
	- [[AWS Global Infrastructure#Global DNS ==Route 53==|Route 53]]: log [[DNS]] queries
- enables real-time monitoring of logs
- adjustable retention

## CloudWatch Logs for EC2
- by default, [[EC2]] does not send logs to CloudWatch
- need to run a CloudWatch log agent on EC2 to push the log files
- make sure [[EC2]] IAM permissions are correct
- log agent can be setup on-premises as well
![[Pasted image 20250221104903.png]]
# Amazon EventBridge
- can react to events happening within AWS accounts
- one use case is to schedule Cron jobs => scripts scheduled on a regular basis
	![[Pasted image 20250221105522.png]]
- can also react to a service doing something => Event Pattern
	![[Pasted image 20250221105543.png]]
- ![[Pasted image 20250221105641.png]]
- **Default Event Bus** => events from within AWS services or schedules
	![[Pasted image 20250221105812.png]]
- **Partner Event Bus** => events from partners of AWS
	![[Pasted image 20250221105825.png]]
- **Custom Event Bus** => own custom applications that can send own custom events
	![[Pasted image 20250221105924.png]] 
- **Schema Registry**: model event schema to look at data types and alike
- can archive events sent to an event bus (set period or infinite)
- can replay archived events
# AWS CloudTrail
- provides governance, compliance and audit for AWS account
- enabled by default
- gets an history of events/API calls made within AWS account by:
	- Console
	- SDK
	- CLI
	- AWS Services
- can put logs from CloudTrail into [[#CloudWatch Logs]] or [[Amazon S3]]
- **trail can be applied to All Regions *(default)* or a single Region**
- ==if resource is deleted, investigate CloudTrail first! ==
## Diagram
![[Pasted image 20250221110815.png]]

# AWS X-Ray
- tradition debugging method:
	- test locally
	- add log statements everywhere
	- redeploy in production
- the problem is that log analysis is hard when log formats differ across applications
- no common view of entire architecture
- ==the problems are solved by X-Ray==
- X-Ray allows to do tracing and visual analysis of application
![[Pasted image 20250222090006.png]] 

## Advantages
- troubleshooting performance
- understanding dependencies in microservice architecture
- pinpoint service issue with tracing
- review request behavior
- find errors and exceptions
- know if we are meeting time SLA
- where am i throttled?
- impacted users identification

# Amazon CodeGuru
- ML-powered service
- automated code reviews and application performance recommendations
- Two functionalities:
	- **CodeGuru Reviewer**: automated code reviews for static code analysis (development)
	- **CodeGuru Profiler**: recommendations about app performance during runtime (production)
![[Pasted image 20250222090511.png]] 
## CodeGuru Reviewer
- looks at commits and tells lines of code that might be incorrect
- identify critical issues, security vulnerabilities and hard-to-find bugs
- *Example*: common coding best practices, resource leaks, security detection, input validation
- user ML and automated reasoning
- Supports Java and Python
- Integrates with GitHub, Bitbucket and AWS CodeCommit
## CodeGuru Profiler
- for production or pre-prod
- helps understand runtime behaviour
- *Example*: identify if application is consuming excessive CPU capacity on a logging routine
- Features:
	- identify and remove code inefficiencies
	- improve application performance
	- decrease compute costs
	- provides heap summary
	- anomaly detection
- supports apps running on AWS or on-premises
# AWS Health Dashboard
## Service History
- shows all regions, all services health
- shows historical information for each day
## Your Account
- provides alerts and remediation guidance when AWS is experiencing events that might impact us
- ==Service Health Dashboards displays general status of AWS services, Account Health Dashboard gives a personalized view into the performance and availability of the AWS services underlying our AWS resources==
- displays relevant and timely information to help manage events in progress and provide proactive notification to help plan for scheduled activities
- can aggregate data from an entire AWS Organization
- global service
# Summary
![[Pasted image 20250222091708.png]] 

