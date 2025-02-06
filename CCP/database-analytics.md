# Amazon Database & Analytics

Subject Tags: AWS
Created time: October 9, 2024 12:01 PM
Last edited time: October 9, 2024 4:56 PM

### Databases Introduction

- storing data on **disk** (EFS, EBS, EFS, EC2 Instance Store, s3) can have its **limits**
- Sometimes you want to store data in a database
- You can structure the data
- You build indexes to efficiently query/search through your data
- You define relationships between your datasets
- Databases are optimised for a purpose and come with different features, shapes and constraints

### Relational Databases

- Looks just like an excel spreadsheets, with links between the tables
- In a relational database you’re building relations between tables and linking them
- Can use SQL language to perform queries

### NoSQL Databases

- Non relational databases
- Built for a specific purpose with specific data models have flexible schemas for building modern apps
- Benefits
    - Flexible
    - Scalability
    - High-performance
    - Highly functional
- Examples: key-value, document, graph, in-memory, search databases

**NoSQL data example:** 

- JSON = JavaScript object notation
- JSOn is a common form of data that fits into a NoSQL model
- Data can be nested
- Fields can change over time
- Support for new types: arrays, etc

```json
{
  "books": [
    {
      "id": 1,
      "title": "To Kill a Mockingbird",
      "author": "Harper Lee",
      "year": 1960
    },
    {
      "id": 2,
      "title": "1984",
      "author": "George Orwell",
      "year": 1949
    },
    {
      "id": 3,
      "title": "Pride and Prejudice",
      "author": "Jane Austen",
      "year": 1813
    }
  ]
}
```

### Databases & Shared Responsibility on AWS

- AWS offers use to manage different databases
- Benefits include:
    - Quick to provision, High availability, Vertical and Horizontal scaling
    - Automated backup & restore, operations and upgrades
    - Operating system patching is handled by AWS
    - Monitoring and Alerting
- Note: many database technologies could be run on EC2, but you must handle yourself the resiliency, backup, patching, high availability, fault tolerance, scaling etc…

### Amazon RDS Overview

- RDS stands for Relational Database Service
- It’s a managed DB service for DB using SQL as a query language
- It allows you to create databases in the cloud that are managed by AWS
    - Postgres
    - MySQL
    - MariaDB
    - Oracle
    - Microsoft SQL Server
    - IBM DB2
    - Aurora (AWS Proprietary database)
- Advantages include:
    - RDS is a managed service:
        - Automatic provisioning, OS patching
        - Continuous backups and restore to specific timestamp
        - Monitor dashboards
        - Read replicas for improved read performance
        - Multi AZ setup for Disaster Recovery
        - Maintenance windows for upgrades
        - Scaling capability
        - Storage backed by EBS
- BUT you cannot use SSH into your instances

### Amazon Aurora

- Aurora is a Proprietary technology created by AWS (not open sourced)
- Postgres and MySQL are both supported as Aurora DB
- Aurora is “AWS cloud optimised” and claims 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
- Aurora storage automatically grows in increments of 10GB up to 128TB
- Aurora costs more than RDS (20% more) - but it is more efficient
- Not in the free tier but RDS is
- Amazon Server-less
    - Automated database instantiation and auto scaling based on actual usage
    - Supports Postgres and MySQL
    - No capacity planning needed
    - No management as no servers
    - Pay per second, can be more cost-effective
    - Use-case: good for infrequent, intermittent or unpredictable workloads
    - How it works: Clients connects to proxy fleet managed by aurora and it instantiates database instances when it needs to scale up or down. They share the same storage volume
    - **Exam: if you see aurora with no management overhead then think of aurora server-less**
    
    ### RDS Deployments: Read Replicas, Multi-AZ
    
- RDS Read Replicas:
    - Scale the read workload of your DB
    - Can create up to 15 Read Replicas
    - Data is only written to the main DB
- Multi-AZ
    - Failover in case of AZ outage (High Availability)
    - Reads and writes in the same main RDS Database
    - Replication from another AZ called failover in case main database crashes
    - Can only have 1 other AZ
- Multi-Region (Read Replicas)
    - Writes happen cross region but the reads since its multi region can be accessed locally in case of region issues so you have backups
    - Disaster recovery strategy In case of region issues
    - Location performance for global reads
    - Replication cost

### Amazon ElastiCache

- The same way RDS is to get managed Relational Databases…
- ElastiCache is to get managed Redis or Memcached
- Caches are i**n-memory** databases with **high performance** and **low latency**
- Helps reduce load off databases for read intensive workloads
- AWS takes care of OS maintenance, patching, optimisation, setup, config, monitoring, backups, failure recovery
- **IN MEMORY DATABASE**
- Saves workload and pressure from RDS

### Dynamo DB

- Fully Managed Highly available with replication across 3 AZ
- **NoSQL** database
- Scales to massive workload, distributed “**serverless”** database
- **We do not provision any servers/instances**
- Millions of requests per seconds, trillions of row, 100s of TB storage
- Fast and consistent performance
- **Single-digit millisecond latency - low latency retrieval**
- Integrated with IAM for security, authorisation and administration
- Low cost and auto scaling capabilities
- Standard & Infrequent Access Table Class
- Data
    - Key/Value database
    - Row by Row items

### Dynamo DB Accelerator - DAX

- Fully managed in-memory cache **for DynamoDB**
- 10x performance improvement -single- digit millisecond latency to microseconds latency when accessing dynamoDB tables
- Secure, highly scalable and highly available
- Difference with ElastiCache at the CCP level: DAX is only used for and is integrated with dynamoDB, while ElastiCache can be used for other databases

**DynamoDB - Global Tables**

- Make a DynamoDB table accessible with low latency in multiple regions
- Active-Active replication (read/write to any AWS region)

