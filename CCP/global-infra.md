# Leveraging the AWS Global Infrastructure

Created by: Yacqub 
Created time: October 12, 2024 3:38 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

### Why make a global Application?

- A global application is an application deployed in multiple geographies
- On AWS: this could be Regions and / or Edge Locations
- Decreased latency
    - Latency: time it takes a network packet to reach a server
    - E.g it takes time for a packet from Australia to reach UK
    - The closer your application the better the experience
- Disaster Recovery (DR)
    - If an entire AWS Region goes down (earthquake, storms, power shutdowns, politics)
    - You can fail-over to another region and have your app still work
- Attack protection: distributed global infrastructure is harder to attack

## Global AWS Infrastructure

- **Regions:** for deploying applications and infrastructure
- **Availability Zones:** Made of multiple data centers
- **Edge locations (Points of Preference):** for content delivery as close as possible to users

## Global AWS Services

- Global DNS: Route 53
    - Great to route users to the closest deployment with least latency
    - Great for disaster recovery
- Global content delivery Network (CDN): CloudFront
    - Replicate part of your application to AWS Edge Locations - decrease latency
    - Cache common requests - improved user experience and decreased latency
- S3 transfer acceleration
    - Accelerate global uploads & downloads into Amazon s3
- AWS Global Accelerator:
    - Improve global application availability and performance using the AWS global network

### Amazon Route 53 Overview

- Route53 is a Managed DNS (Domain Name System)
- DNS is a collection of rules and records which helps clients understand how to reach a server through URLs
- In AWS the most common records are:
    - [www.google.com](http://www.google.com) → 12.34.56.78 == A record (IPv4)
    - [www.google.com](http://www.google.com) → 2001:0db8:85a3:00000:8a2e == AAAA (IPv6)
    - [search.google.com](http://search.google.com) → [www.google.com](http://www.google.com) == CNAME:hostname to hostname
    - [example.com](http://example.com) → AWS resource == Alias (ELB, CloudFront, S3, RDS etc…)
- A record example using Route 53
    - Web browser, Application Server IPv4, Route 53
    - Web browser DNS request (to Route53) DNS responds with an IP
    - IP can then be used by our web browser
- Route 53 Routing Policies
    - Need to know them at a high-level for the cloud practitioner exam
        - Simple Routing Policy
            - No health Checks
            - Web browser will go into our DNS system and gets an IP address as a result
        - Weighted Routing Policy
            - Assigned weights to EC2 instances (70,20,10)
            - DNS will make sure clients have 70% on first 20% on second 10% on third (kind of like load balancing)
        - Latency Routing Policy
            - Global application, one in California and other in Australia and our users are all around the world
            - It will look at where users are located and redirected to the closer servers
        - Failover Routing Policy
            - Disaster Recover
            - Primary ec2 instance, failure ec2 instance
            - DNS System to perform health check on primary
            - If primary instance fails then redirected to failover.

## AWS CloudFront

- content Delivery Network (CDN)
- Improves read performance, content is cached at the edge
- Improves user experience
- 216 Points of Presence globally (edge locations)
- DDOS protection
- Origins
    - S3 Bucket
        - For distributing files and caching them at the edge
        - Enhanced security with CloudFront **Origin Access Control**
        - OAC is replacing Origin Access Identity (OAI)
        - CloudFront can be used as an ingress (to upload files to S3)
- Custom Origin HTTP
    - Application Load Balancer
    - EC2 Instance
    - S3 Website (must enable as static S3)
    - Any HTTP backend you want
- At a high level:
    - CloudFront edge level around the world
    - Connected to an Origin (S3 or HTTP)
    - Client connects to edge location sees if it has it in the cache if not → will retrieve from the origin and store as local cache for other client to get it quicker.
- CloudFront vs s3 Cross Region Replication
    - CF:
        - Global edge network
        - Files are cached for maybe a day
        - Great for static content that must be available everywhere
    - S3 Cross Region Replication
        - Must be setup for each region you want replication to happen
        - Files are updated in near real-time
        - Read only
        - Great for dynamic content that needs to be available at low efficiency

## Global Applications Summary

- Global DNS: Route 53
    - Great way to route users to the closest deployment with least latency
    - Great for disaster recovery strategies
- CloudFront
    - Global Content Delivery Network (CDN)
    - Replicate part of your application data into AWS Edge Locations
    - Cache common requests - improved user experience and decreased latency
- S3 Accelerator
    - Accelerate global uploads & downloads into Amazon S3
- AWS Global Accelerator
    - Improved global application availability and performance using the AWS global network
- AWS Outposts
    - Deploy outpost racks in your own data centers to extend AWS Servics
    - Hybrid
- AWS Wavelength
    - Bring AWS services to the edge of the 5G networks
    - Ultra low latency
- AWS Local Zones
    - Bring AWS resources (compute, database, storage) close to your users
    - Good for latency-sensitive application

---