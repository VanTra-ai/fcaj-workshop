---
title: "Week 3 Worklog"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

- Understood and configured manual routing on TGW for centralized networking across multiple VPCs, completely replacing complex VPC Peering models.
- Managed and securely connected to Private/Public instances without needing Bastion Hosts, SSH Keys, or opening sensitive ports (22, 3389).
- Proficient in instance administration (modifying configuration, creating Snapshots, packaging Custom AMIs), troubleshooting lost Key Pairs, and practically deploying a Node.js CRUD application.
- Applied IAM Policies (JSON) to grant permissions based on the principle of least privilege, tightly controlling regions, instance types, and resource deletion rights.

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Start Date | Completion Date | Reference Material                   |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------ |
| 2   | - Initialized a 4-VPC connection architecture via the central AWS Transit Gateway hub.<br>- Created a Transit Gateway and configured Transit Gateway Attachments for the 4 VPCs.<br>- Set up Transit Gateway Route Tables (configured Associations and Propagations).<br>-Added routes pointing back to the Transit Gateway into the Route Tables of each VPC to establish network traffic flow.                                                                                                                                                         | 04/05/2026 | 04/05/2026      | https://000020.awsstudygroup.com/vi/ |
| 3   | - Prepared VPC and Security Group infrastructure, initialized Public Linux EC2 and Private Windows EC2 instances.<br>- Created an IAM Role granting AmazonSSMManagedInstanceCore and AmazonS3FullAccess permissions for EC2.<br>- Created VPC Interface Endpoints (ssm, ssmmessages, ec2messages) and an S3 Gateway Endpoint so that the Private EC2 can communicate with Systems Manager without Internet access.<br>- Configured session logs storage on an S3 bucket.<br>- Performed Port Forwarding via Session Manager to securely connect via RDP. | 05/05/2026 | 05/05/2026      | https://000058.awsstudygroup.com/vi/ |
| 4   | - Researched the EC2 tiering architecture, instance types, storage options (EBS, Instance Store), and Key Pair mechanisms.<br>- Prepared VPC, Subnets (Auto-assign public IP), and separate Security Groups for Linux and Windows environments.<br>- Initialized an Amazon Linux instance and connected via SSH (using MobaXterm or PuTTY).<br>- Initialized a Microsoft Windows Server instance and connected via RDP.                                                                                                                                  | 06/05/2026 | 06/05/2026      | https://000004.awsstudygroup.com/vi/ |
| 5   | - Modified Instance Type configurations.<br>- Created and managed EBS Snapshots, initialized Custom AMIs (using Sysprep for Windows).<br>- Handled lost Key Pair troubleshooting: Restored Windows EC2 access using AWS Systems Manager (Run Command) and restored Linux EC2 access using EC2 User Data.<br>- Deployed a Node.js (CRUD) application on Amazon Linux: Installed the LAMP stack, phpMyAdmin, Node.js via nvm, and configured the database.                                                                                                 | 07/05/2026 | 07/05/2026      | https://000004.awsstudygroup.com/vi/ |
| 6   | - Wrote IAM Policies (JSON) to restrict resource usage for cost optimization (Cost Governance).<br>- Granted permissions allowing users to launch EC2 instances only in a specific Region (Singapore).<br>- Restricted EC2 launches by Instance Family (t3, t4g, m5), Instance Type (t3.small, t3.large), and EBS volume type (gp3).<br>- Restricted EC2 termination rights based on corporate IP addresses and a specified time window.                                                                                                                 | 08/05/2026 | 08/05/2026      | https://000004.awsstudygroup.com/vi/ |

### Week 3 Achievements:

- Centralized Networking Knowledge & Implementation (TGW):
  - Successfully initialized a Transit Gateway acting as a central "Cloud Router," completely replacing complex VPC Peering architectures during system scaling.
  - Successfully connected 4 independent VPCs to the central router and precisely configured the route tables of each VPC to enable cross-VPC communication.
  - Successfully set up Transit Gateway Route Tables through manual configuration of Association and Propagation mechanisms to tightly control traffic flow.

- Secure Access Control (Systems Manager):
  - Securely connected to Public Linux EC2 instances via Session Manager without opening port 22, ensuring network traffic travels exclusively over HTTPS (port 443).
  - Configured VPC Interface Endpoints (ssm, ssmmessages, ec2messages) and an S3 Gateway Endpoint to manage a completely internet-isolated Windows server.
  - Automated the export of session logs recording command histories to an S3 bucket while performing Port Forwarding via SSM to Remote Desktop (RDP) into a Private Windows server.

- Advanced EC2 Operations & Application Deployment:
  - Performed resource upgrades (Instance Types), created EBS Snapshots for backups, and packaged standard Custom AMIs (using Sysprep on Windows) to launch new servers error-free.
  - Successfully rescued a Windows server that lost its Key Pair using SSM Run Command (EC2Rescue) and restored Linux server access by overwriting the public key via EC2 User Data.
  - Successfully configured Web Server environments (LAMP on Linux, XAMPP on Windows), installed phpMyAdmin, and deployed a live Node.js CRUD application connected to a database.

- Cost Governance & Deep-Layer Security (IAM):
  - Authored JSON policies enforcing users to perform EC2 operations exclusively within Singapore (ap-southeast-1) and automatically denying actions in other regions.
  - Configured StringNotLike conditions to restrict users to cost-effective instance families (t3, t4g, m5), specific instance types (t3.small, t3.large), and mandate the use of modern gp3 volumes.
  - Restricted server termination rights (ec2:TerminateInstances) to be permitted only when two conditions are met simultaneously: requests originating from a corporate static IP and outside the system freeze window.
  - Executed a thorough cleanup process for all practical resources (EC2, AMIs, Snapshots, Key Pairs, VPCs, IAM) to prevent unexpected cost generation.
