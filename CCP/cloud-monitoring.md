# Cloud Monitoring

Created by: Yacqub 
Created time: October 16, 2024 5:37 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

## Amazon CloudWatch Metrics

- CloudWatch provides metrics for every service in AWS
metric is a variable to monitor (CPU, NetworkIn…)
- Metrics have timestamps
- Can create CloudWatch dashboards of metrics
- Important Metrics
    - Ec2 instances: CPU Utilisation, Satus checks, Network
        - every 5 mins by default metrics
        - Option for detailed monitoring every minute
    - EBS Volume: Disk Read/Writes
    - S3 Buckets: bucketsizebytes, numberofobjects, allrequests
    - Billing: total estimated charge
    - Service limits: how much you’ve been using a service API
    - Custom metrics

## CloudWatch Alarms

- Used to trigger notifications for any metric
- Alarm actions…
    - Auto scaling: increase or decrease EC2 instances ‘desired’ count
    - EC2 Actions: stop, terminate, reboot or recover an EC2 instance
    - SNS notifications: send a notification into an SNS topic
- Various options (sampling, %, max,min, etc…)
- Can choose the period on which to evaluate an alarm
- Example: create a billing alarm on the CloudWatch billing metric
- Alarm States: OK. INSUFFICIENT_DATA,ALARM

## Amazon CloudWatch Logs

- CloudWatch Logs can collect log from:
    - Elastic beanstalk: collection of logs from application
    - ECS: collection from containers
    - AWS Lambda: collection from function logs
    - CloudTrail based on filter
    - CloudWatch log agents: on EC2 machines or on-premise servers
    - Route53: Log DNS queries
- Enables real-time monitoring of logs
- Adjustable for retention (1 week, 30 days etc…)
- For EC2
    - Default no logs from your EC2
    - You need to create CloudWatch agent on EC2 to push the log files you want
    - Make sure IAM permissions are correct
    - The CloudWatch log agent can be setup on-premises too

## Amazon EventBridge (formally known as CloudWatch Events)

- Schedule: Cron jobs (scheduled scripts)
    - schedule every hour → trigger lambda function
- Event Patterns: Event rules to react to a service doing something
    - IAM Root Sign in event → SNS Topic with Email notification
- Trigger lambda functions, send SQS/SNS messages…
- These are default event bus - based on AWS services
- Partner Event Bus - react to events happening outside of AWS
    - Partners of AWS
        - Zendesk
        - DataDog
- Custom Apps - Custom Event Bus
- Schema Registry: model event schema
- Archive events: sent to an event bus
    - Replay archived events
- Server-less service

## AWS CloudTrail

- provides governance, compliance and audit for you AWS Account
- CloudTrail is enabled by default
- Get an history of events / API calls made within your AWS Account by:
    - Console
    - SDK
    - CLI
    - AWS Service
- Can put logs from CloudTrail into CloudWatch Logs or S3
- A trail can be applied to all regions (default) or a single region
- If a resource is deleted in AWS, investigate CloudTrail first!
- Any time API is to be looked up its CLOUD TRAIL

## AWS X-Ray

- Debugging in production, the good old way:
    - Test locally
    - Add log statements everywhere
    - Re-deploy in production
- log formats differ across applications and log analysis is hard.
- Debugging: one big monolith ‘easy’, distributed services ‘hard’
- Enter AWS X-Ray
    - Tracing and visual analysis of our applications
    - See performance, where its failing
- Advantages
    - Troubleshooting performance (bottlenecks)
    - Understand dependencies in a microservice architecture
    - Pinpoint service issues
    - Review request behaviour
    - Find errors and exceptions
    - Are we meeting time SLA
    - Where am I throttled?
    - Identify users that are impacted

## Amazon CodeGuru

- Machine Learning powered service for automated code reviews and application performance recommendations
- Provides two functionalities
    - CodeGuru reviewer: automated code reviews for static code analysis (development)
    - CodeGuru profiler: visibility/recommendations about application performance during runtime (production) and cost improvements
- Code guru reviewer
    - Looks at your commits and tells lines of codes that have bugs, vulnerabilities
    - Example: common coding best practices. Resource leaks, security, validation
    - Uses machine learning and automated reasoning
    - Hard-learned lessons across millions of code reviews
    - Supports java and python
- code guru profiler
    - Helps understand runtime behaviour of your application
    - Example: identify if your application is consuming excessive CPU capacity on a logging routine
    - Features:
        - Identify remove code inefficiencies
        - Improve application performance
        - Decrease compute costs
        - Provides heap summary
        - Anomaly detection
    - Support applications running on AWS or on-premise
    - Minimal overhead on application

## AWS HealthDashboard

- Service history
    - Shows all regions, all services health
    - Shows historical information for each day
    - Has an RSS feed you can subscribe to
    - Previously called Service Health Dashboard
- Your Account
    - Previously called Personal Health Dashboard
    - Provides alerts and remediation guidance when AWS is experiencing events that may impact you.
    - Displays general status of AWS services, personalized view into the performance and availability of the services underlying your resource
    - Relevant and timely information.
    - Proactive notification
    - Can aggregate data from an entire AWS Organisation
    - Global service
    
    ## Monitoring Summary
    
    - CloudWatch
        - Metrics: monitor the performance of AWS services and billing metrics
        - Alarms: automate notification, perform EC2 action, notify to SNS based on metric
        - Logs: collect log files from EC2 instances, servers, Lambda
        - Events: react to events in AWS or trigger a rule on a schedule
        - CloudTrail: audit API calls made within your AWS account
        - CloudTrail Insights: automated analysis of your CloudTrail Events
        - X-ray: trace requests made through your distributed applications
        - AWS health dashboard: status of all AWS services across all regions
        - AWS Account Health Dashboard: events that impact your infrastructure
        - CodeGuru: automated code reviews and application performance recommendations

---