# Other Compute Services: ECS, Lambda, Batch, Lightsail

Created by: Yacqub 
Created time: October 10, 2024 8:13 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

## ECS - Elastic Container Service

- Launch Docker containers on AWS
- You must provision & maintain the infrastructure (the ec2 instances)
- AWS takes care of starting / stopping containers
- Has integrations with the application Load Balancer

## Fargate

- Also for docker container launch on AWS
- Serverless offering don’t manage any servers
- You do not provision the infrastructure (no EC2 instances to manage)
- Simpler
- AWS just runs containers for you based on the CPU / RAM

## ECR - Elastic Container Registry

- Private docker registry on AWS
- Store your docker images so they can be run by ECS or Fargate
- This comes before fargate or ECS

## What is Serverless?

- A new paradigm in which the developers don’t have to manage servers anymore…
- They just deploy the code
- They deploy functions
- Initially… Serverless == FaaS (function as a service)
- Serverless was pioneered by AWS lambda but now also includes anything that’s managed: databases, messaging, storage etc
- It doesn’t mean that there is no servers it means you just don’t manage, provision or see them
- Examples include:
    - Amazon s3, dynamoDB, Fargate, Lambda

## Lambda Overview

- Using an EC2 instance, we have a virtual server in the cloud but are limited by RAM and CPU
- Continuously running
- Scaling means intervention to add / remove servers over time
- Virtual functions - no servers to manage
- Limited by time - short executions
- Run on-demand
- Scaling is automated

Benefits of AWS Lambda

Easy pricing

- Pay per request and compute time

Free tier of 1,000,000 AWS lambda requests and 400,000 GBs of compute time

Integrated with the whole AWS suite of services

Event-Driven: functions get invoked by AWS when needed

Integrated with many programming languages

Easy monitoring with AWS CloudWatch

Easy to get more resources per function (up to 10GB of ram)

Increasing RAM will also improve CPU and network

- Languages
    - Node.js, Python, c#, ruby
    - Custom Runtime API (community supported, example rust or golang)
- Lambda container image
    - The container image must implement the Lambda Runtime API
- Example: Serverless Thumbnail Creation:
    - New image in S3 → Lambda trigger creates thumbnail → push metadata to DynamoDB

## Lambda Pricing

- Pay per calls:
    - First 1M requests is free
    - $0.20 per 1M requests after
- Pay per duration
    - 400,000 GB-seconds of compute time per month if FREE
    - == 400,000 seconds if function is 1GB RAM
    - == 3,200,000 seconds if function is 128GB
    - After that $1.00 for 6,000 GB-seconds
- very cheap and popular service
- **Lambda pricing is based on calls and duration**

 ****

## Amazon API Gateway

- example: building a serverless API
- For client to have intermediary between the lambda function through API Gateway via a REST API
- Proxy request from api gateway to lambda → Crud to DynamoDB e.g
- Serverless fully scalable
- Supports restful apis
- Support for security, user authentication, api throttling, api keys, monitoring

## AWS Batch

- fully managed batch processing at any scale
- Efficiently run 100,000s of computing batch jobs on AWS
- A job that has a start and an end (opposed to continuous)
- Batch will dynamically launch ec2 instances or spot instances
- Will provision right amount of compute / memory
- Batch jobs are defined as docker images and run on ECS
- Helpful for cost optimisations and focusing less on the infrastructure
- Example:
    - Image put into S3 → trigger AWS Batch which automatically has an ECS cluster made of EC2 or spot instances → batch will make sure you have the right number of instances to accommodate for the load of jobs you have in the batch queue

**Batch vs Lambda**

- Lambda
    - Time limit
    - Limited runtimes
    - Limited temporary disk space
    - Serverless
- Batch
    - No time limit
    - Any runtime as you want as its packaged as a docker image
    - Rely on EBS / instance store for disk space
    - Relies on EC2

## Amazon Lightsail

- Standalone server
    - Virtual servers, storage, databases and networking all in one place
- low and predictable pricing
- Simpler alternative to using EC2, RDS,ELB,EBS,Route53…
- Great for people with little cloud experience
- Setup monitoring and notifications
- Use case:
    - Simple web applications
    - Websites (wordpress)
    - Dev / test enviroments
- Has high availability but no auto scaling, limited AWS integrations

---