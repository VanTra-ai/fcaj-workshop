---
title: "Module 3: Connect EC2 Backend with RDS PostgreSQL & API Activation"
date: 2026-07-15
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### 1. Module Introduction

{{% notice info %}}
In the **WMS Pro Logistics System**, the NestJS Backend application running on Amazon EC2 (`wms-pro-server`) needs to seamlessly communicate with the Amazon RDS PostgreSQL database (`wms-pro-db`).

This module guides you through extracting the RDS Endpoint, configuring Security Group rules (Port `5432`), SSHing into EC2 to setup runtime dependencies (Node.js 20 LTS, PM2 Process Manager), and bringing up the live API service.
{{% /notice %}}

{{% notice tip %}}
**Pro Tip:** NestJS TypeORM is configured with `synchronize: true`. As soon as the Backend connects to RDS, all database tables (`users`, `orders`, `shipments`, `locations`, `wallets`, etc.) are automatically schema-synchronized inside `logistics` database without manual migrations.
{{% /notice %}}

---

### 2. Step-by-Step Deployment Guide

#### Step 1: Extract Amazon RDS Endpoint
1. Log in to the AWS Management Console.
2. In the top search bar (`[Alt+S]`), search for **RDS** and select **Aurora and RDS**.
3. Click **Databases** in the left menu.
4. Select `wms-pro-db` created in Module 1.
5. Under the **Connectivity & security** tab, locate **Endpoints**.
6. Copy the **Endpoint** address (e.g., `wms-pro-db.c7asq8i066d6.ap-southeast-1.rds.amazonaws.com`). This will be used as the `DB_HOST` in `.env`.

![RDS Endpoint Step 1](/images/5-Workshop/5.4-Connect-EC2-RDS/image12.png)
![RDS Endpoint Step 2](/images/5-Workshop/5.4-Connect-EC2-RDS/image2.png)
![RDS Endpoint Step 3](/images/5-Workshop/5.4-Connect-EC2-RDS/image11.png)

---

#### Step 2: Configure Security Group Rules for RDS
To allow EC2 instances to query RDS PostgreSQL, open Port `5432` on the RDS Security Group:
1. Under **Connectivity & security** for `wms-pro-db`, locate **Security**.
2. Click the Security Group `wms-rds-sg`.
3. Select `wms-rds-sg` in the Security Groups list.
4. Select **Inbound rules** tab $
ightarrow$ Click **Edit inbound rules**.
5. Click **Add rule**:
   * **Type**: Select **PostgreSQL** (Port `5432`).
   * **Source**: Select **Custom** $
ightarrow$ Enter EC2 Public IP (`54.169.12.125/32`) or select EC2 Security Group ID (`wms-ec2-sg`).
   * **Description**: `Allow EC2 to access RDS`.
6. Click **Save rules**.

![RDS Security Group Edit 1](/images/5-Workshop/5.4-Connect-EC2-RDS/image3.png)
![RDS Security Group Edit 2](/images/5-Workshop/5.4-Connect-EC2-RDS/image15.png)
![RDS Security Group Edit 3](/images/5-Workshop/5.4-Connect-EC2-RDS/image4.png)
![RDS Security Group Edit 4](/images/5-Workshop/5.4-Connect-EC2-RDS/image13.png)

---

#### Step 3: SSH into EC2 & Install Runtime Dependencies
1. Open Terminal (MobaXterm, PuTTY, or VS Code Terminal).
2. Connect to EC2 using `wms-server-key.pem`:
   ```bash
   ssh -i "wms-server-key.pem" ubuntu@54.169.12.125
   ```

![SSH to EC2](/images/5-Workshop/5.4-Connect-EC2-RDS/image7.png)

3. Update Ubuntu package manager:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

![Ubuntu Update](/images/5-Workshop/5.4-Connect-EC2-RDS/image5.png)

4. Install Node.js 20 LTS, Git, and PM2:
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
   sudo apt-get install -y nodejs git build-essential

   node -v
   npm -v
   ```

![Nodejs Install](/images/5-Workshop/5.4-Connect-EC2-RDS/image14.png)

5. Install PM2 globally:
   ```bash
   sudo npm install -g pm2
   ```

![PM2 Install](/images/5-Workshop/5.4-Connect-EC2-RDS/image10.png)

---

#### Step 4: Deploy NestJS Backend & Configure Environment (.env)
1. Clone `logistics-backend` repository on EC2:
   ```bash
   git clone https://github.com/vantra-ai/logistics-backend.git
   cd logistics-backend
   ```

![Git Clone Backend](/images/5-Workshop/5.4-Connect-EC2-RDS/image9.png)

2. Install dependencies:
   ```bash
   npm install
   ```

![NPM Install](/images/5-Workshop/5.4-Connect-EC2-RDS/image1.png)

3. Create and edit `.env`:
   ```bash
   nano .env
   ```
   Paste environment configuration:
   ```env
   # --- DATABASE CONFIGURATION (Amazon RDS) ---
   DB_HOST=wms-pro-db.c7asq8i066d6.ap-southeast-1.rds.amazonaws.com
   DB_PORT=5432
   DB_USER=postgres
   DB_PASS=WmsPro2026Password!
   DB_NAME=logistics
   DB_SSL=false

   # --- SECURITY CONFIGURATION ---
   JWT_SECRET=WmsProLogisticsSuperSecretKey2026!

   # --- MAIL SERVICE (Nodemailer OTP) ---
   MAIL_HOST=smtp.gmail.com
   MAIL_PORT=587
   MAIL_USER=phamvantra1301@gmail.com
   MAIL_PASS=your_google_app_password
   MAIL_FROM="WMS Logistics Pro" <phamvantra1301@gmail.com>
   ```

4. Build production bundle:
   ```bash
   npm run build
   ```

![NPM Run Build](/images/5-Workshop/5.4-Connect-EC2-RDS/image8.png)

5. Launch application using PM2:
   ```bash
   pm2 start dist/main.js --name wms-api
   pm2 save
   pm2 startup
   ```

![PM2 Start](/images/5-Workshop/5.4-Connect-EC2-RDS/image6.png)

---

#### Step 5: Verify API & Swagger Documentation
1. Check PM2 process status:
   ```bash
   pm2 status
   ```
2. Open browser and access Swagger UI:
   `http://54.169.12.125:3333/api`
3. The **Logistics API - Swagger Documentation** page confirms successful database connection and API operation.

---

### 3. Module 3 Summary

After completing Module 3, you have achieved:
* Extracted RDS Endpoint and opened port `5432` access on Security Groups.
* Installed Node.js 20, Git, and PM2 on Ubuntu EC2.
* Configured `.env` parameters connecting NestJS Backend to RDS PostgreSQL.
* Activated Backend API service running 24/7 on port `3333` serving Next.js Web App and Flutter Mobile App.
