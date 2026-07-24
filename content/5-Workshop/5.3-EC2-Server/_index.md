---
title: "Module 2: Deploy Amazon EC2 Application Server"
date: 2026-07-15
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### 1. Module Introduction

{{% notice info %}}
**Amazon EC2 (Elastic Compute Cloud)** provides scalable compute capacity in the AWS Cloud. In the **WMS Pro Logistics System**, the EC2 server serves as the operational heart running two main components:
* **Backend API (NestJS):** Core business logic, TMS dispatching algorithms, RDS PostgreSQL connection, and real-time WebSockets on port `3333`.
* **Frontend Web App (Next.js):** Management Dashboard UI for Coordinators and System Administrators.
{{% /notice %}}

{{% notice tip %}}
**Pro Tip:** Using `t2.micro` or `t3.micro` instances paired with Ubuntu Server 24.04 LTS allows you to utilize 750 hours/month of server runtime and 30GB of EBS storage free under the AWS Free Tier.
{{% /notice %}}

---

### 2. Step-by-Step Deployment Guide

#### Step 1: Access Amazon EC2 Service
1. Log in to the AWS Management Console.
2. In the top search bar (`[Alt+S]`), type **EC2**.
3. Select **EC2 (Virtual Servers in the Cloud)**.

![Access Amazon EC2 Service](/images/5-Workshop/5.3-EC2-Server/image7.png)

---

#### Step 2: Launch EC2 Instance
1. On the EC2 Dashboard, find **Launch instance**.
2. Click the orange **Launch instance** button.

![Launch EC2 Instance](/images/5-Workshop/5.3-EC2-Server/image8.png)

---

#### Step 3: Configure Detailed EC2 Server Parameters

##### 2.1. Server Name (Name and tags)
* **Name**: Enter `wms-pro-server`.

##### 2.2. Operating System (AMI Selection)
1. Under Quick Start, select **Ubuntu**.
2. **Amazon Machine Image (AMI)**: Select **Ubuntu Server 24.04 LTS (HVM)**, SSD Volume Type (64-bit x86 - *Free tier eligible*).

![Select Ubuntu OS](/images/5-Workshop/5.3-EC2-Server/image1.png)

##### 2.3. Hardware Configuration (Instance type)
* **Instance type**: Select `t2.micro` or `t3.micro` (*Free tier eligible*).

##### 2.4. SSH Key Pair Configuration
1. Under **Key pair (login)**, click **Create new key pair**.
2. Configure parameters:
   * **Key pair name**: Enter `wms-server-key`.
   * **Key pair type**: Select **RSA**.
   * **Private key file format**: Select `.pem` (for OpenSSH / MobaXterm / Termius / VS Code) or `.ppk` (for PuTTY).
3. Click **Create key pair** to download the private key file.
4. Select `wms-server-key` in the dropdown list.

![Create Key Pair](/images/5-Workshop/5.3-EC2-Server/image11.png)
![Select Key Pair](/images/5-Workshop/5.3-EC2-Server/image4.png)

##### 2.5. Network & Security Group Settings
1. Click **Edit** on the right side of **Network settings**.
2. **VPC**: Select **Default VPC**.
3. **Auto-assign public IP**: Select **Enable**.
4. **Firewall (security groups)**: Select **Create security group**.
5. **Security group name**: Enter `wms-ec2-sg`.
6. Add the following Inbound Rules:

| Rule Type | Protocol | Port Range | Source Type | Source CIDR | Purpose |
| --- | --- | --- | --- | --- | --- |
| **SSH** | TCP | `22` | Anywhere | `0.0.0.0/0` | Remote Terminal Management |
| **HTTP** | TCP | `80` | Anywhere | `0.0.0.0/0` | Web App / Nginx Reverse Proxy |
| **HTTPS** | TCP | `443` | Anywhere | `0.0.0.0/0` | SSL/TLS Encryption |
| **Custom TCP** | TCP | `3333` | Anywhere | `0.0.0.0/0` | NestJS Backend API & Socket.io |

![Security Group Settings 1](/images/5-Workshop/5.3-EC2-Server/image10.png)
![Security Group Settings 2](/images/5-Workshop/5.3-EC2-Server/image9.png)
![Security Group Rules](/images/5-Workshop/5.3-EC2-Server/image5.png)

{{% notice warning %}}
**Security Notice:** Opening ports 22 (SSH) and 3333 to `0.0.0.0/0` (Anywhere) is for testing purposes. In production, restrict port 22 to your personal static IP (*My IP*).
{{% /notice %}}

##### 2.6. Storage Configuration
* **Root volume**: Keep default 8 GiB gp3 (SSD).

---

#### Step 4: Launch Instance & Retrieve Public IP
1. Review settings in the Summary pane.
2. Click **Launch instance**.
3. Once launched, click the Instance ID to view server details.
4. Record the **Public IPv4 address** (e.g., `54.169.12.125`). This IP will be used in `.env` files for Web and Mobile apps.

![Launch Instance Success](/images/5-Workshop/5.3-EC2-Server/image3.png)
![Instance Summary](/images/5-Workshop/5.3-EC2-Server/image2.png)
![Public IP Address](/images/5-Workshop/5.3-EC2-Server/image6.png)

---

### 3. Module 2 Summary

In this module, you have successfully:
* Launched an **Amazon EC2 Ubuntu 24.04 LTS** instance (`wms-pro-server`) on AWS Free Tier.
* Created the SSH key pair `wms-server-key` for remote administration.
* Configured `wms-ec2-sg` opening ports 22, 80, 443, and 3333.
* Obtained a Public IPv4 Address ready for application deployment.
