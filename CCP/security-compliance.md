# Security & Compliance

Created by: Yacqub 
Created time: October 20, 2024 2:52 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

## DDOS Protection on AWS

- **AWS Shield Standard:** protects against DDOS attack for your website and applications, for all customers at no additional costs
- **AWS Shield Advanced:** 24/7 premium DDOS protection
- **AWS WAF:** filter specific requests based on rules
- **CloudFront and Route53:**
    - Availability protection using global edge network
    - Combined with AWS Shield, provides attack mitigation at the edge
- AutoScaling
- Route53 with AWS Shield → CloudFront Distribution with AWS Shield → Load Balancer → ec2 instance auto scaling group

## AWS Shield

- Free service that is active for every AWS customer
- Provides protection from attacks such as SYN/UDP floods, reflection attacks and other layer 3/4 attacks

## AWS Shield Advanced

- Optional DDOS mitigation service ($3k per month per organisation)
- Protect against more sophisticated attacks on EC2, ELB, CloudFront, AWS, Route53
- 24/7 response team access
- Protect against higher
- fees during usage spikes due to DDOS

## AWS WAF - Web Application Firewall

- protects web application from common web exploits (layer 7)
- Layer 7 HTTP
- Deploy on load balancer, gateway, cloudfront
- Define web ACL (web access control list):
    - Rules can include IP address, headers, body, strings
    - Protects from common attacks - SQL injection and cross-site scripting (xss)
    - Size constraints, geo-match (block countries)
    - Rate-based rules (to count occurrences of events) - for DDOS protection

## AWS Network Firewall

- Protect your entire amazon VPC
- From layer 3 to layer 7 protection
- Any direction you can inspect
    - VPC to VPC traffic
    - Outbound to internet
    - Inbound to internet
    - To & from direct connect & site-to-site VPN

## AWS Firewall Manager

- Manage all security rules in all accounts of an AWS Organisation
- Security policy: common set of security rules
    - VPC Security groups for EC2, application load balancer, etc…
    - WAF rules
    - AWS Shield Advanced
    - AWS Network Firewall
- Managing VPC security groups across multiple accounts in an organisation think FIREWALL MANAGER
- Rules are applied to new resources as they are created, good for compliance across all future accounts

## Penetration Testing on AWS

- AWS customers are welcome to carry out security assessments or penetration tests against their AWS infrastructure without prior approval for 8 services
    - EC2, NAT Gateways, ELB
    - RDS
    - CloudFront
    - Aurora
    - API Gateways
    - Lambda, Lambda Edge Functions
    - Lightsail resources
    - Elastic Beanstalk environments
- List can increase over time you wont be tested on that at the exam
- Prohibited activities
    - DNS zone walking via Amazon Route 53 Hosted Zones
    - Denial of Service (DOS), Distributed Denial of Service (DDOS), Simulated Dos, Simulated DDOS
    - Port flooding
    - Protocol flooding
    - Request flooding
- For any other simulated events, contact security team

## Encryption

- **At rest**: data is stored or archived on a device
    - On a hard disk, on a RDS instance, in S3 Glacier Deep Archive, etc.
    - Example: Encrypted at rest on EFS or Encrypted at rest on S3
- **In transit** (in motion): data being moved from one location to another
    - Transfer from on-premises to AWS, EC2 to DynamoDB, etc
    - Means data transferred on the network
- We want to encrypt data in **both** states to protect it
- Using **encryption keys**
- **AWS KMS** (Key Management Service)
    - AWS manages the encryption keys for us
    - Encryption Opt-in:
        - EBS volumes: encrypt volumes
        - S3 buckets: server-side encryption of objects
        - Redshift database, RDS: encryption of data
        - EFS drives: encryption of data
    - Encryption automatically enabled:
        - CloudTrail logs
        - S3 Glacier
        - Storage Gateway
    - KMS keys
        - Customer Managed Key:
            - Create, manage and used by the customer, can enable or disable
            - Possibility of rotation policy
            - Possibility to bring your own key
        - AWS Managed Key:
            - Created managed and used on the customers behalf by AWS
            - Used by AWS services (S3,EBS,Redshift)
        - AWS Owned Key:
            - Collection of CMKs that an AWS service owns and manages to use in multiple accounts
            - AWS can use those to protect resources in your account (but you can’t view the keys)
        - CloudHSM Keys (custom keystore)
            - Keys generated from your own CloudHSM hardware device
            - Cryptographic operations are performed within the CloudHSM cluster
- **CloudHSM**
    - CloudHSM → AWS provisions encryption hardware but we manage the encryption keys not AWS
    - Dedicated Hardware (HSM - Hardware Security Module)
    - HSM device is tamper resistant, FIPS 140-2 level 3 compliance

## AWS Certificate Manager (ACM)

- Lets you easily provision, manage and deploy SSL/TLS Certificates
- Used to provide in-flight encryption for your websites (HTTPS)
- Supports both public and private TLS certificates
- Automatic TLS certificate renewal
- Integration with
    - ELB
    - CloudFront distributions
    - APIs on API Gateway

## Secrets Manager

- Newer service, meant for storing secrets
- Capability to force rotation of secrets every X days
- Automate generation of secrets on rotation uses lambda
- Integration of RDS (MYSQL, PostgreSQL, Aurora)
- Secrets are encrypted using KMS
- Mostly meant for RDS integration

## Artifact

