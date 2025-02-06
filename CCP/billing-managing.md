# Account Management & Billing

Created by: Yacqub 
Created time: October 27, 2024 7:58 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

## AWS Organisations

- Global Service
- Allows to manage multiple AWS accounts
- The main account is the master account
- Cost benefit:
    - Consolidated billing across all accounts -single payment method
    - Pricing benefits from aggregated usage (volume discount)
    - Pooling of reserved EC2 instances for optimal savings
- API available to automate AWS account creation
- Restrict account privileges using service control policies
- Multi Account strategies
    - Create accounts per department, per cost center, per dev / test prod, based on regulatory restrictions, for better resource isolation, to have separate per account service limits, isolated account for logging
    - Multi account vs one account multi vpc
    - Use tagging standards for billing purpsoses
    - Enable cloudtrail on all accounts

## Consolidated Billing

- When enabled provides you with
    - Combined usage: combine the usage across all AWS accounts in the AWS organisation to share the volume pricing, reserved instances and savings plans discounts
    - One bill: get one bill for all AWS accounts in the AWS Organisation
- The management account can turn off reserved instances discount sharing for any account int he AWS organisation including itself

## AWS Control Tower

- Easy way to set up and govern a secure and compliant multi account AWS environment based on best practices
    - Benefits
        - Automate the setup of your environment in a few clicks
        - Automate ongoing policy management using guardrails
        - Detect policy violations and remediate them
        - Monitor compliance through interactive dashboard
    - AWS Control Tower runs on top of AWS organisations to organise accounts and implement SCPs (Service Control Policies)

## Resource Access Manager (RAM)

- share resources that you own with other AWS accounts
- Share with any account within organisation
- Avoid resource duplication
- Supported resources:
    - Aurora
    - VPC subnets
    - Transit Gateway
    - Route 53
    - EC2 Dedicated Hosts

## AWS Service Catalog

- Users that are new to AWS have too many options and may create stacks that are not compliant or in line with the rest of the organisation
- Some users just want a quick self service portal to launch a set of authorised products pre-defined by admins
- Includes: virtual machines, databases, storage options, etc…
- Enter AWS Service Catalog
- As an admin
    - You’re going to creat products which are cloud formation templates
    - A portfolio is a collection of products
    - Define who has access to what products in the portfolio IAM permissions
- As a user:
    - Login to your portal
    - Quick list of products available due to IAM permissions

## Pricing Models in AWS

- 4 pricing models
    - **Pay as you go:**
        - Pay for what you use, remain agile, responsive, meet scale demands
    - **Save when you reserve:**
        - minimum risks, predictably manage budgets, comply with long-terms requirements
        - Reservations are available for EC2 instances, dynamodb
    - **Pay less by using more:**
        - Volume-based discounts
    - **Pay less as AWS grows**
- Free services & free tier in AWS
    - IAM
    - VPC
    - Consolidated Billing
    - **Services that you pay for the resources created**
        - Elastic Beanstalk
        - CloudFormation
        - Auto Scaling Groups
    - Free tier
        - EC2 t2.micro instance for a year
        - S3 EBS, ELB, AWS Data transfer
- **Compute Pricing - EC2**
    - Only charged for what you use
        - Number of instances
        - Instance configuration
            - Physical capacity
            - Region
            - OS and software
            - Instance type
            - Instance size
        - ELB running time and amount of data processed
        - Detailed monitoring
    - On-demand instances:
        - Minimum of 60s
        - Pay per second (Linux/windows) or per hour (others)
    - Reserved instances:
        - Up to 75% discount compared to On-demand on hourly rate
        - 1 or 3 years commitment
        - All upfront, partial upfront, no upfront
    - Spot instances:
        - Up to 90% discount compared to On-demand on hourly rate
        - Bid for unused capacity
    - Dedicated host:
        - On-demand
        - Reservation for 1 year or 3 years commitment
    - Savings plan as an alternative to save on sustained usage
- **Compute Pricing - Lambda & ECS**
    - Lambda
        - Pay per call
        - Pay per duration
    - ECS
        - EC2 Launch Type Model: No additional fees, you pay for the AWS resources stored and created in your application
    - Fargate
        - Fargate Launch Type Model: pay for vCPU and memory resources allocated to your applications in your container
- **Storage Pricing - S3**
    - Storage Class:
        - S3 Standard
        - S3 infrequent access
        - S3 One-Zone IA
        - S3 Intelligent Tiering
        - S3 Glacier
        - S3 Glacier Deep Archive
    - Number and size of objects: price can be tiered (based on volume)
    - Number and type ofrequests
    - Data transfer OUT of the S3 region
    - S3 transfer acceleration
    - Lifecycle transitions
    - Similar service is EFS
