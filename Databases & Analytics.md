# Database
- structure the data
- build **indexes** to efficiently **query/search** the data
- define **relationships** between datasets
- **optimized for a purpose** and come with different features, shapes and constraints

## Types
### Relational Databases
- data stored in tables
- can use SQL language for queries
![[Pasted image 20250216162211.png]]

### NoSQL Databases
- non relational databases
- flexible schema for building modern apps
- Benefits:
	- flexible - easy to evolve the data model
	- scalable - designed to scale out using distributed clusters
	- high performance - optimized for specific data model
	- highly functional - types optimized for the data model
- Examples: Key-Value, document, graph, in-memory databases

#### NoSQL data example: JSON
![[Pasted image 20250216162633.png]]

## Shared Responsibility
- provides managed databases
- Benefits
	- Quick provisioning
	- high availability
	- vertical and horizontal scaling
	- Automated Backup & Restore, Operations and Upgrades
	- OS patching
	- Monitoring, alerting
==***Note***: we can run own database technology on EC2, but we will also need to handle resiliency, backups, patching, fault tolerance, etc. on our own.==

## Managed Databases
### Amazon RDS
- RDS = Relational Database Service
- managed database service where SQL is used
- Supports multiple database engines:
	- Postgres
	- MySQL
	- MariaDB
	- Oracle
	- Microsoft SQL Server
	- IBM DB2
	- Aurora (AWS Proprietary Database)
#### Advantage over EC2
- RDS is a managed service
	- automated provisioning, OS Patching
	- continuous backups and restore to specific timestamp (Point in Time Restore)
	- Monitoring Dashboards
	- read replicas for improved read performance
	- multi AZ for disaster recovery
	- maintenance windows for upgrades
	- scaling capability
	- storage backed by EBS

#### RDS Solution Architecture
![[Pasted image 20250216164759.png]]

#### Amazon Aurora
- Amazon proprietary technology
- Supports PostgreSQL and MySQL
- *"cloud optimized"*. Claims 5x performance improvements over MySQL on RDS and over 3x over Postgres on RDS
- Storage grows automatically in increments of 10GB, up to 128TB
- cost more than RDS (20%) - but more efficient
- not in the free tier

#### Amazon Aurora Serverless
- automated database instantiation and auto-scaling based on usage
- PostgreSQL and MySQL are both supported
- no capacity planning required
- least management overhead
- pay per second
- Use cases: good for infrequent, intermittent or unpredictable workloads...
![[Pasted image 20250217103454.png]]

#### RDS Deployments: Read Replicas, Multi-AZ, Multi-Region
- **Read Replicas**
	- Scale the read workload of DB
	- up to 15 read replicas
	- data can only be written to main DB 
	![[Pasted image 20250217110003.png]]
- Multi-AZ
	- Failover in case of AZ outage (high availability)
	- data is only read/written to main DB
	- can only have 1 other AZ as failover
	![[Pasted image 20250217110143.png]]
- Multi-Region (Read Replicas)
	- Disaster recovery in case of region issue
	- Local performance for global reads
	- Replication cost
	![[Pasted image 20250217110408.png]]
### Amazon ElastiCache
- managed Redis or Memcached
- in-memory databases with high performance, low latency
- reduce load off read intensive workloads

#### Solution Architecture - Cache
![[Pasted image 20250217111026.png]]

### DynamoDB
- fully managed highly available with replication across 3 AZ
- NoSQL database
- scales to massive workloads
- distributed '*serverless*' database
- millions of requests per second, trillions of row, 100s of TB of storage
- single-digit millisecond latency - low latency retrieval
- IAM for security, authorization and administration
- low cost and auto scaling 
- Standard & Infrequent Access (IA) Table Class

#### Type of data
- key/value database
	![[Pasted image 20250217111425.png]]
#### DynamoDB Accelerator - DAX
- fully managed in-memory cache for DynamoDB
- **10x performance improvement** - single digit millisecond latency to microseconds latency
- secure, highly scalable and highly available
- ***ElastiCache** can be used with other DBs but **DAX** only with DynamoDB*
	![[Pasted image 20250217112638.png]]
#### Global Tables
- accessible with low latency in multiple-regions
- active-active replication (read/write to any AWS Region)
![[Pasted image 20250217112845.png]]

### Redshift
- based on PostgreSQL
- used for **OLAP** - Online Analytical Processing (*analytics and data warehousing*)
- load data once every hour
- 10x better performance than other data warehouses
- scale to PBs of data
- data stored in columns(columnar) instead of rows
- **MPP** (Massively Parallel Query Execution)
- pay as you go based on provisioned instances
- SQL interface for queries
- BI tools such as AWS Quicksight or Tableau can be integrated

