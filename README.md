# Simple-Monitoring-and-Notification-System-in-AWS-
This project demonstrates how to set up a simple monitoring and notification system in AWS using EC2, SNS (Simple Notification Service), and CloudWatch.It includes steps to create an EC2 instance, configure SNS for email notifications, and set up a CloudWatch alarm to monitor CPU utilization.

## Prerequisites

- An AWS account with necessary permissions to create EC2 instances, SNS topics, and CloudWatch alarms.
- An email address for receiving notifications.

## Steps

### 1. Create an EC2 Instance

1. Launch an EC2 `t2.micro` spot instance.
2. Connect to the instance using **EC2 Instance Connect**.
3. Install `stress-ng` to simulate CPU load:
   ```bash
   sudo yum install -y stress-ng
   ```

---

### 2. Configure SNS (Simple Notification Service)

1. Go to the **Simple Notification Service** in the AWS Management Console.
2. Delete any existing topics and subscriptions created earlier (if applicable).
3. Create a new SNS topic with the name `ID_topic2`.
4. Create a new subscription and provide your email address.
5. Confirm the subscription by clicking the link sent to your email.

---

### 3. Set Up CloudWatch Alarm

1. Go to **CloudWatch** in the AWS Management Console.
2. Delete any old alarms created earlier (if applicable).
3. Create a new alarm:
   - Select **Alarms** > **All Alarms** > **Create Alarm**.
   - Choose **Select Metric** and search for your EC2 instance ID.
   - Select **EC2 Per-Instance Metrics** and choose **CPU Utilization**.
   - Set the period to **1 minute**.
   - Set the condition to **CPU Utilization >= 40%** and click **Next**.
   - For actions, select **Send notification to** and choose your SNS topic from the dropdown.
   - Name the alarm and click **Create Alarm**.

---

### 4. Test the Setup

1. Connect to your EC2 instance and run the following command to simulate CPU load:
   ```bash
   stress-ng --cpu 1 --cpu-method matrixprod --timeout 300s
   ```
2. Open another terminal window and connect to the instance using **EC2 Instance Connect**.
3. Run the `top` command to monitor CPU usage in real-time:
   ```bash
   top
   ```
4. Once the CPU utilization crosses 40%, you should receive an email notification via SNS.

---

## Conclusion

This project provides a basic framework for monitoring AWS resources and setting up notifications based on predefined metrics. You can extend this setup to monitor other metrics or integrate additional AWS services as needed.

---
