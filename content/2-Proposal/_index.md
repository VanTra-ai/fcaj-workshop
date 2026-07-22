---
title: "Proposal"
date: 2026-07-12
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

In this section, I summarize the contents of the workshop on deploying a real-world warehouse and transportation management system to the AWS cloud platform.

# WMS Pro: Comprehensive Warehouse & Transportation Management System  
## A Comprehensive Warehouse & Transportation Management Solution on AWS Cloud

### 1. Executive Summary  
**WMS Pro** is an integrated internal logistics management platform designed to solve operational challenges faced by express delivery services. The system connects three core components: **Backend (NestJS)**, **Web Dashboard (Next.js)**, and **Mobile App (Flutter)**. By leveraging **AWS Cloud infrastructure (EC2, RDS, S3)**, WMS Pro provides real-time shipment monitoring, intelligent fleet management, and automated financial reconciliation with absolute precision.

### 2. Problem Statement  
*Current Issues*  
Many small and medium-sized logistics providers face difficulties with:
- Managing goods loss due to manual handover processes.
- Cash-on-Delivery (COD) reconciliation discrepancies between shippers and post offices.
- Slow and inaccurate address entry.
- Lack of real-time Key Performance Indicator (KPI) reporting systems for business decision-making.

*The Solution*  
WMS Pro adopts a strict 12-step **State Machine** model to lock down the order lifecycle. The system integrates a 2-tier administrative boundary model (2025 standard), optimizing address entry time by 80%. All data operates on **Amazon RDS (PostgreSQL)** to guarantee transaction integrity (ACID compliance) and **Amazon S3** for storing proof of delivery and incident images.

*Benefits and Return on Investment (ROI)*  
- **Operational Improvement**: Reduces dispatch staffing costs by 30% thanks to order assignment algorithms and virtual parking lots.
- **Financial Transparency**: E-wallet system and centralized reconciliation eliminate cash leakage risks.
- **Optimized Cost**: Utilizing the **AWS Free Tier**, infrastructure operational costs are estimated at < $10 USD/month during the initial phase. Expected break-even period is 4-6 months due to savings in manual operation and management expenses.

### 3. Solution Architecture  
The system employs a Multi-tier Architecture deployed on AWS to ensure security and scalability.

![WMS Pro System Architecture](/images/2-Proposal/wms_platform_architecture.jpeg)

*AWS Services Used*  
- **Amazon EC2 (t3.micro)**: Runs Backend application (NestJS) and Web Frontend (Next.js) with Nginx Reverse Proxy.
- **Amazon RDS (PostgreSQL)**: Relational database storing waybills, user information, and financial transactions.
- **Amazon S3**: Stores incident proof images and Proof of Delivery (POD).
- **AWS IAM**: Manages resource access permissions via Role-based access control instead of static Access Keys.
- **Amazon CloudFront (Optional)**: Accelerates static content delivery for the Web App.

### 4. Technical Implementation  
*Implementation Phases*  
1. **Analysis & Design**: Finalize order state machine and Entity Relationship Diagram (ERD) (April).
2. **Core API & Database Development**: Develop NestJS Backend connecting to RDS, set up pagination, and JWT security (May).
3. **Multi-platform Development**: Build Web Dashboard for Admin/Warehouse staff and Flutter Mobile App for Shippers (June).
4. **Cloud Migration & Testing**: Deploy entire system to AWS, integrate S3, and test real-world operational flows (July).

*Technical Requirements*  
- **Backend**: Node.js 20+, NestJS, TypeORM.
- **Frontend**: Next.js 14+ (App Router), Tailwind CSS.
- **Mobile**: Flutter SDK 3.x, Provider/Riverpod for state management.
- **DevOps**: Docker, Nginx, PM2 for service maintenance on EC2.

### 5. Timeline & Milestones  
- **April - May**: Complete waybill handling logic and e-wallet financial operations.
- **June**: Complete "Virtual Parking Lot" and "2-in-1 Order Processing Station" interfaces.
- **July**: 
    - Week 1: Set up VPC and RDS on AWS.
    - Week 2: Deploy Backend & Web to EC2, configure S3.
    - Week 3: Build Mobile App, perform E2E (End-to-End) testing.
    - Week 4: Final acceptance and handover.

### 6. Budget Estimation (AWS Free Tier Focused)  
- **Compute (EC2)**: $0.00 USD (750 hours/month t2.micro/t3.micro).
- **Database (RDS)**: $0.00 USD (750 hours/month, 20GB storage).
- **Storage (S3)**: ~$0.10 USD (For initial 5GB image data).
- **Data Transfer**: ~$0.50 USD (Based on actual traffic).
*Total Estimated Cost*: **< $1.00 USD/month** during the first year.

### 7. Risk Assessment  
- **Security Risk**: Waybill data leak. *Mitigation*: Use HTTPS, data masking on public tracking links, and Security Group IP restrictions.
- **Operational Risk**: Shipper loses network connectivity while delivering. *Mitigation*: Mobile App supports local offline storage and syncs when reconnected.
- **Financial Risk**: Errors in wallet credit/debit logic. *Mitigation*: Utilize Database Transactions and Pessimistic Locking.

### 8. Expected Outcomes  
- A Production-ready Logistics management system.
- Capability to process 10,000+ waybills/month under Free Tier configuration.
- Seamless, consistent user experience between Web and Mobile.
- Clean data foundation ready for future integration of route forecasting AI modules.