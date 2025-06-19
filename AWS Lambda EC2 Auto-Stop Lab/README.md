# 🛑 myStopinator – AWS Lambda EC2 Auto-Stop Lab

## 📘 Description  
This lab demonstrates how to automate the shutdown of an EC2 instance using **AWS Lambda** triggered by **EventBridge (CloudWatch Events)** on a scheduled basis. This project strengthens serverless automation skills aligned with SOC, detection engineering, and cloud operations workflows.

---

## 🧠 Objectives

- Automatically stop an EC2 instance every minute  
- Learn how Lambda integrates with EventBridge  
- Use IAM roles for secure function execution  
- Monitor execution results through CloudWatch  
- Demonstrate infrastructure control and automation using Python (boto3)

---

## 📸 Screenshots & Explanations

### 1. What is AWS Lambda?
![Screenshot 2025-06-08 210034](https://github.com/user-attachments/assets/469289f8-957f-4747-a61f-88ddd7f297d5)

AWS Lambda is a serverless compute service provided by Amazon Web Services that allows you to run code without provisioning or managing servers. You simply upload your code, define the trigger, and Lambda takes care of the rest — from scaling to execution..

### 2. Lambda Function Setup – Initial Configuration
![Screenshot 2025-06-08 210335](https://github.com/user-attachments/assets/667a13a1-db27-4d33-8681-291ea8788dc0)
![Screenshot 2025-06-08 210354](https://github.com/user-attachments/assets/a164f7e3-487c-4b67-8888-7193003b481d)

Creating a new Lambda function from scratch named `myStopinator`, using the Python 3.11 runtime, x86_64 architecture, and assigning basic Lambda execution permissions.

### 3. Configuring an EventBridge Trigger for AWS Lambda
![Screenshot 2025-06-08 210528](https://github.com/user-attachments/assets/15491d5a-c799-4753-ae92-3e835570173a)
98iooooooooooooouy777hhhh1

This shows the configuration of an EventBridge trigger for an AWS Lambda funtion. A new rule is being created to invoke the function every minute based on the schedule expression. The schedule type ensures that this expression runs at a fixed rate (once per minute). 

### 4. Trigger View with EventBridge
![Screenshot 2025-06-08 210528](https://github.com/user-attachments/assets/ab66d1a8-ebe8-4baa-bf81-8f482281edf5)

**Caption:** Lambda function `myStopinator` is triggered by **EventBridge (CloudWatch Events)** for scheduled execution.

### 5. EventBridge Rule – Run Every Minute
![Screenshot 2025-06-08 210956](https://github.com/user-attachments/assets/cd280f63-ff30-4b09-928c-53bd7f65244d)

**Caption:** EventBridge rule created to run every 1 minute using `rate(1 minute)` schedule expression.

### 6. IAM Role Configuration – Lambda Permissions
![Screenshot 2025-06-08 211142](https://github.com/user-attachments/assets/e9bfbb32-d2f5-40de-9bff-c966767f3c59)

**Caption:** Custom IAM role `myStopinatorRole` provides Lambda with the necessary EC2 and logging permissions.

### 7. Lambda Function Creation Settings
![Screenshot 2025-06-08 211220](https://github.com/user-attachments/assets/6e83354c-f194-41f3-bdeb-413a319ede0e)

**Caption:** Lambda function setup screen with selected runtime (Python 3.11), x86_64 architecture, and role assignment.

### 8. AWS Lambda Landing Page
![Screenshot 2025-06-08 211409](https://github.com/user-attachments/assets/ad9cf83f-213a-4afa-ac93-25d39aadc4d7)

**Caption:** AWS Lambda console showing various supported runtimes. This project uses **Python** for script execution.

### 9. EC2 Console Showing Instance State
![Screenshot 2025-06-08 211458](https://github.com/user-attachments/assets/d45dfe26-cd0a-40c4-a94d-3778b7618a30)

**Caption:** EC2 dashboard shows instance `instance1` is transitioning from `running` to `stopping`, confirming Lambda worked.

### 10. Confirmation: Lambda Successfully Updated
![Screenshot 2025-06-08 211612](https://github.com/user-attachments/assets/7366ded4-ddae-49c9-a7f1-a6426e6c63bc)

**Caption:** Final deployment confirmation that the Lambda function `myStopinator` was successfully updated and is operational.

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
