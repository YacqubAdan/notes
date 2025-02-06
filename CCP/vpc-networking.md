# VPC & Networking

Created by: Yacqub 
Created time: October 17, 2024 6:28 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

## VPC Overview

- VPC, Subnets, Internet Gateways & NAT gateways
- Security groups, Network ACL (NACL), VPC Flow Logs
- 1, 2 questions in exam
- Default VPC

## IP Addresses

- IPv4 - Internet Protocol version 4 (4.3 billion addresses)
    - Public IPv4 - can be used on the internet.
        - Ec2 instance gets a new public IP address every time you stop then start it (default)
    - Private IPv4 - can be used on private networks (LAN) such as internal AWS networking (e.g 192.168.1.1)
        - Stays the same for EC2 instance lifetime
    - Elastic IP - allows you to attach fixed public IPv4 address to EC2 instance
    - Note: all public IPv4 on AWS will be charged at $0.005 per hour (including EIP)
        - Free tier: 750 hours usage per month
    - IPv6 - internet protocol version 6 (3.4 x 10^38 Addresses)
        - Every IP address is public in AWS(no private range)
        - Example: 2001:db8:3333:444:cccc:dddd:eeee:ffff
        - Free

## VPC & Subnets

- Virtual Private Cloud: private network to deploy your resources (regional resources)
    - Linked to region
- Subnets: allows you to partition your network inside your VPC (availability zone resource)
- Public subnet: accessible from the internet
- Private subnet: not accessible from the internet
- To define access to the internet and between subnets, we use Route Tables.

## VPC Diagram

- AWS Cloud → Region → VPC → VPC CIDR Range(Ip addresses allowed) → across 2,3 availability zones → each availability zone can have a private and public subnet → can deploy EC2 in each of these subnets

## Internet Gateway & NAT Gateways

- internet gateways help our VPC instances connect with the internet
- Public subnet will have a route to the internet gateway
- NAT Gateways (AWS-managed) & NAT instances (self-managed) allows your instances in your **private subnets** to access the internet while remaining private (updates etc)

## Network ACL & Security Groups within VPC

- NACL (Network ACL) - first line of defence firewall which controls traffic from and to the subnet (**subnet level)**
    - **Allow** and **Deny** rules
    - Are attached at the subnet level
    - Rules only include IP addresses
    - Before it reaches EC2 instance
- Security Groups - Firewall that controls traffic to and from an EC2 instance
    - Can only have **allow** rules
    - Rules include IP addresses and other security

## VPC Flow log

- capture information about IP traffic going into your interface:
    - VPC flow logs
    - Subnet flow logs
    - Elastic Network Interface flow logs
- Helps to monitor and troubleshoot connectivity issues
    - subnets to internet
    - Subnets to subnets
    - Internet to subnets
- Captures network information from AWS managed interfaces too: Elastic Load Balancers, ElastiCache, Aurora, RDS, etc…
- VPC Flow logs data can go to S3, CloudWatch Logs and Kinesis data firehose
- VPC Peering
    - Connect two VPC privately using AWS Network
    - Make them behave as if they were in the same network
    - Must not have overlapping CIDR (Ip addresses)
    - Not transitive connection (must be established for each VPC that need to communicate with each other)

## VPC Endpoints

- Endpoints allow you to connect to AWS services using a private network instead of the public www network
    - Better security
    - Less latency
- VPC Endpoint Gateway: S3 & DynamoDB only
- VPC Endpoint Interface: the rest e.g CloudWatch

## AWS PrivateLink (VPC Endpoint Services)

- Most secure and scalable way to expose a service to 1000s of VPCs
- Does not require VPC peering, internet gateway, Nat, route tables…
- Requires a network load balancer (service VPC) and ENI (Customer VPC)

## Site to Stie VPN & DirectConnect

- Site to Site VPN
    - Connect an on-premises VPN to AWS
    - The connection is automatically encrypted
    - Goes over the public internet
- Direct Connect (DX)
    - Establish a physical connection between on-premise and AWS
    - The connection is private secure and fast
    - Goes over a private network
    - Takes at least a month to establish
- Site to site VPN
    - On premise:Must use a customer gateway customer gateway (CGW)
    - AWS: Must use a Virtual Private Gateway (VGW)

## AWS Client VPN

- Connect from your computer using OpenVPN to your private network in AWS and on-premises
- Allow you to connect to your EC2 instances over a private IP
- Goes over public internet

## Transit gateway

- for having transitive peering between thousands of VPC and on-premise, hub-and-spoke (star) connections
- One single gateway that provide this functionality
- Works with direct connect gateway, VPN connections

### VPC Summary

- VPC: virtual private cloud
- Subnet: tied to an AZ, network partition of the VPC
- Internet gateway: at the VPC level, provide internet access
- NAT Gateway/Instances: give internet access to private subnet
- NACL: stateless, subnet rules for inbound and outbound traffic
- Security Groups: stateful, operate at the EC2 instance level
- VPC Peering: connect two VPC with non overlapping Ip addresses. Non transitive
- Elastic IP - fixed public IPv4 ongoing cost if not using
- VPC Endpoints: private access to AWS Services within VPC
- PrivateLink: Private connection to service in 3rd party VPC
- VPC Flow logs: network traffic logs
- Site to Site VPN: VPN over public internet between on-premise DC and AWS
- ClientVPN: OpenVPN connection from your computer into VPC
- Direct Connect: direct connection to AWS
- Transit Gateway: connect thousands of VPC and on-premises networks together

---