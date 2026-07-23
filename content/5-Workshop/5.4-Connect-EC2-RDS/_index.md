---
title: "Module 3: Connect EC2 to RDS PostgreSQL"
date: 2026-07-15
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

# MODULE 3: CONFIGURE EC2 BACKEND CONNECTION TO RDS POSTGRESQL

### STEP 1: Get RDS Database Endpoint
1. In the top search bar, type **RDS** and select the RDS service.
2. Click on your `wms-pro-db` instance created in Module 1.
3. Under the **Connectivity & security** tab, copy the **Endpoint** string (e.g., `wms-pro-db.c7asq8i066d6.ap-southeast-1.rds.amazonaws.com`).
*(Save this Endpoint string to configure `DB_HOST` in the NestJS Backend).*

![View RDS Database Details](/images/5-Workshop/5.4-Connect-EC2-RDS/image6.png)
![Copy Database Endpoint](/images/5-Workshop/5.4-Connect-EC2-RDS/image3.png)
![Connectivity & Security Tab](/images/5-Workshop/5.4-Connect-EC2-RDS/image5.png)

---

### STEP 2: Configure RDS Security Group Firewall
To allow the EC2 application server (`wms-pro-server`) to communicate with the RDS database, port `5432` must be opened on the RDS Security Group:

1. Under `wms-pro-db` details -> **Connectivity & security**, click the **VPC security groups** link (`wms-rds-sg`).
2. You will be redirected to the VPC Security Groups management page.
3. Select the RDS Security Group -> Click the **Inbound rules** tab -> Click **Edit inbound rules**.
4. Click **Add rule**:
   - **Type**: Select **PostgreSQL** (Port `5432`).
   - **Source**: Select **Custom** -> Enter the Security Group ID of `wms-pro-server` (e.g., `sg-xxxxxxxxxxxxxxxxx`) or EC2 Public IP.
   - **Description**: `Allow EC2 backend to access PostgreSQL`.
5. Click **Save rules**.

![Redirect to Security Group Page](/images/5-Workshop/5.4-Connect-EC2-RDS/image1.png)
![Security Groups List](/images/5-Workshop/5.4-Connect-EC2-RDS/image7.png)
![Edit Inbound Rules for RDS](/images/5-Workshop/5.4-Connect-EC2-RDS/image4.png)
![Save Inbound Rules Successfully](/images/5-Workshop/5.4-Connect-EC2-RDS/image2.png)