### RedShift Overview

- Redshift is based on PostgreSQL, but its not used for OLTP (Online transaction processing)
- Its OLAP - online analytical processing (analytics and data warehousing)
- Load data once every hour, not every second
- 10x better performance than other data warehouses, and scale to PBs of data
- **Columnar storage data** (instead of row based)
- Massively Parallel Query Execution (MPP), highly available
- Pay as you go based on instances provisioned
- Has SQL interface for performing queries
- BI tools such as AWS Quicksight or Tableau integration

### Redshift Serverless

- automatically provisions and scales data warehouse underlying capacity
- Run analytics workloads without managing data warehouse infrastructure
- Pay for what you use (save costs)
- Use case: reporting, dashboard in applications, real-time analytics…

### Amazon EMR

- EMR stands for “Elastic MapReduce”
- EMR helps creating **Hadoop clusters** (Big Data) to analyse and process vast amount of data
- The clusters can be made of hundreds of EC2 instances that will collaborate to analyse your data
- Also supports Apache Spark, Hbase, Presto, Flink…
- EMR takes care of all the provisioning and configuration
- Auto scaling and integration with Spot instances
- Use cases: data processing, machine learning, web indexing, big data…

### Amazon Athena

- **Serverless query service** to perform analytics against **S3 Objects**
- Use standard SQL language to query the files
- Supports CSV, JSON, ORC, Afro, and Parquet (built on Presto)
- Pricing: $5 per TB of data scanned
- Use compressed or columnar data for cost-savings (less scan)
- Use cases: business intelligence, analytics, reporting, analyze & query VPC Flow Logs, ELB Logs, CloudTrail trails, etc…

### Amazon QuickSight

- Serverless machine learning-powered business intelligence service to create interactive dashboards
- Fast, automatically scalable, embeddable, with per-session pricing
- Use cases:
    - Business analytics
    - Building visualisations
    - Perform ad-hoc analysis
    - Get business insights using data
- Integrated with RDS, Aurora, Athena, Redshift, S3…
- **Quicksight is the answer for BI in AWS**

### DocumentDB

- Aurora is an “AWS-implementation” of PostgreSQL & MySQL …
- DocumentDB is the same for MongoDB (which is a NoSQL database)
- MongoDB is used to store, query and index JSON data
- Similar “deployment concepts” as Aurora
- Fully managed, highly available, with replication across 3 AZ
- DocumentDB storage automatically grows in increments of 10GB
- Automatically scales to workloads with millions of requests per second

### Amazon Neptune

- Fully managed **graph** database
- A popular **graph dataset** would be a **social network**
    - users have friends
    - Posts have comments
    - Comments have likes from users
    - Users share and like posts…
- Highly available across 3AZs with up to 15 read replicas
- Build and run applications working with highly connected datasets - optimised for these complex and hard queries
- Can store up to billions of relations and query the graph with milliseconds latency
- Highly available with replications across multiple AZs
- **Great for knowledge graphs**
    - Wikipedia
    - Fraud detection
    - Recommendation engines
    - Social networking

### Amazon Timestream

- Fully managed, fast, scalable, serverless time series database
- Automatically scales up/down to adjust capacity
- Store and analyze trillions of events per day
- 1000s times faster and 1/10th the cost of relational databases
- Built in time series analytics functions (helps you identify patterns in your data in near real-time)

### Amazon QLDB

- **QLDB stands for Quantum Ledger Database**
- A ledger is a book recording financial transactions
- Fully managed serverless highly available replication across 3 AZ
- Used to review history of all the changes made to your application data over time
- Immutable: cannot be removed or modified
- 2-3x better performance than common ledger blockchain frameworks and can be manipulated using SQL
- Difference with Amazon Managed Blockchain: no concept of decentralisation, in accordance with financial regulation rules

### Amazon Managed Blockchain

- blockchain makes it possible to build applications where multiple parties can execute transactions without the need for a **trusted, central authority**
- Amazon managed blockchain is a managed service to:
    - Join public blockchain networks
    - Or create your own scalable private network
- Compatible with:
    - Hyper-ledger Fabric
    - Ethereum
- **Decentralised blockchain**

### AWS Glue

- **Managed extract, transform and load (ETL) service**
- Useful to prepare and transform data for analytics
- Fully serverless service
- E.g use glue to **extract** data from s3 bucket and amazon RDS and we would write a script to do a **transform** and then **load** that data into amazon Redshift
- Glue data catalog: catalog of datasets → can be used by Athena, Redshift, EMR

### Database Migration Service

- Migrate one database to another
- Source database → ec2 instance running DMS → Target DB.
- Quickly and securely migrate databases to AWS, resilient, self healing
- The source database remains available during the migration
- Supports
    - Homogeneous migrations → oracle to oracle
    - Heterogeneous migrations → Microsoft SQL Server to Aurora
- **Any time you see migration of a database think DMS**

### Databases & Analytics Summary

- Relational Databases - OLTP: RDS & Aurora (SQL)
- Differences between Multi-AZ, Read Replicas, Multi-Region
- In-memory database: ElastiCache
- Key/value Database: DynamoDB (serverless) & DAX (cache for DynamoDB)
- Neptune: Graph Database
- Timestream: time-series database
- Warehouse - OLAP: Redshift (SQL)
- Hadoop Cluster: EMR
- Athena: query data on Amazon s3 (serverless & SQL)
- QuickSight: dashboards on your data (serverless)
- DocumentDB: Aurora of MongoDB
- Amazon QLDB: Financial transactions Ledger (immutable journal, cryptographically verifiable)
- Amazon Managed blockchain: managed hyperledger fabric & ethereum
- Glue: Managed ETL (Extract, transform, load) and data catalog service
- Database Migration: DMS