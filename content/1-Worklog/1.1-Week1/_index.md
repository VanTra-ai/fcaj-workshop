---
title: "Week 1 Worklog"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

- Familiarized with team members in the First Cloud AI Journey (FCAJ); understood the learning roadmap, practical project standards, and regulations at the internship unit.
- Explored Cloud Computing mindset, global infrastructure (Region, AZ, Edge Location), and resource interaction methods (Console, CLI, SDK).
- Mastered IAM identification knowledge, administrative group permission assignment, and compliance with basic security principles (MFA, Access Key).
- Got acquainted with the Free Tier environment combined with Budget tools for cost monitoring, and understood the operational process of the AWS support case system.

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Start Date | Completion Date | Reference Material                                                                                                                                       |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | - Joined community networks (WhatsApp, Facebook, LinkedIn) for learning and communication.<br>- Connected and interacted with members of the FCAJ program.<br>- Read and acknowledged working regulations, and understood graduation requirements.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | 20/04/2026 | 20/04/2026      |                                                                                                                                                          |
| 3   | - Explored the definition and 4 major benefits of Cloud Computing.<br>- Analyzed AWS infrastructure: Data Center structure, Region, AZ (high availability with at least 3 AZs/Region), and Local Zone in Vietnam connected to Singapore.<br>- Familiarized with the AWS Management Console interface, learned an overview of the CLI for automation, and the role of Serialization/Retrying in AWS SDK.<br>- Researched software development tools using AI assistant – AWS Kiro (Kiro IDE, Agent Hook, Steering files, Rollback checkpoint).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | 21/04/2026 | 21/04/2026      | https://www.youtube.com/playlist?list=PLahN4TLWtox3TSYFbN1DNX7NZgTVXNj3x                                                                                 |
| 4   | - Researched documentation distinguishing Free Plan vs Paid Plan and the strategy to receive $200 Credit.<br>- Initialized the AWS Free Tier account and set up a Virtual MFA Device.<br>- Practiced IAM Console: Created an admin-group (assigned AdministratorAccess policy) and an admin-user (enabled first-time password reset policy), downloaded and securely stored the .csv credential file.<br>- Verified anonymous login via Sign-in Link, practiced creating an Access Key for the CLI, and performed key lifecycle management operations (Deactivate/Delete).<br>- Briefly studied IAM Role and system permission structure.                                                                                                                                                                                                                                                                                                                                                                                             | 22/04/2026 | 22/04/2026      | https://000001.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i                                         |
| 5   | - Implemented the practical campaign consisting of 5 credit-earning tasks from the Explore AWS widget on the console homepage.<br>+ Task 1 (EC2): Successfully initialized a Test Instance, configured the first-kp (.pem) key pair, Security Group, and performed Terminate upon completion.<br>+ Task 2 (Bedrock): Thử nghiệm chat playground với mô hình Claude 3 Haiku, thực hiện mở case hỗ trợ Bedrock Allowlisting với AWS Support khi gặp lỗi Authorization.<br>+ Task 3 (Budgets): Set up the monthly cost budget My Monthly Cost Budget ($100) with automatic email alerts attached at 85% and 100% thresholds. <br>+ Task 4 (Lambda): Built a serverless web application running Node.js using a sample Blueprint, activated the Public Function URL, and securely deleted the function.<br>+ Task 5 (RDS): Rapidly initialized a sample Aurora relational database cluster (PostgreSQL Compatible) for the Dev/Test environment and followed the proper cluster deletion procedure after its status changed to Available. | 23/04/2026 | 23/04/2026      | https://000001.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i                                         |
| 6   | - Researched the operational structure of AWS Support across 4 service tiers (Basic, Business Support+, Enterprise, Unified Operations).<br>- Learned the support case management process and 3 common error categories (Billing, Limit Increase, Technical Support).<br>- Expanded on AWS Budgets theory (Cost, Usage, RI, Savings Plans Budget) and practiced creating custom advanced budgets combined with lab resource cleanup.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | 24/04/2026 | 24/04/2026      | https://000007.awsstudygroup.com/vi/<br>https://000009.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |

### Week 1 Achievements:

- Understood what AWS is, mastered global infrastructure knowledge (Region, AZ, Local Zone), and basic service categories:
  - Compute (EC2, Lambda)
  - Database (RDS - Aurora PostgreSQL)
  - Management & Governance (Budgets, AWS Support)
  - Artificial Intelligence (Amazon Bedrock, AWS Kiro)

- Successfully created and configured an AWS Free Tier account along with standard security settings:
  - Enabled Virtual MFA for the Root account
  - Created IAM Groups and IAM Users with administrative permissions

- Got familiar with the AWS Management Console and learned how to find, access, and use services from the web interface.

- Practiced configuring and managing identities and access keys, including:
  - Access Key
  - Secret Key
  - Key lifecycle management (Generation, Deactivation, Deletion)

- Used the AWS Console to perform basic operations and completed the task chain to receive the $200 Credit:
  - Created, connected to, and terminated an EC2 virtual server
  - Created and managed key pairs (.pem format for SSH)
  - Submitted a Support Case requesting AI model access permissions
  - Set up Budgets with email alerts for costs and usage thresholds
  - Initialized a Serverless Lambda function and an RDS database cluster

- Capable of bridging network infrastructure theory with web interface operations to manage AWS resources concurrently, being aware of the importance of cleaning up resources after practice

- Understood the team working culture and development roadmap of the FCAJ program
