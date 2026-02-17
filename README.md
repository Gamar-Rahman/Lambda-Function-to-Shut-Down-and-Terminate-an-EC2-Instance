# Lambda-Function-to-Shut-Down-and-Terminate-an-EC2-Instance
This lab demonstrates how to create and test an AWS Lambda function that can:  
🛑 Stop (shut down) an EC2 instance 
❌ Terminate an EC2 instance

📌 Lab Overview
The lab also emphasizes secure IAM configuration, least privilege access, and Lambda test events for safe validation before production deployment.

🏗 Architecture Overview

Components used:

AWS Lambda

Amazon EC2

IAM Role with least privilege

CloudWatch Logs

🎯 Lab Objectives
By completing this lab, you will:

✔ Create a Lambda function using Python (boto3)
✔ Attach least-privilege IAM permissions
✔ Use test events for validation
✔ Shut down an EC2 instance programmatically
✔ Terminate an EC2 instance programmatically
✔ Monitor execution via CloudWatch

🛠 Step 1 – IAM Policy (Least Privilege)
Create a custom IAM policy:

Step 2 – Lambda Function: Shut Down Instance
import boto3
import json

ec2 = boto3.client('ec2')

def lambda_handler(event, context):
    instance_id = event['instance_id']
    
    response = ec2.stop_instances(
        InstanceIds=[instance_id]
    )
    
    return {
        'statusCode': 200,
        'body': json.dumps(f'Instance {instance_id} is stopping.')
    }

Step 3 – Lambda Function: Terminate Instance

lambda/terminate_instance.py

import boto3
import json

ec2 = boto3.client('ec2')

def lambda_handler(event, context):
    instance_id = event['instance_id']
    
    response = ec2.terminate_instances(
        InstanceIds=[instance_id]
    )
    
    return {
        'statusCode': 200,
        'body': json.dumps(f'Instance {instance_id} is terminating.')
    }


Step 4 – Test Event

lambda/test-event.json

{
  "instance_id": "i-0123456789abcdef0"
}
Replace with your real EC2 instance ID.

📊 Step 5 – Monitoring with CloudWatch

After execution:

Open CloudWatch

Navigate to Log Groups

Select your Lambda function log group

Review execution logs

🔐 Security Considerations

Use least privilege IAM

Restrict by specific instance ARN

Enable CloudTrail for API auditing

Consider adding approval workflow before termination

Log all automation activity

🚨 Real-World Use Cases

Automatic shutdown of unused instances

Cost optimization automation

Incident response automation

Containment during security breach

DevSecOps infrastructure governance

☁️ Cloud Security Relevance

This lab demonstrates:

Infrastructure automation

Cloud resource control

Secure serverless execution

IAM permission design

Event-driven architecture

Strong foundation for:

Cloud Security Engineer

DevSecOps Engineer

SOC Automation Engineer

Incident Response Engineer

📦 Optional Advanced Enhancements

You can improve this lab by adding:

Tag-based filtering (only stop instances with specific tag)

Scheduled shutdown via EventBridge

Slack/Email notification

Multi-account support

Approval-based termination workflow
