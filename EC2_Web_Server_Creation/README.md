# Deploying a Public-Facing Web Server on AWS EC2 with Apache and User Data

## Description

This lab demonstrates how to launch an EC2 instance and configure it to act as a web server using Amazon Linux 2023. A user data script automates the installation and configuration of Apache (httpd), and the instance is placed in a custom VPC with a security group allowing inbound HTTP traffic. This exercise showcases foundational AWS skills in cloud provisioning, infrastructure security, and automated deployment.

---

## Objectives

- Create a custom VPC and public subnet
- Launch a t2.micro EC2 instance using Amazon Linux 2023
- Configure Apache HTTP server with a user data script
- Apply a security group allowing inbound HTTP (port 80)
- Validate server availability from the browser
- Monitor instance logs and metrics to verify success

---

## Technologies Used

- EC2 (Amazon Elastic Compute Cloud)
- Amazon Linux 2023
- Apache HTTP Server
- User Data (Bash scripting)
- Security Groups
- VPC/Subnet configuration
- CloudWatch logs and metrics

---

## Screenshots and Captions

### 1. Launch Instance Wizard – AMI and Instance Type  
This screenshot shows the selection of Amazon Linux 2023 AMI and t2.micro as the instance type, eligible for the AWS free tier.

![Screenshot 2025-06-08 193445](https://github.com/user-attachments/assets/a2c305da-8ac9-45e1-968c-8f7ff674e735)

---

### 2. Configure Networking – VPC and Subnet  
The EC2 instance is launched into a custom lab VPC and public subnet to allow internet access.

![Screenshot 2025-06-08 194408VPC](https://github.com/user-attachments/assets/e9f4f368-25aa-45f5-b50f-146c2cf6f620)


---

### 3. Configure Security Group – Web Server Access  
A new security group is created with a rule to allow HTTP traffic (Only for lab purposes) from any IPv4 address. Security groups on AWS act as a firewall at the instance level. 

![Screenshot 2025-06-08 194408SEC](https://github.com/user-attachments/assets/98da44b7-0523-4944-8acd-9e25c629d2b8)
![Screenshot 2025-06-08 200309](https://github.com/user-attachments/assets/7caa953f-d354-42c5-a37d-d25b1d0276a6)


### 4. Configure Instance Settings - Monitoring and Protection Options
Here we configure optional instance-level settings such as shutdown behavior, termination protection, and detailed monitoring. These settings help enhance control and reliability. In this case, many of the options are left as default for the purpose of the lab. 
![Screenshot 2025-06-08 194517](https://github.com/user-attachments/assets/3f5ab7b8-f281-4762-b25c-95aa00a6aebc)

---

### 5. Configure User Data Script  
User data is used to automatically install, start, and serve a simple HTML page via Apache on instance launch.

![Screenshot 2025-06-08 194730](https://github.com/user-attachments/assets/1a0a6706-ab11-4c7f-bf00-2067704ce070)

`**Script is shown at the bottom of this page**`

### 6. Instance Launched Successfully
![Screenshot 2025-06-08 194906](https://github.com/user-attachments/assets/4e92ce17-58ef-4cc4-9562-9fb0e3fc47ce)
![Screenshot 2025-06-08 195428](https://github.com/user-attachments/assets/565c1587-5543-4663-a6d8-c38532ee8f48)


### 7. Review Instance Boot Logs – Verifying Network Initialization
Here we review the system log for the EC2 instance to confirm successful boot and configuration. The log output shows that cloud-init completed and the instance correctly initialized its network interfaces, routes, and IPv4/IPv6 addressing. This step is useful for verifying that the user data script had a chance to run and that no errors occurred during startup.

![Screenshot 2025-06-08 195818](https://github.com/user-attachments/assets/ae820359-8989-4852-a99e-02003e7f760f)


```bash
#!/bin/bash
dnf install -y httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html

---



