---
title: "Workshop"
date: 2026-07-15
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Workshop: Deploying WMS Pro System on AWS Cloud Infrastructure

In this section, I document the complete step-by-step **Hands-on Lab** guide for deploying the **WMS Pro (Comprehensive Warehouse & Transportation Management System)** platform onto AWS Cloud infrastructure. Each lab module includes detailed instructions and actual screenshots from the AWS Management Console and Terminal.

---

### Hands-on Lab Modules:

1. **[5.1 - Workshop Overview](5.1-overview/):** Introduction to workshop goals, 3-tier cloud architecture, prerequisites, and AWS Free Tier cost optimization tips.
2. **[5.2 - Module 1: Deploy Amazon RDS PostgreSQL Database](5.2-rds-postgresql/):** Provisioning Amazon RDS PostgreSQL cluster (`wms-pro-db`), creating initial `logistics` database, and configuring `wms-rds-sg` security group.
3. **[5.3 - Module 2: Launch Amazon EC2 Application Server](5.3-ec2-server/):** Launching EC2 Ubuntu 24.04 LTS virtual server (`wms-pro-server`), creating SSH key pair `wms-server-key`, and configuring Security Group inbound rules (ports 22, 80, 443, 3333).
4. **[5.4 - Module 3: Configure EC2 Backend Connection to RDS & API Activation](5.4-connect-ec2-rds/):** Extracting RDS Endpoint, configuring SG-to-SG Inbound rule 5432, installing Node.js 20 / PM2 via SSH, setting up `.env` parameters, and bringing up Swagger API Documentation.

---

{{% notice info %}}
💡 **Note:** All hands-on steps in this workshop strictly follow security best practices and cost optimization rules within the **AWS Free Tier** allocation.
{{% /notice %}}
