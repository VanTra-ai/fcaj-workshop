---
title: "Module 1: Deploy Amazon RDS PostgreSQL Database"
date: 2026-07-15
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### 1. Module Introduction

{{% notice info %}}
**Amazon RDS (Relational Database Service)** is a fully managed relational database service provided by AWS. RDS automates time-consuming administration tasks such as infrastructure provisioning, database setup, patching, backups, and disaster recovery.

In the **WMS Pro Logistics System**, the Database layer stores all critical data: orders, warehouse inventory, driver wallet balances, tracking history, and waybills. PostgreSQL is selected to ensure full transaction integrity (ACID) and seamless compatibility with TypeORM on the NestJS Backend.
{{% /notice %}}

{{% notice tip %}}
**Pro Tip:** Under the AWS Free Tier, you get 750 hours/month of Amazon RDS (using `db.t2.micro` or `db.t4g.micro` instances) along with 20GB of General Purpose SSD (`gp2`/`gp3`) storage completely free for your first 12 months.
{{% /notice %}}

---

### 2. Step-by-Step Deployment Guide

#### Step 1: Access Amazon RDS Service
1. Log in to the AWS Management Console.
2. In the top main search bar (`[Alt+S]`), type **RDS** or **Aurora and RDS**.
3. Select **Aurora and RDS (Managed Relational Database Service)** from the search results.

![Access Amazon RDS Service](/images/5-Workshop/5.2-RDS-PostgreSQL/image4.png)

---

#### Step 2: Navigate to Create Database Page
1. On the RDS Dashboard, in the left navigation menu, click **Databases**.
2. Click the orange **Create database** button in the top right corner.
3. Select **Full configuration** mode to customize network and security parameters.

![Navigate to Create Database](/images/5-Workshop/5.2-RDS-PostgreSQL/image9.png)

---

#### Step 3: Configure Detailed Database Parameters

##### 2.1. Engine Options & Creation Method
* **Engine type**: Select **PostgreSQL**.
* **Choose a database creation method**: Select **Full configuration**.

![Engine Options](/images/5-Workshop/5.2-RDS-PostgreSQL/image6.png)

##### 2.2. Templates & Availability
* **Templates**: Select **Free tier**.
* **Availability and durability**: Default to **Single-AZ DB instance deployment** (1 instance).

![Templates Free Tier](/images/5-Workshop/5.2-RDS-PostgreSQL/image3.png)

##### 2.3. Settings & Credentials
* **Engine version**: Keep the default latest version (e.g., PostgreSQL 18.3-R2).
* **DB instance identifier**: Enter `wms-pro-db`.
* **Master username**: Enter `postgres`.
* **Credentials management**: Select **Self managed**.
* **Master password**: Enter your admin password (e.g., `WmsPro2026Password!`).
* **Confirm master password**: Re-enter password to confirm.

![Settings and Credentials](/images/5-Workshop/5.2-RDS-PostgreSQL/image10.png)
![Master Password Setup](/images/5-Workshop/5.2-RDS-PostgreSQL/image1.png)

{{% notice warning %}}
⚠️ **Important Notice:** Save your Master Username (`postgres`) and Master Password in a secure location. These credentials are required for the `DB_USER` and `DB_PASS` environment variables in the NestJS Backend `.env` file.
{{% /notice %}}

##### 2.4. Instance & Storage Configuration
* **DB instance class**: Choose **Burstable classes (includes t classes)** $
ightarrow$ Select `db.t4g.micro` or `db.t2.micro` (*Free tier eligible*).
* **Storage type**: Select **General Purpose SSD (gp2)**.
* **Allocated storage**: Enter `20` (GiB).

![Instance and Storage](/images/5-Workshop/5.2-RDS-PostgreSQL/image7.png)

##### 2.5. Connectivity & Networking
* **Compute resource**: Select **Don’t connect to an EC2 compute resource**.
* **Virtual private cloud (VPC)**: Select **Default VPC**.
* **Public access**: Select **Yes**.

{{% notice note %}}
**Security Note:** Setting `Public access = Yes` at this stage allows local database seeding and testing from your workstation. In Module 3, we will restrict Inbound Rules in the Security Group to allow only EC2 IP addresses.
{{% /notice %}}

* **VPC security group (firewall)**: Select **Create new**.
* **New VPC security group name**: Enter `wms-rds-sg`.

![Connectivity Configuration](/images/5-Workshop/5.2-RDS-PostgreSQL/image2.png)
![Public Access and Security Group](/images/5-Workshop/5.2-RDS-PostgreSQL/image11.png)

##### 2.6. Initial Database Name (Additional Configuration)
1. Scroll down to expand **Additional configuration**.
2. Under **Database options** $
ightarrow$ **Initial database name**: Enter `logistics`.

![Initial Database Name](/images/5-Workshop/5.2-RDS-PostgreSQL/image5.png)

{{% notice warning %}}
CRITICAL: If **Initial database name** is left empty, Amazon RDS will create an empty instance without creating the database schema. NestJS Backend will fail with error `"logistics" does not exist`. You MUST specify `logistics` in this step!
{{% /notice %}}

---

#### Step 4: Launch and Verify Database Status
1. Review all configured parameters.
2. Click the orange **Create database** button at the bottom of the page.
3. The status of `wms-pro-db` will initially show `Creating`. This process takes 5-10 minutes.
4. Once the status changes to `Available`, click `wms-pro-db` to copy the **Endpoint** address and **Port** (`5432`).

![Create Database Complete](/images/5-Workshop/5.2-RDS-PostgreSQL/image8.png)

---

### 3. Module 1 Summary

In this module, you have successfully:
* Deployed **Amazon RDS for PostgreSQL** (`wms-pro-db`) on AWS Free Tier.
* Provisioned the initial `logistics` database 100% compatible with NestJS TypeORM Entities.
* Created the `wms-rds-sg` security group prepared for SG-to-SG rules with EC2.
