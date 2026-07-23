---
title: "Module 1: Deploy RDS PostgreSQL Database"
date: 2026-07-15
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# MODULE 1: DEPLOY AMAZON RDS POSTGRESQL DATABASE

### STEP 1: Access Amazon RDS Service
1. In the top main search bar (`[Alt+S]`), type: **RDS** or click directly on **Aurora and RDS** under Recently visited.
2. Select the **RDS (Managed Relational Database Service)** service from the search results.

![Access Amazon RDS Service](/images/5-Workshop/5.2-RDS-PostgreSQL/image2.png)

---

### STEP 2: Navigate to Create Database Page
1. On the RDS Dashboard, in the left navigation menu, click **Databases**.
2. Click the orange **Create database** button in the top right corner.
3. Choose the **Full configuration** option.

![Create Database Page](/images/5-Workshop/5.2-RDS-PostgreSQL/image9.png)

---

### STEP 3: Configure Detailed Parameters (Create database)

#### 1. Engine Options
- **Engine type**: Select **PostgreSQL**
- **Database creation method**: Select **Full configuration**

![Select PostgreSQL](/images/5-Workshop/5.2-RDS-PostgreSQL/image4.png)
![Engine Configuration](/images/5-Workshop/5.2-RDS-PostgreSQL/image8.png)

#### 2. Settings & Credentials
- **Engine version**: Keep the latest default PostgreSQL version (e.g., PostgreSQL 16/18).
- **DB instance identifier**: Enter `wms-pro-db`.
- **Master username**: `postgres`.
- **Credentials management**: Select **Self managed**.
- **Master password & Confirm master password**: Enter your admin password (e.g., `WmsPro2026Password!`).

![Settings Configuration](/images/5-Workshop/5.2-RDS-PostgreSQL/image7.png)
![Master Password Setup](/images/5-Workshop/5.2-RDS-PostgreSQL/image12.png)

#### 3. Instance Configuration & Storage
- **DB instance class**: Choose a micro instance (e.g., `db.t4g.micro` or `db.t3.micro`) eligible for **Free Tier**.
- **Storage type**: Keep **General Purpose SSD (gp2)** or **gp3**.
- **Allocated storage**: Enter `20` (GiB).

![Instance Configuration & Storage](/images/5-Workshop/5.2-RDS-PostgreSQL/image1.png)

#### 4. Connectivity
- **Compute resource**: Select **Don't connect to an EC2 compute resource**.
- **Virtual private cloud (VPC)**: Select **Default VPC**.
- **Public access**: **CRITICAL**: Switch from **No** to **Yes** (To enable direct seeding from local PC).
- **VPC security group (firewall)**: Select **Create new**, name the Security Group `wms-rds-sg`.

![Connectivity Configuration](/images/5-Workshop/5.2-RDS-PostgreSQL/image6.png)
![Public Access & Security Group](/images/5-Workshop/5.2-RDS-PostgreSQL/image5.png)

#### 5. Monitoring & Additional Configuration
- **Monitoring**: Leave defaults.
- Expand **Additional configuration** at the bottom of the page.
- **Initial database name**: Enter exactly `logistics` (Required to match NestJS backend source code).
- Keep all other settings (Backup, Encryption, Maintenance) as default.

![Set Initial Database Name](/images/5-Workshop/5.2-RDS-PostgreSQL/image3.png)

---

### FINAL STEP: Launch Database
After filling in `logistics` as the **Initial database name**, scroll to the bottom and click the orange **Create database** button.

![Complete Database Creation](/images/5-Workshop/5.2-RDS-PostgreSQL/image10.png)
![Check Databases List](/images/5-Workshop/5.2-RDS-PostgreSQL/image11.png)
