AWS Services Used

Amazon EC2
Amazon VPC
Amazon CloudWatch
Amazon SNS
Security Groups
Internet Gateway
Route Tables


Project Objectives
Create a custom VPC and networking components
Launch an EC2 instance in a public subnet
Monitor EC2 CPU utilization using CloudWatch
Create CloudWatch Alarms
Configure SNS email notifications
Generate CPU load using the Stress utility
Validate alarm triggering and notification delivery
Network Configuration
VPC
Resource	Configuration
VPC Name	MyMonitoringVPC
CIDR Block	10.0.0.0/16
Public Subnet
Resource	Configuration
Subnet Name	PublicSubnet
CIDR Block	10.0.1.0/24
Internet Gateway
Resource	Configuration
Name	MyIGW
Route Table
Destination	Target
0.0.0.0/0	Internet Gateway
EC2 Configuration
Parameter	Value
Instance Name	cloudwatch-test
Instance Type	t3.micro
AMI	Amazon Linux 2023
Key Pair	cloudwatch
Security Group	cloudwatch-sg
Security Group Rules
Inbound Rules
Type	Port	Source
SSH	22	My IP
Outbound Rules
Type	Destination
All Traffic	0.0.0.0/0
SNS Configuration
Topic
Parameter	Value
Topic Name	EC2-Alerts
Type	Standard
Subscription
Parameter	Value
Protocol	Email
Endpoint	User Email
CloudWatch Alarm Configuration
Parameter	Value
Alarm Name	HighCPUAlarm
Metric	CPUUtilization
Statistic	Average
Period	5 Minutes
Threshold	Greater Than 70%
Evaluation Periods	1
Action	SNS Notification
Generating CPU Load

Install Stress Utility:

sudo dnf install stress -y

Verify Installation:

stress --version

Generate CPU Utilization:

stress --cpu 2 --timeout 900

This command creates high CPU utilization for 15 minutes, allowing CloudWatch to collect metrics and evaluate the alarm.

Monitoring Results
CloudWatch Metrics

Observed CPU utilization reaching approximately:

98%
Alarm Lifecycle
INSUFFICIENT_DATA
          ↓
         OK
          ↓
       ALARM
Notification Flow
EC2 CPU Spike
      ↓
CloudWatch Metric
      ↓
CloudWatch Alarm
      ↓
SNS Topic
      ↓
Email Alert

Skills Demonstrated
AWS Networking Fundamentals
Amazon EC2 Administration
Amazon CloudWatch Monitoring
Amazon SNS Messaging
Linux System Administration
Troubleshooting and Alerting
Cloud Operations


Outcome

Successfully implemented a cloud monitoring and alerting solution using Amazon CloudWatch and Amazon SNS, enabling proactive monitoring of EC2 resources and automated notification of operational events.