#### Redshift Serverless
- automatically provision and scale data warehouse
- pay for what is used
- run analytics workloads without managing data warehousing infrastructure
- Use Cases
	- Reporting
	- Dashboarding apps
	- real time analytics
	- ...
![[Pasted image 20250217113809.png]]

### Amazon EMR
- EMR = Elastic MapReduce
- helps to create [[Hadoop]] clusters (Big Data) to analyze and process vast amounts of data
- clusters can be made of hundreds of EC2 instances
- Supports: Apache Spark, HBase, Presto, Flink...
- takes care of configuration and provisioning
- auto-scaling and integrated with Spot instances
- Use Cases
	- data processing
	- machine learning
	- web indexing
	- big data
	- ...
### DocumentDB
- DocumentDB is the [[#Amazon Aurora]] version of PostgreSQL/MySQL for [[MongoDB]]
- [[MongoDB]] compatible
- similar "deployment concepts" as [[#Amazon Aurora]]
- Fully managed, highly available with replication across 3 AZ
- Automatically grows in increments of 10GB
- Automatically scales to workloads with millions of requests per second
### Amazon Neptune
- GraphDB
- replication across 3 AZ
- up to 15 read replicas
- used to build and run apps with highly connected datasets
- optimized for complex and hard queries of graph datasets
- can store up to billions of relations and query the graph with millisecond latency
- Great for 
	- Knowledge graphs
	- Fraud detection
	- Recommendation engines
	- Social networking

### Amazon Timestream
- fully managed, fast, serverless time series DB
- automatically scaling based on capacity
- store and analyze trillions of events per day
- 1000s time faster & 1/10$^\text{th}$ the cost of relational DB
- built-in time series analytics functions

### Amazon QLDB
- QLDB = Quantum Ledger Database
- fully managed, serverless, highly available, replication across 3 AZ
- used to review the history of all the changes made to application over time
- **Immutable** system and cryptographically verifiable
- for recording transactions
- 2-3x better performance than common ledger blockchain framework, manipulate data using SQL
- *Difference with Amazon Managed Blockchain*: **no decentralization component**, in accordance with financial regulation rules
### Amazon Managed Blockchain
- managed service that
	- join public [[Blockchain]] networks
	- or create own scalable private network
- Compatible with frameworks Hyperledger Fabric & Ethereum
## Database Migration Service (DMS)
- to migrate data from one DB to another
![[Pasted image 20250217141628.png]]
- quickly and securely migrate databases to AWS which is resilient and self healing
- source DB remains available during migration
- Supports
	- Homogenous Migration
		- *Example*: Oracle to Oracle
	- Heterogenous Migration
		- DMS is smart enough to know how to convert the data from source to target
		- *Example*: Microsoft SQL Server to Aurora
# Analytics
### Amazon Athena
- serverless query service to perform analytics against S3 objects
- uses standard SQL language to query the files
- supports CSV, JSON, ORC, Avro and Parquet (built on Presto)
- Pricing: $5 per TB of data scanned
- use compressed or columnar data for cost-savings due to less scan requirement
- Use Cases
	- BI
	- analytics
	- reporting, analyze & query VPC Flow Logs, [[Elastic Load Balancing & Auto Scaling Groups#Why use Elastic Load Balancer?|ELB]] Logs, CloudTrail trails, etc...
![[Pasted image 20250217133703.png]]

### Amazon QuickSight
![[Pasted image 20250217133947.png]]
- serverless ML powered BI service to create interactive dashboards
- fast, automatically scalable, embeddable with per-session pricing
- Use Cases:
	- Business analytics
	- Building visualizations
	- Perform ad-hoc analysis
	- Get business insights using data
- Integrated with [[#Amazon RDS]], [[#Amazon Aurora]], [[#Amazon Athena]], [[#Redshift]], [[Amazon S3#S3|S3]],...
### AWS Glue
- managed ETL service
- used to prepare and transform data for analytics
- fully serverless
![[Pasted image 20250217141054.png]] 
- **Glue Data Catalog**
	- catalog of our datasets in AWS Infrastructure.
	- reference of everything
		- column names
		- field names
		- field types
		- ...
	- can be used by services such as [[#Amazon Athena]], [[#Redshift]] and [[#Amazon EMR]]

# Summary
![[Pasted image 20250217142140.png]]