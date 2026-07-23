---
title: "Module 2: Launch EC2 Application Server"
date: 2026-07-15
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

# MODULE 2: LAUNCH APPLICATION SERVER WITH AMAZON EC2

### STEP 1: Access Amazon EC2 Service
1. In the top search bar (`[Alt+S]`), type: **EC2**.
2. Select **EC2 (Virtual Servers in the Cloud)** from the search results.

![Access Amazon EC2 Service](/images/5-Workshop/5.3-EC2-Server/image11.png)

---

### STEP 2: Launch Instance
1. On the **EC2 Dashboard**, click the orange **Launch instance** button.

![Click Launch Instance](/images/5-Workshop/5.3-EC2-Server/image4.png)

---

### STEP 3: Configure EC2 Instance Parameters

#### 1. Name and tags
- **Name**: Enter `wms-pro-server`

#### 2. Application and OS Images
- Select **Ubuntu** (System provided).
- **AMI**: Select **Ubuntu Server 24.04 LTS (HVM), SSD Volume Type** (64-bit x86).

![Select Ubuntu OS](/images/5-Workshop/5.3-EC2-Server/image7.png)

#### 3. Instance type
- Choose `t3.micro` or `t2.micro` (**Free Tier** eligible).

#### 4. Key pair (SSH Access Key)
1. Click **Create new key pair**.
2. **Key pair name**: Enter `wms-server-key`
3. **Key pair type**: RSA
4. **Private key file format**: `.pem` (for Linux/Mac/OpenSSH) or `.ppk` (for PuTTY).
5. Click **Create key pair** and securely store the downloaded key file.
6. Select the newly created key pair from the drop-down menu.

![Configure Key Pair](/images/5-Workshop/5.3-EC2-Server/image3.png)
![Key Pair Created](/images/5-Workshop/5.3-EC2-Server/image9.png)

#### 5. Network settings (Security Group Firewall)
- **VPC**: Select **Default VPC**.
- **Auto-assign public IP**: Select **Enable** (Required to access server via Public IP).
- **Firewall (Security group)**: Select **Create security group**.
- Check the boxes:
  - ☑ **Allow SSH traffic from**: Anywhere (`0.0.0.0/0`)
  - ☑ **Allow HTTP traffic from the internet**: Anywhere (`0.0.0.0/0`)
  - ☑ **Allow HTTPS traffic from the internet**: Anywhere (`0.0.0.0/0`)
- Click **Add security group rule** to open the NestJS API port:
  - **Type**: Custom TCP
  - **Port range**: `3333`
  - **Source**: Anywhere (`0.0.0.0/0`)

![Network Settings Security Group](/images/5-Workshop/5.3-EC2-Server/image2.png)
![Allow HTTP/HTTPS & Custom Port 3333](/images/5-Workshop/5.3-EC2-Server/image1.png)
![Detailed Inbound Rules Setup](/images/5-Workshop/5.3-EC2-Server/image5.png)

#### 6. Configure storage
- Keep default storage: `8 GiB` or `20 GiB` **gp3/gp2** (Free Tier eligible).

---

### STEP 4: Launch EC2 Instance
1. In the right panel, click the orange **Launch instance** button.
2. Verify **Successfully initiated launch of instance** message.
3. Click the Instance ID link (e.g., `i-0123456789abcdef0`) to view server status.

![Click Launch Instance](/images/5-Workshop/5.3-EC2-Server/image10.png)
![Launch Successful](/images/5-Workshop/5.3-EC2-Server/image6.png)
![View EC2 Instances List](/images/5-Workshop/5.3-EC2-Server/image8.png)
