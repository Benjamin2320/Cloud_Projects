# AWS Lambda EC2 Auto-Stop Lab

## Description  
This lab demonstrates the use of a Python-based AWS Lambda function to automatically stop a specific EC2 instance. The function is triggered on a scheduled basis using EventBridge CloudWatch Events, allowing for automated instance management without manual intervention. The lab covers the setup of the Lambda function, configuration of scheduling rules, and validation through CloudWatch metrics and EC2 instance state changes.

---

## Objectives

- Automatically stop an EC2 instance every minute  
- Learn how Lambda integrates with EventBridge  
- Use IAM roles for secure function execution  
- Monitor execution results through CloudWatch  
- Demonstrate infrastructure control and automation using Python (boto3)

---

## Lab

### 1. What is AWS Lambda?
![Screenshot 2025-06-08 210034](https://github.com/user-attachments/assets/469289f8-957f-4747-a61f-88ddd7f297d5)

AWS Lambda is a serverless compute service provided by Amazon Web Services that allows you to run code without provisioning or managing servers. You simply upload your code, define the trigger, and Lambda takes care of the rest — from scaling to execution..

### 2. Lambda Function Setup – Initial Configuration
![Screenshot 2025-06-08 210335](https://github.com/user-attachments/assets/667a13a1-db27-4d33-8681-291ea8788dc0)
![Screenshot 2025-06-08 210354](https://github.com/user-attachments/assets/a164f7e3-487c-4b67-8888-7193003b481d)

Creating a new Lambda function from scratch named `myStopinator`, using the Python 3.11 runtime, x86_64 architecture, and assigning basic Lambda execution permissions.

### 3. Configuring an EventBridge Trigger for AWS Lambda
![Screenshot 2025-06-08 210528](https://github.com/user-attachments/assets/15491d5a-c799-4753-ae92-3e835570173a)

This shows the configuration of an EventBridge trigger for an AWS Lambda funtion. A new rule is being created to invoke the function every minute based on the schedule expression. The schedule type ensures that this expression runs at a fixed rate (once per minute). 

### 4. Automating EC2 Shutdowns with Python in AWS Lambda
![Screenshot 2025-06-08 210956](https://github.com/user-attachments/assets/4de53a1f-caa8-4298-9ba0-0118c7645945)
![Screenshot 2025-06-08 211142](https://github.com/user-attachments/assets/cff44676-e4de-4b09-9e79-a6b909370044)

This displays an AWS Lambda function named "myStopinator" that is set up to stop EC2 instances using the boto3 library with Python. The code defines the region and instance ID, creates an EC2 client, and uses the stop_instances method to shut down tyhe specified instance. 

### 5. CloudWatch Monitoring
![Screenshot 2025-06-08 211220](https://github.com/user-attachments/assets/a3b5c586-ae9f-41c3-8241-d75838b34ace)

This screenshot shows the monitoring tab for the myStopinator Lambda function. CloudWatch metrics are used to confirm that the function has executed successfully on schedule. Key metricsa such as Invocation, Duration, and Success Rate provide visibility into the function's behavior and performance over time.  

### 6. EC2 Console Showing Instance State
![Screenshot 2025-06-08 211612](https://github.com/user-attachments/assets/9d413dd7-be8f-41e0-9ab7-55737a2db949)

**Caption:** EC2 dashboard shows instance 'instance1' is transitioning from `running` to `stopping`, confirming Lambda worked.

---

## 🐍 Lambda Function Code

```python
import boto3

region = 'us-east-1'
instances = ['i-02e724a266321b282']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.stop_instances(InstanceIds=instances)
    print('Stopped your instances: ' + str(instances))
