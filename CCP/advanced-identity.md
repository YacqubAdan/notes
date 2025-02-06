# Advanced Identity

Created by: Yacqub 
Created time: November 4, 2024 7:01 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

## AWS STS (Security Token Service)

- Enables you to create temporary, limited-privileges credentials to access your AWS resources
- Short term credentials: you configure expiration period
- Use cases:
    - Identity federation: manage user identities in external systems, and provide them with STS tokens to access AWS resources
    - IAM Roles for cross/same account access
    - Provide temporary credentials for EC2 instances to access AWS resources
- Any time in exam you see temporary limited credentials to AWS think AWS STS

## Amazon Cognito

- identity for your web and mobile applications users
- Instead of creating IAM user you create a user in Cognito
- Amazon Cognito → own database of users → mobile and web apps would have integrated login with Cognito
- Login with Facebook, Google, Twitter
- This is to manage users on web

## Microsoft Active Directory (AD)

- Found on any windows server with AD Domain Services
- Database of objects: User, accounts, computers, printers, file shares, security groups
- Centralised security management, create account assign permission
- This is how you can have many machines with the same user and password for example companies
- **AWS Directory Services**
    - AWS Managed Microsoft AD
        - Create own AD in AWS, manage users locally
        - Establish “trust” connections with your on-premise AD
    - AD connector
        - Directory Gateway to redirect to on premise AD, supports MFA
        - Users are managed on the on-premise AD
    - Simple AD
        - AD-compatible managed directory on AWS
        - Cannot be joined with on-premise AD

## AWS IAM Identity Center (Successor to AWS Single Sign-On)

- One login for all your
    - AWS accounts in AWS Organisations
    - Business cloud applications
    - Ec2 windows Instances
- Identity providers
    - Built in identity store in IAM Identity center
    - 3rd party: Active Directory AD, OneLogin, Okta

---