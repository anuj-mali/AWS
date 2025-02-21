- when multiple applications are deployed, they might to need to communicate with one another
- Two patterns of application communication
	- ###### Synchronous communication
		- application to application
		![[Pasted image 20250219143921.png]]
		- problematic if sudden spikes in traffic
	- Asynchronous communication
		- event based
		- application to queue to application
		- decoupled
			- [[#SQS]]: queue model
			- [[#SNS]]: pub/sub model
			- [[#Kinesis]]: real-time data streaming model
		- services can scale independently from application
		![[Pasted image 20250219143932.png]]

# Amazon SQS
- Simple Queue Service
![[Pasted image 20250219160548.png]]

- Fully managed service (serverless)
- ==used to decouple applications==
- scales from 1 message per second to 10,000s per second
- Default retention of messages: 4 days, maximum of 14 days
- no limit on queue size
- messages are deleted after read by consumers
- Low latency
- consumers share work to read messages & scale horizontally
### Decouple between Application Tiers
![[Pasted image 20250219161120.png]]

## FIFO Queues
- processed in order by consumer
![[Pasted image 20250219161229.png]]

# Amazon Kinesis
- ==for exam== **Kinesis** => real-time big data streaming
- managed service to collect, process, and analyze real-time streaming data at any scale

#### Kinesis Data Streams
> low latency streaming to ingest data at scale from hundreds of thousands of sources
#### Kinesis Data Firehose
> loads streams into [[Amazon S3]], [[Databases & Analytics#Redshift|Redshift]], ElasticSearch, etc...
#### Kinesis Data Analytics
> perform real-time analytics on streams using SQL
#### Kinesis Video Streams
> monitor real-time video streams for analytics or ML

## High Level Overview
![[Pasted image 20250220120224.png]]

# Amazon SNS
![[Pasted image 20250220135412.png]] 
- SNS => Simple Notification Service
- "event publishers" only sends message to one SNS topic
- many "event subscribers" can listen to SNS topic notifications
- each subscriber gets all the messages
- up to 12.5 millions subscriptions per topic and soft limit of 100,000 topics
![[Pasted image 20250220135808.png]] 

# Amazon MQ
> managed message broker service for
> RabbitMQ
> ActiveMQ
- [[#Amazon SQS]], [[#Amazon SNS]] = proprietary protocols from AWS
- Traditional applications might use open protocols such as: MQTT, AMQP, STOMP, Openwire, WSS
- When migrating to cloud, instead of changing the application to use [[#Amazon SQS]] and [[#Amazon SNS]], Amazon MQ can be used.
- doesn't scale as much as [[#Amazon SQS]]/[[#Amazon SNS]] 
- runs on servers, can run in Multi-AZ with failover => can be made highly available
- has both queue and topic features
==__*use only and only if company is migrating to cloud and needs to use open protocols*__==
