---
title: "Week 12 Worklog"
date: 2026-07-12
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:

* Provision and containerize the entire AWS Cloud infrastructure for the Logistics system (WMS Pro) with cost optimization under the Free Tier tier (< $10 USD/month).
* Successfully deploy Amazon RDS PostgreSQL Database, configure security isolation with Security Groups, and ensure seamless connection with Amazon EC2 application server.
* Configure production environment (Node.js 20, PM2, Nginx Reverse Proxy) on Ubuntu EC2; successfully deploy NestJS Backend API and Next.js Frontend Web App.
* Integrate Amazon S3 object storage for delivery/incident proof images, applying IAM Role Instance Profile to EC2 to access S3 without hardcoded Access Keys.
* Configure Cloud server IP address for Flutter Mobile App, package APK file, and execute End-to-End (E2E) acceptance testing of real-world business flows on physical devices.
* Standardize security compliance with AWS Well-Architected Framework: Configure SG-to-SG Inbound rules between EC2 and RDS, verify KMS data encryption.
* Record System Demo Video, package technical documentation, complete Workshop/Internship Report pages on Hugo Site, and complete final project acceptance.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date |
| --- | --- | --- | --- |
| Mon | - System parameter analysis and `.env` environment file preparation across 3 subsystems (Backend NestJS, Web Next.js, Mobile Flutter).<br>- Provision Amazon RDS for PostgreSQL database (`db.t3.micro`, 20GB SSD, Single-AZ), configure Master User `postgres` and VPC Security Group.<br>- Provision Amazon EC2 server (Ubuntu 24.04 LTS, `t3.micro`), assign Elastic IP and open Security Group ports: 22 (SSH), 80 (HTTP), 443 (HTTPS), 3333 (NestJS API).<br>- SSH into EC2 via MobaXterm and install runtime environment: Node.js 20 LTS, Git, PM2 Process Manager, and Nginx Web Server. | 06/07/2026 | 06/07/2026 |
| Tue | - Clone `logistics-backend` source code from GitHub to EC2, configure `.env` troring `DB_HOST` to Amazon RDS PostgreSQL Endpoint.<br>- Compile source code (`npm install`, `npm run build`), enable TypeORM auto-table synchronization (`synchronize: true`), and manage process via PM2 (`pm2 start dist/main.js --name wms-api`).<br>- Test public API connection and Swagger UI interface at `http://<EC2-Public-IP>:3333/api`.<br>- Deploy `logistics-web-app` (Next.js): Configure `NEXT_PUBLIC_API_URL`, build production bundle, and configure Nginx Reverse Proxy routing port 80 to Web App (port 3000) and API (port 3333). | 07/07/2026 | 07/07/2026 |
| Wed | - Create public Amazon S3 Bucket to store delivery proof images and incident report photos uploaded from the mobile application.<br>- Edit `lib/core/network/api_client.dart` in Flutter codebase, updating `_baseUrl` directly to EC2 Server Public IP.<br>- Package mobile application into release APK (`flutter build apk`) and install onto physical Android device.<br>- Execute field delivery test flow: Shipper App Login $\rightarrow$ Barcode Scan $\rightarrow$ Capture Proof Photo $\rightarrow$ Upload to S3 $\rightarrow$ Real-time Sync to Web Dashboard. | 08/07/2026 | 08/07/2026 |
| Thu | - Apply AWS Well-Architected Framework security practices:<br>&emsp; + Configure RDS Security Group SG-to-SG rule: Only accept port 5432 Inbound traffic from EC2 Security Group ID.<br>&emsp; + Create IAM Role with `AmazonS3FullAccess` policy, attached to EC2 as Instance Profile so NestJS Backend accesses S3 securely without static Access/Secret Keys.<br>&emsp; + Review KMS Encryption Enabled attributes on Amazon S3 Bucket and Amazon RDS Instance.<br>- Package all codebase repositories on GitHub, clean temporary files, and finalize security audit. | 09/07/2026 | 09/07/2026 |
| Fri | - Record and edit professional Demo Video covering closed E2E operational scenarios of WMS Pro (order creation, warehouse storage, truck/bike dispatching, mobile delivery, and financial wallet reconciliation).<br>- Consolidate technical documentation, Cloud architecture, deployment guides, and update to Workshop documentation site (`vantra-ai.github.io/fcaj-workshop/`).<br>- Edit, review writing tone, and finalize complete Internship Graduation Report in accordance with AWS and HUTECH requirements. | 10/07/2026 | 10/07/2026 |

### Week 12 Achievements:

* **Successful AWS Production Cloud Infrastructure Deployment:**
  * Provisioned and operated stable Amazon RDS PostgreSQL 100% compatible with TypeORM, optimizing cost under AWS Free Tier.
  * Configured Ubuntu EC2 running NestJS Backend (port 3333) and Next.js Frontend (port 3000) concurrently via PM2 Process Manager and Nginx Reverse Proxy.
  * Successfully integrated Amazon S3 object storage for multimedia assets (delivery proof images, incident photos).
* **Multi-Platform Logistics Platform Packaging & Acceptance:**
  * Configured and built release APK for Flutter Mobile App, connecting seamlessly to Cloud API via EC2 Public IP.
  * Successfully conducted real-time E2E business flow acceptance: Shipper barcode scanning and photo upload on mobile instantly update order status and COD wallet balance on Web Dashboard.
* **AWS Well-Architected Security Compliance:**
  * Completely eliminated static Access Key/Secret Key hardcoding using IAM Role Instance Profiles on EC2.
  * Completely isolated RDS Database from public Internet via Security Group ID Inbound rules (SG-to-SG).
  * Ensured data security and integrity via server-side KMS encryption.
* **Final Report Products & Acceptance Documentation:**
  * Completed professional Demo Video recording all operations of WMS Pro system.
  * Consolidated all Workshop deployment guides and completed final Graduation Internship Report.