- **Storage Pricing - EBS**
    - Volume type (based on performance)
    - Storage volume in GB per month provisioned
    - IOPS:
        - General purpose SSD: included
        - Provisioned IOPS SSD: provisioned amount in IOPS
        - Magnetic: Number of requests
    - Snapshots:
        - Added data cost per GB per month
    - Data transfer:
        - Any data transfer out are tiered for volume discounts
        - Inbound is free
- **Database Pricing - RDS**
    - Per hour billing
    - Database characteristics:
        - Engine
        - Size
        - Memory class
    - Purchase type:
        - On-demand
        - Reserved instances (1 or 3 years) with required up-front
    - Backup storage: there is no additional charge for backup storage up to 100% of your total database storage for a region
    - Additional storage (per GB per month)
    - Number of input and output requests per month
    - Deployment type (storage and I/O are variable)
        - Single AZ
        - Multiple AZ
    - Data transfer:
        - Outbound data transfer are tiered based on volume
        - Inbound is free
- **Content Delivery - CloudFront**
    - Pricing is different across different geographic regions
    - Aggregated for each edge location, then applied to your bill
    - Data transfer out (volume discount)
    - Number of HTTP/HTTPS requests
- **Networking costs in AWS per GB**
    - Free traffic inbound
    - Free traffic between ec2 instances in the same AZ using private IP
    - If you have two instances in two different AZ to communicate
        - $0.02 per GB  → public IP
        - $0.01 per GB 0 → private IP
        - Recommend private
    - Separate region communication fee of $0.02 per GB

## Savings plan Overview

- commit a certain $ amount per hour for 1 or 3 years
- Easiest way to setup long-term commitments on AWS
- Two types
    - **EC2 Savings Plan**
        - Up to %72 discount compared to On-demand
        - **Commit to usage of individual instance families in a region (e.g. C5 or M5)**
        - Regardless of AZ, size, OS or tenancy
    - **Compute Savings Plan**
        - Up to %66 discount compared to on-demand
        - Regardless of family, region, size, OS, tenancy, compute options
        - Compute options: EC2, Fargate, Lambda
    - Machine Learning Savings Plan: SageMaker…
- Setup from the AWS Cost Explorer console
- Estimate pricing at savingsplan

## AWS Compute Optimiser

- Reduce costs and improve performance by recommending optimal AWS resources for your workloads
- Helps you choose optimal configurations and right-size your workloads (over/under provisioned)
- Uses machine learning to analyse your resources configurations and their utilisation CloudWatch metrics
- Supported resources
    - Ec2 instances
    - Ec2 auto scaling groups
    - EBS volumes
    - Lambda functions
- Lower your costs by up to 25%
- Recommendations can be exported to S3

## Billing and Costing Tools

- **Estimating costs in the cloud:**
    - Pricing Calculator
- **Tracking costs in the cloud:**
    - Billing Dashboard
    - Cost Allocation Tags
    - Cost and Usage Reports
    - Cost Explorer
- **Monitoring against costs plans:**
    - Billing Alarms
    - Budgets

## AWS Pricing Calculator

- https://calculator.aws/
- Estimate the cost for your solution architecture

## Cost Allocation Tags

- Use to track your AWS costs on a detailed level
- AWS generated tags
    - Automatically applied to the resource you create
    - Starts with a prefix aws:
- User defined tags
    - Defined by the user
    - Starts with prefix user:
- Tagging and Resource Groups
    - Tags are used for organising resources:
        - EC2: instances, images, load balancers, security groups…
        - RDS, VPC resources, Route 53, IAM users, etc…
        - Resources created by CloudFormation are all tagged the same way
    - Free naming, common tags are: Name, Environment, Team

## Cost & Usage Reports

- Dive deeper into your AWS costs and usage
- Contains the most comprehensive set of costs and usage data, including additional metadata about services, pricing and reservations (EC2 Reserved Instances)
- Lists AWS usage for each service category used by an account and its IAM users in hourly or daily line items, as well as any tags that you have activated for cost allocation purposes.
- Can be integrated with Athena redshift or quicksight
- Excel spreadsheet

## Cost Explorer

- Visualise, understand and manage your AWS costs and usage overtime
- Create custom reports that analyse cost and usage data
- Analyse data at a high level” total costs and usage across all accounts
- Or monthly, hourly, resource level granularity
- Choose an optimal savings plan to lower prices on your bill
- **Forecasts usage up to 12 months based on previous usage**

## Monitoring Costs in the Cloud

- **Billing Alarms**
    - **Billing data metric is stored in CLoudWatch us-east-1**
    - Billing data re for overall worldwide AWS costs
    - Its for actual cost, not for projected costs
    - Intended a simple alarm
