# Deploying & Managing Infrastructure at Scale

Created by: Yacqub 
Created time: October 11, 2024 7:39 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

## Cloud Formation

- Declarative way of outlining your AWS infrastructure, for any resource (most of them are supported)
- For example Within a CloudFormation template you say:
    - I want a security group
    - I want two EC2 Instances using this security group
    - I want a s3 bucket
    - I want a load balancer in front of these machines
- Benefits:
    - Infrastructure as code
        - No resources are manually created which is great for control
        - Changes to the infrastructure are reviewed through code
    - Cost
        - Each resource within the stack is tagged with an identifier so you can see easily how much a stack costs you
        - You can estimate costs of your resources using CloudFormation template
        - Savings strategy: In dev, you could automation deletion of templates at 5pm and recreated at 8am safely.
    - Productivity
        - Ability to destroy and re-create an infrastructure on the fly
        - Automation generation of Diagram for your templates
        - Declarative programming (no need to figure out ordering and orchestration)
    - Don’t re-invent the wheel
        - Leverage existing templates on the web
        - Leverage the documentation
    - Supports all resources in AWS
        - If it doesn’t support them can use custom resources
    
    ## AWS Cloud Development Kit (CDK)
    
    - Define your cloud infrastructure using familiar language:
        - JavaScript/typescript, python, java
    - The code is “compiled” into a CloudFormation template (JSON/YAML)
    - You can deploy infrastructure and application runtime code together
        - Great for lambda functions
        - Great for docker containers in ECS / EKs
    
    ## Typical architecture: Web App 3-tier
    
    - User → Load balancer → traffic to multiple EC2 managed by ASG → store data in RDS / in memory cache to ElastiCache
    - Developer Problems on AWS
        - Don’t want to manage infrastructure (config databases, load balancers etc)
        - Only want to deploy code
        - Scaling concerns
        - Most web apps have the same/similar architecture (ALB + ASG)
    - **All developers want is for their code to run?**
    - Consistently across different applications & environments
    - That is what Elastic Beanstalk does
    
    ## Elastic BeanStalk
    
    - Developer centric view of deploying an application on AWS
    - It uses all the components we’ve seen before:
        - EC2
        - ASG
        - ELB
        - RDS…
    - All in one view that’s easy to make sense of
    - Still full control over the configuration
    - Beanstalk is a Platform as a Service (PaaS)
    - Free but pay for all the underlying resources
    - Managed Service
        - Instance configuration / OS is handled by Beanstalk
        - Deployment strategy can be configured but performed by Beanstalk
        - Capacity provisioning
        - Load balancing and auto scaling
        - Application health monitoring dashboard
    - Just the application code is the developers responsibility
    - **Developer DREAM**
    - Three architecture models:
        1. Single Instance deployment: good for dev
        2. LB + ASG for production or pre-production web applications
        3. ASG only: great for non-web apps in production (workers etc..)
    - Supports for many platforms:
        - Go, Java, .NET, node.js, php, python, ruby, packer, docker
    - Health Monitoring
        - Health agent pushes metrics to CloudWatch
        - Checks for app health events
    
    ## Code Deploy
    
    - We want to deploy our application automatically
    - Works with EC2 instances upgrades e.g v1 → v2
    - Works with on-premises servers upgrades v1 → v2
    - Hybrid service
    - Servers / instances must be provisioned and configured ahead of time with the code deploy agent.
    
    ### CodeCommit (depreciated)
    
    - Github replacement
    - Stores code
    - Benefits:
        - Fully Managed
        - Scalable & highly available
        - Private, secured, integrated with AWS
    
    ## CodeBuild
    
    - allows to build code in the cloud
    - Compiles source code, run tests and produces packages that are ready to be deployed
    - Benefits
        - Fully managed, serverless
        - Continuously scalable, available
        - Secure
        - Pay as you go pricing - only pay for the build time
    
    ## Code Pipeline
    
    - Orchestrate the different steps to have the code automatically pushed to production
        - code → build → test → provision → deploy
        - CI/CD (Continuous Integration & Continuous Delivery)
    - Example
        - code pipeline orchestration layer = CodeCommit → CodeBuild → CodeDeploy → Elastic Beanstalk
    - Benefits
        - Fully managed, compatible with code commit,build,deploy, elastic beanstalk, cloudformation, GitHub
        - Fast delivery, rapid updates
    
    ## CodeArtifact
    
    - Software packages depend on each other to be built (also called code dependencies) and new ones are created.
    - Storing and retrieving these dependencies is called artifact management
    - Traditionally you need to setup your own artifact management system
    - Code artifact, secure, scalable, cost effective artifact management system
    - Works with common dependency management tools like Maven, npm, yarn, pip, NuGet
    - Developers can then retrieve dependencies straight from code artifact
    
    ## AWS Systems Manager (SSM)
    
    - Helps you manage your EC2 and On-Premises systems at scale
    - Hybrid AWS Service (like codedeploy)
    - Suite of 10+ products
    - Most important features are:
        - Patching automation for enhanced compliance
        - Run commands across an entire fleet of servers
        - Store parameter configuration with the SSM parameter store
    - Works for Linux windows macOS and raspberry Pi
    - **For exam: any time there is a way to patch fleet of ec2 instances or on-premise servers or command consistently across all servers then its SSM**
    - Need to install the SSM agent onto the systems we control (small program that uses it in the background)
    - Installed by default on amazon Linux AMI or Ubuntu
    - SSM Agent must be installed on all so that it can report back to
    - Linked to both EC2 and on-premise
    - Most faults go back to the SSM Agent
    
    ## System Manager - SSM Session Manager
    
    - Allows you to start a secure shell on your EC2 on-premise servers
    - No SSH access, bastion hosts, or SSH keys needed
    - No port 22 needed (better security)
    - Supports Linux macOS and windows
    - Send session log data to S3 or CloudWatch logs
    - Fleet Manager is where all the managed ec2 instances will appear
    - Makes use of the SSM agents of each individual instance / on-premise so that it can communicate back without needing ssh.
    
    ## Systems Manager Parameter Store
    
    - Secure storage for configuration and secrets
    - API Keys, passwords, configurations…
    - Serverless, scalable, durable, easy SDK
    - Control access permissions using IAM
    - version tracking , encryption (optional)
    
    ## Deployment Summary
    
    **Deployment Services**
    
    - Cloud Formations: (AWS Only)
        - Infrastructure as Code, works with almost all of AWS resources
        - Repeat across regions & accounts
    - Beanstalk (AWS Only)
        - Platform as a Service (PaaS), limited to certain programming languages or Docker
        - Deploy code consistently with a known architecture: ALB ASG EC2 RDS
    - Code Deploy
        - Deploy and upgrade any application onto servers (hybrid service)
    - System Manager
        - Patch, configure and run commands at scale (hybrid)
    
    **Developer Services**
    
    - CodeCommit
        - Store code in private git repository
    - CodeBuild
        - Build & test code in AWS serverless
    - Code Deploy
        - Deploy code onto servers
    - CodePipeline
        - Orchestration of Pipeline
    - CodeArtifact
        - Store software packages / dependencies on AWS
    - AWS CDK
        - Define your cloud infrastructure using a programming language
    

---