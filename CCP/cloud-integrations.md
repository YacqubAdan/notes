# Cloud Integrations

Created by: Yacqub 
Created time: October 15, 2024 7:28 PM
projects: Study for Certified Cloud Practitioner (https://www.notion.so/Study-for-Certified-Cloud-Practitioner-5293c4b3d04743559817d1ef5c77b407?pvs=21)

## Amazon SNS

- The ‘event publishers’ only sends message to one SNS topic
- As many ‘event subscribers’ as we want to listen to the SNS topic notifications
- Each subscriber to the topic will get all the messages
- Up to 12M subscriptions per topic 100k topics limit
- SNS → publish → Subscribers (SQS, Lambda, Kinesis Data Firehose)

## Amazon MQ

- SQS, SNS are ‘cloud native’ services: proprietary protocols from AWS
- Traditional applications running from on-premise may use open protocols such as: MQTT, AMQP, STOMP, Openwire, WSS
- When migrating to cloud may not want to re-engineer the app to use SQS and SNS we can use amazon MQ
- Managed message broker for
    - RabbitMQ
    - ActiveMQ
- Doesn’t scale as much as SQS/SNS
- MQ may have surver issues, can run in multi-as with failover
- MQ has queue features (SQS) and topic features (SNS)

## Cloud Integrations Summary

- SQS
    - Queue service in AWS
    - Multiple producers, messages are kept up to 14 days
    - Multiple consumers share the read and delete messages when done
    - Used to decouple applications in AWS
- SNS
    - Notification service in AWS
    - Subscribers: email, lambda, SQS, HTTP, Mobile
    - Multiple subscribers: sns will send to all of them
    - No message retention
- Kinesis: real time data streaming persistence and analysis
- Amazon MQ: managed message broker for ActiveMQ and RabbitMQ in the cloud

---