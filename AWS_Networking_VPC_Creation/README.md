# AWS Networking: VPC, Subnets, Routing, and Web Server Deployment

This lab demonstrates how to manually create a Virtual Private Cloud (VPC) on AWS from scratch, including all foundational networking components such as subnets, route tables, gateways, and security groups. The goal is to design a segmented and secure cloud network environment suitable for hosting a web server, while gaining hands-on experience with AWS networking components relevant to SOC, NOC, and cloud security roles.

---

## Lab Objectives

- Create a custom VPC with defined CIDR blocks
- Set up public and private subnets across availability zones
- Establish routing using route tables and gateways
- Configure security groups for controlled access to EC2
- Launch a web server instance in the public subnet with HTTP access
- Verify networking and connectivity using system logs

---

## Overview

Amazon Virtual Private Cloud (VPC) is a networking service in AWS that enables users to create isolated, customizable networks in the cloud. With a VPC, users can define their own IP address ranges, create public and private subnets, configure route tables, and attach internet or NAT gateways to control traffic flow.
As part of AWS’s Infrastructure as a Service (IaaS) offerings, VPC provides foundational network control, allowing organizations to build secure, scalable environments for deploying cloud-based resources such as virtual machines, databases, and applications. It plays a critical role in cloud architecture, offering flexibility and security for both development and production workloads.

### 1. VPC Homepage

![Screenshot 2025-06-01 213514](https://github.com/user-attachments/assets/8e3c5281-2755-4f11-8c79-b6d45fbdcebb)

---

### 2. Defining Subnet Structure and CIDR Ranges

Here we configure a public and private subnet CIDR block for our custom VPC, enabling DNS resolution and hostnames to support internal name resolution and AWS service discovery. We also opt for NAT gateway deployment in a single availability zone, allowing private subnet resources to reach the internet without being directly exposed.

**Other settings configured in this step but not shown here include:**

- **IPv4 CIDR block**: We defined the main VPC range (`10.0.0.0/16`) earlier in the wizard.
- **Internet Gateway**: Automatically created and attached to allow public subnet access.
- **Elastic IP allocation**: Reserved for NAT gateway internet traffic.
- **Tagging resources**: Each component (subnets, gateways, route tables) was tagged for easier identification and automation.
  
![Screenshot 2025-06-01 213650](https://github.com/user-attachments/assets/0d697812-39af-4f7e-b6db-51861d98ebd0)

---

### 3. VPC Resource Provisioning in Progress

Here we review the VPC creation workflow where AWS provisions all selected networking components. This includes the creation of the VPC, subnets, internet and NAT gateways, route tables, and elastic IPs.

![Screenshot 2025-06-01 213731](https://github.com/user-attachments/assets/5e844b2e-8df2-43f3-a9f1-7ab93a056501)

---

### 4. Visualizing the VPC Topology with the Resource Map

Here we review the AWS VPC resource map to confirm successful deployment of key components. This visual snapshot shows the VPC, associated public and private subnets, route tables, and network gateways. It provides a high-level view of how traffic flows through the environment and verifies the relationships between subnets, routing policies, and external access points.

![Screenshot 2025-06-01 213924](https://github.com/user-attachments/assets/15b0339d-46f6-4fb4-83d7-af7b1fe86d29)

---

### 5. Subnet and Route Table Association

Here we manage explicit subnet associations for custom route tables. The private subnet is explicitly linked to `lab-rtb-private1-us-east-1a`, while the public subnets remain implicitly tied to the main route table. This step ensures internal and external traffic flows are segmented and routed correctly based on subnet intent (public vs private).

![Screenshot 2025-06-01 214617](https://github.com/user-attachments/assets/e18393c4-b539-43ab-88d2-9d555ac76763)

---

### 6. Subnet and Route Table Association

**Here we manually associate subnets with the appropriate route tables.** This ensures proper routing between private/public zones and the internet or NAT gateway.

![Route Table Associations](./Screenshot%202025-06-01%20214617.png)

---

### 7. Configuring a Security Group for HTTP Access

Here we create a security group named **Web Security Group** that allows inbound HTTP traffic (port 80) from any IP address (`0.0.0.0/0`). This enables public web access to the EC2 instance. 

![Screenshot 2025-06-01 214919](https://github.com/user-attachments/assets/5dc67705-3feb-4a04-8ad7-e463c4ca673d)

---

### 8. Finalizing and Deploying the Web Server

At last, we finalize the instance configuration by assigning it to the appropriate subnet and security group, then proceed to launch. This concludes the lab by successfully deploying a web-accessible EC2 instance inside our custom VPC, demonstrating the complete provisioning of an IaaS networking environment.

![Screenshot 2025-06-01 215047](https://github.com/user-attachments/assets/4aed49ee-0331-4e40-9073-9a43b59dcd05)

![Screenshot 2025-06-01 215154](https://github.com/user-attachments/assets/9ce91f23-e090-4f15-9af9-94a36a091a7c)




## Next Steps

- Add EC2 Auto-Stop automation using Lambda (aligns with cloud cost management)
- Add monitoring via CloudWatch and VPC flow logs
- Create an ALB to handle high availability and load balancing
