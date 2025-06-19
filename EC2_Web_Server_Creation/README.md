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

### 2. Configure Instance – Name and Tags  
The instance is named "Web Server" to reflect its purpose.
![Screenshot 2025-06-08 194408](https://github.com/user-attachments/assets/b177d896-948d-4170-a90c-21d29c02f090)


---

### 3. Configure Networking – VPC and Subnet  
The EC2 instance is launched into a custom lab VPC and public subnet to allow internet access.

![Network Settings](../images/network-settings.png)

---

### 4. Configure Security Group – Web Server Access  
A new security group is created with a rule to allow HTTP traffic (Only for lab purposes) from any IPv4 address. Security groups on AWS act as a firewall at the instance level. 

![Screenshot 2025-06-08 194408](https://github.com/user-attachments/assets/3cd8d001-ca44-4e84-ab89-32f744d975a1)
![Screenshot 2025-06-08 200309](https://github.com/user-attachments/assets/d1696da1-6979-4076-ba3d-f4799792286d)


---

### 5. Configure User Data Script  
User data is used to automatically install, start, and serve a simple HTML page via Apache on instance launch.
![Screenshot 2025-06-08 194730](https://github.com/user-attachments/assets/1a0a6706-ab11-4c7f-bf00-2067704ce070)

```bash
#!/bin/bash
dnf install -y httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