- **Budgets**
    - Create a budget and send alarms when costs exceed the budget
    - 4 types
        - Usage
        - Cost
        - Reservation
        - savings plan
    - For reserved instances
        - Track utilisation
        - Supports EC2, ElastiCache, RDS, Redshift
    - Up to 5 SNS notifications per budget
    - Can filter by: service, linked account, tag, purchase option, instance type, region, availability zone, api operation etc…
    - Same option as AWS Cost Explorer
    - 2 budgets are free, then $0.02 per day per budget

## AWS Cost Anomaly Detection

- continuously monitor your cost and using using ML to detect unusual spendings
- It learns your unique, historic spend patterns to detect one time cost spike
- Sends you the anomaly detection report with root=cause analysis
- Get notified with individual alerts or daily/weekly summary

## AWS Service Quotas

- Notify you when you’re close to a service quota value threshold
- Create CloudWatch Alarms on the Service QUotas console
- Example: lambda concurrent executions
- Request a quota increase from AWS service quotas or shutdown resources before limit is reached

## AWS Trusted Advisor

- No need to install anything - high level AWS account assessment
- Checks
    - Do you have EBS public snapshots
    - Are you using root account
- Provides recommendations on 6 categories
    - Cost optimisation
    - Performance
    - Security
    - Fault tolerance
    - Service limits
    - Operational excellence
- **Business & enterprise support plan**
    - Full set of checks
    - Programmatic access using AWS support api

## AWS Support Plans Pricing

- Basic Support Plan → Free
    - Customer service & communities - 24/7 access to customer service, documentation, whitepapers and support forums
    - Trusted advisor - access to the 7 core trusted advisor checks and guidance to provision your resources following best practices to increase performance and improve security
    - AWS personal health dashboard - personalised view of the health of AWS services and alerts when your resources are impacted
- Developer Support Plan →
    - Business hours email access to Cloud Support Associates
    - Unlimited cases / contacts
    - Case severity / response times
        - General guidance: < 24 business hours
        - System impaired: < 12 business hours
- Business Support Plan →
    - Intended to be used if you have production workloads
    - Trusted Advisor - Full set of checks + API access
    - 24/7 phone email and chat access to cloud support engineers
    - Unlimited cases / contacts
    - Access to infrastructure event management for additional fee
    - Case severity / response time:
        - General guidance: < 24 business hours
        - System impaired: < 12 business hours
        - Production system impaired: < 4 hours
        - Production system down: < 1 hour
- Enterprise On-Ramp support plan
    - Intended to be used if you have production or business critical workloads
    - All of business +
    - Access to a pool of technical account managers (TAM)
    - Concierge support team (for billing and account best practises)
    - Infrastructure event management, well-architected & operations reviews
    - Case severity / response time
        - …
        - Production system impaired: < 4 hours
        - Production system down: < 1 hour
        - Business-critical system down: < 30 minutes
- Enterprise support plan
    - Intended to be used if you have mission critical workloads
    - All of business +
    - Designated technical account manager
    - Support team
    - Reviews
    - Case severity / response time
        - …
        - Production system impaired: < 4 hours
        - Production system down: < 1 hour
        - Business-critical system down: < 15 mins

## Account Best Practices Summary

- Operate multiple accounts using AWS Organisations
- Using SCP (Service control policies) to restrict account power
- Easily setup multiple accounts with best practices using AWS Control Tower
- Use tags and cost allocation tags for easy management and billing
- IAM guidelines: MFA, least-privilege, password policy, password rotation
- AWS Config to record all resources configurations and compliance over time
- CloudFormation to deploy stacks across accounts and regions
- Trusted Advisor to get insights, support plan adapted to your needs
- Send service logs and access logs to s3 or cloudwatch logs
- Cloudtrail to record API calls made within account
- If your account is compromised: change the root password, delete and rotate all passwords / keys, contact the AWS suppport
- Allow users to create pre-defined stacks defined by admins using AWS Service Catalog

## Billing and Costing Tools - Summary

- Compute Optimizer: recommends resources configurations to reduce cost
- Pricing calculator: cost of services on AWS
- Billing Dashboard: high level overview + free tier dashboard
- Cost allocation tags: tag resources to create detailed reports
- Cost and usage reports: most comprehensive billing dataset
- Cost explorer: view current usage (detailed) and forecast usage
- Billing alarms: in us-east-1 - track overall and per service billing
- Budgets: more advanced - track usage, costs, RI and get alerts
- Savings plan: easy way to save based on long term usage of AWS
- Cost anomaly detection: detect unusual spends using Machine Learning
- Service Quotas: notify you when you’re close to service quota threshold

---