                              AWS EventBridge Real-Time Notification Architecture

<p align="center">
  <img src="00_AWS_Architecture_Diagram.png" alt="AWS Architecture Diagram">
</p>

Project Overview

This project demonstrates how to build an automated, event-driven monitoring and alerting system using AWS EventBridge and Amazon Simple Notification Service (SNS). The primary objective is to capture real-time infrastructure events—specifically Amazon S3 object creation/deletion and Amazon EC2 instance state changes—and dispatch instant alert notifications to designated email endpoints.

Services Used

Amazon EventBridge
Amazon S3 (Simple Storage Service)
Amazon EC2 (Elastic Compute Cloud)
Amazon SNS (Simple Notification Service)

Configuration Details

| Parameter | Configuration |
| :--- | :--- |
| AWS Region | Europe (Ireland) `eu-west-1` |
| EC2 Instance | `t3.micro` (Name: `MY_SERVER`) |
| S3 Bucket | `amazon-bucket-eb` |
| Event Bus | `default` |
| EventBridge Rule | `my_rule` |
| SNS Topic Name | `Public_Topic` |
| SNS Subscriptions | `EMAIL`, `EMAIL-JSON` |

Step 1 - Provision Resources

Launched an Amazon EC2 instance named `MY_SERVER` (`t3.micro`) in the `eu-west-1b` Availability Zone and created an Amazon S3 bucket named `amazon-bucket-eb` to serve as event sources.

Step 2 - Configure the Notification Layer (SNS)

Created an Amazon SNS Topic named `Public_Topic` (Standard Topic) and configured two confirmed email subscriptions (`EMAIL` and `EMAIL-JSON`) to receive automated alerts upon event triggering.

Step 3 - Set Up EventBridge Rules

Created an EventBridge Rule named `my_rule` on the `default` event bus. Configured event pattern filtering for:

Amazon S3: Object creation (`PutObject`) and deletion (`DeleteObject`) events on `amazon-bucket-eb`.

Amazon EC2: Instance state-change notifications for `MY_SERVER`.

Targeted the SNS topic `Public_Topic` with an IAM execution role granting EventBridge permissions to publish messages to SNS.

Step 4 - Trigger Events and Verify Endpoints

Simulated infrastructure events to test end-to-end routing:

S3 Event Verification: Uploaded and deleted files (`2,3.pdf`, `Aditya_Resume-1.pdf`) in `amazon-bucket-eb` to generate S3 event payloads.

EC2 Event Verification: Stopped `MY_SERVER` to generate an EC2 state-change notification (`stopped`).

Email Verification: Received automated JSON alert payloads directly in the subscribed inbox detailing both S3 object events and EC2 state changes.

Project Verification & Screenshots

Step 01 - Architecture Diagram:

![Architecture Diagram](00_AWS_Architecture_Diagram.png)

Step 02 - EventBridge Target Configuration:

![EventBridge Targets](01_EventBridge_Rule_Targets.png)

Step 03 - EventBridge Rules Overview:

![EventBridge Rules Overview](02_EventBridge_Rules_Overview.png)

Step 04 - Monitored S3 Bucket (amazon-bucket-eb):

![S3 Bucket Setup](03_S3_Bucket_Setup.png)

Step 05 - Configured SNS Topic & Subscriptions:

![SNS Topic Details](04_SNS_Topic_Details.png)

Step 06 - Monitored EC2 Instance (MY_SERVER):

![EC2 Instance Running](05_EC2_Instance_Running.png)

Step 07 - Confirmed SNS Subscription Endpoint:

![SNS Email Subscription](06_SNS_Email_JSON_Subscription.png)

Step 08 - Target Configuration & IAM Execution Role:

![Target Configuration](07_EventBridge_Target_Configuration.png)

Step 09 - S3 Bucket Object Activity:

![S3 Uploaded Objects](08_S3_Uploaded_Objects.png)

Step 10 - S3 Event Email Notification Received:

![S3 Email Alert](09_Email_Alert_S3_Events.jpg)

Step 11 - EC2 State Change Email Notification Received:

![EC2 Email Alert](10_Email_Alert_EC2_State_Change.png)

Testing & Verification

Confirmed that AWS EventBridge intercepts real-time S3 object events and EC2 instance state changes on the `default` bus.

Verified seamless event routing from EventBridge rules to Amazon SNS topics using IAM roles.

Validated automated alert delivery of formatted JSON payloads across multiple email endpoints.

Learning Outcomes

Engineered an event-driven monitoring system using serverless AWS components.

Configured EventBridge event patterns to capture multi-service resource events.

Managed Amazon SNS topics and email subscription endpoints.

Applied proper IAM policies to permit EventBridge target invocation.

Author

ADITYA MANIVANNAN

AWS Cloud | DevOps Engineer