- Portal that gives customers on-demand access to AWS compliance documentation and AWS agreements
- Artifact Reports - allows you to download AWS security and compliance documents from third-party auditors, ISO certifications, Payment Card Industry (PCI)
- Artifact Agreements - allows you to review, accept and track the status of AWS agreements such as Businesss Associate Addendum (BAA)
- Can be used to support internal audit or compliance

## GuardDuty

- intelligent threat discovery to protect your AWS account
- Uses machine learning algorithms, anomaly detection, 3rd party data
- One click to enable (30 day trial), no need to install software
- Input data includes:
    - CloudTrail events log - unusual api calls, unauthorised deployments
    - VPC flow logs - unusual internal traffic, unusual IP address
    - DNS logs - compromised EC2 instances sending encoded data within DNS queries
    - Optional features - EKS audit logs, RDS and aurora, EBS, S3
- Can setup eventbridge rules to be notified in case of findings
- **Can protect against cryptocurrency attacks dedicated findings for it**

## Amazon Inspector

- Automated security assessments
- For EC2 instances
    - Leveraging the AWS system manager agent (SSM)
    - Analyse against unintended network accessibility
    - Analyse running OS against known vulnerabilities
- For Container images push to Amazon ECR
    - Assessment of container images as they are pushed
- Lambda Functions
    - Identifies software vulnerabilities in function code and package dependencies
    - Assessment of functions as they are deployed
- Reporting & integration with AWS Security hub
- Send findings to amazon Event Bridge
- What does it evaluate?
    - Only for EC2 instances, container images & lambda functions
    - Continuous scanning of the infrastructure only when needed
    - Package vulnerabilities
    - Network reachability (ec2)
    - A risk score is associated with all vulnerabilities for prioritisations

## **AWS Config**

- Helps with auditing and recording compliance of your AWS resources
- Records configuration and changes over time
- Possibility of storing the configuration data into S3 (Analysed by Athena)
- Questions that can be solved using AWS Config
    - Is there unrestricted SSH access to my security groups?
    - Do my buckets have any public access?
    - How has my ALB configuration changed over time?
- You can receive alerts (SNS notifications) for any changes
- AWS config is a per-region service
- Can be aggregated across regions and accounts
- AWS Config **Resource**
    - View compliance of a resource over time (red, green)
    - View configuration of a resource over time
    - View CloudTrail api calls if enabled

## Amazon Macie

- is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect sensitive data in AWS
- Macie helps identify and alert you to sensitive data, such as personally identifiable information (PII)
- Example: s3 bucket → Macie → amazon eventbridge → SNS/lambda

## AWS Security Hub

- Central security tool to manage security across several AWS accounts and automate security checks
- Integrated dashboards showing current security and compliance status to quickly take actions
- Automatically aggregates alerts in predefined or personal findings formats from various AWS services & partner tools:
    - Config
    - GuardDuty
    - Inspector
    - Macie
    - IAM Access Analyser
    - AWS Systems Manager
    - AWS Firewall Manager
- Must first enable AWS Config service

## Amazon Detective

- GuardDuty, Macie, security hub are used to identify potential security issues or findings
- Sometimes security findings require deeper analysis to isolate the root cause and take action - complex process
- Amazon detective
    - Analyse
    - Investigates
    - Quickly identifies the root cause of security issues
    - Suspicious activities (ML and graphs
- Automatically collects and processes events from VPC flow logs, CloudTrail, GuardDuty and create a unified view

## AWS Abuse

- report suspected AWS resources used for abusive or illegal purposes
- Abusive & prohibited behaviours are:
    - Spam - receiving undesired emails from AWS-owned Ip address, websites & forums
    - Port scanning - sending packets to your ports to discover the unsecured ones
    - Dos or DDOS attacks
    - Hosting objectionable or copyright content
    - Distributing malware
- Contact the AWS abuse team

## Root User Privileges

- root user = account owner
- Has complete access to all AWS services and resources
- do not use the root account for everyday tasks
- Actions that can be performed only by the root user:
    - Change account settings
    - Close your AWS account
    - Change or cancel your AWS support plan
    - Register as a seller in the reserved instance marketplace
    - Configure S3 bucket to enable MFA

## IAM Access Analyser

- Find out which resources are shared externally
    - S3 Bucket
    - IAM roles
    - KMS Keys
    - Lambda functions & layers
    - SQS queues
    - Secret Manager Secrets
- Define Zone of Trust = AWS account or AWS Organisation
- Access outside zone of trusts → findings

## Security & Compliance Summary

- Shared Responsibility
- Shield: DDOS Protection + 24/7 support for advanced
- WAF: Firewall to filter incoming requests based on rules
- KMS: Encryption keys managed by AWS
- CloudHSM: Hardware encryption, we manage encryption keys
- AWS certificate manager: provision, manage and deploy SSL/TLS certificates
- Artifact: get access to compliance reports such as PCI, ISO…
- GuardDuty: find malicious behavior with VPC, DNS and CloudTrail logs
- Inspector: find software vulnerabilities in EC2, ECR images, and lambda functions
- Network Firewall: Protect VPC against network attacks
- Config: track config changes and compliance against rules
- Macie: find sensitive data in amazon S3 buckets
- CloudTrail: Track API calls made by users within account
- Security hub: gather security findings from multiple AWS accounts
- Detective: find root cause of security issues
- AWS abuse: report to team for abusive illegal purposes
- Root user privileges:
    - Change account settings
    - Close your AWS account
    - Change or cancel your AWS support plan
    - Register as seller in the reserved instance marketplace
- IAM Access Analyser: identify which resources are shared externally
- Firewall Manager: manage security rules across an organisation(WAF, Shield…)

---