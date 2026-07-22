---
title: "Week 4 Worklog"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

- Mastered the mindset of system resource classification, proficient in scientific data tagging skills, and automated management of large server groups using smart AWS Resource Groups filters.
- Built a centralized monitoring solution (Observability). Proficient in the data collection process (Metrics & Logs), establishing proactive alarms via email, and designing intuitive dashboards to monitor system health in real time.
- Understood the design principles of fault-tolerant and high-availability applications. Deployed an auto-scaling system based on actual load by separating network partitions (Public/Private Subnets) combined with load balancers.
- Approached the managed virtual private server (VPS) service model with optimized fixed costs. Proficient in multi-application deployment processes, deep-layer security setup, system backup, and resource upgrades without causing service disruptions.

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Start Date | Completion Date | Reference Material                   |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------ |
| 2   | - Practiced creating a t3.micro instance and assigning data management tags directly on the Console interface.<br>- Configured resource classification tag pairs: Owner, Service, Environment, BusinessUnit.<br>- Practiced tag management via AWS CLI using commands: create-tags, run-instances, and create-volume.<br>- Filtered and checked the list of tagged resources via the describe-instances CLI command.<br>- Initialized a MarketingBU management group as a tag-based group to automatically aggregate EC2 virtual machines.<br>- Performed lab resource cleanup: Terminated all EC2 instances and deleted the newly created Resource Group.                                                                                                     | 11/05/2026 | 11/05/2026      | https://000027.awsstudygroup.com/vi/ |
| 3   | - Deployed a sample monitoring infrastructure via the AWS CloudFormation Stack service.<br>- Analyzed CPUUtilization and EBSWriteBytes metrics, modified the Y-axis, and added horizontal/vertical reference lines.<br>- Practiced writing SEARCH() search expressions and SORT() mathematical expressions to extract advanced metrics.<br>- Checked system logs, configured log retention periods down to 1 week.<br>- Wrote error log query statements via Logs Insights and created a Metric Filter from the ERROR keyword to convert logs into numeric data.<br>- Configured email alerts via AWS SNS, integrated charts into the CloudWatch Dashboard, and deleted the stack.                                                                             | 12/05/2026 | 12/05/2026      | https://000008.awsstudygroup.com/vi/ |
| 4   | - Set up the AutoScaling-Lab VPC infrastructure consisting of 3 AZs, divided into 3 public subnets and 3 private subnets.<br>- Configured Security Groups for the application (opening ports 22, 80, 443, 5000) and for the RDS database (opening port 3306).<br>- Launched the FCJ-Management EC2 instance in the public subnet and connected via SSH.<br>- Initialized a Multi-AZ MySQL database on Amazon RDS, connected to it, and imported sample data tables.<br>- Installed the Node.js environment, cloned the source code, configured the environment variables file, and ran the web application via PM2.<br>- Prepared and uploaded simulated data scripts to CloudWatch Custom Metrics to support the Predictive Scaling feature.                  | 13/05/2026 | 13/05/2026      | https://000006.awsstudygroup.com/vi/ |
| 5   | - Created an AMI backup from the current EC2 instance and set up a standard Launch Template configuration.<br>- Initialized a Target Group on port 5000 and configured an Application Load Balancer to distribute traffic across 3 public subnets.<br>- Set up an Auto Scaling Group (Desired: 1, Min: 1, Max: 3) and integrated Amazon SNS to send automated notifications.<br>- Tested the Auto Scaling feature by simulating heavy traffic using the WebStress tool.<br>- Practiced configuring 4 scaling mechanisms: Manual, Scheduled, Dynamic, and Predictive.                                                                                                                                                                                           | 14/05/2026 | 14/05/2026      | https://000006.awsstudygroup.com/vi/ |
| 6   | - Initialized a decoupled, high-availability Workshop-DB-Instance MySQL database on Amazon Lightsail.<br>- Initialized a cluster of 3 virtual machines (WordPress, PrestaShop, Akaunting) and assigned fixed Static IPs to each instance.<br>- Logged into the VMs via SSH, ran automated scripts to route all application data connections back to the central database.<br>- Enhanced deep-layer security by completely removing the SSH port (Port 22) from the firewalls of all 3 Lightsail VMs.<br>- Enabled Automated Snapshots and practiced virtual machine scale migration (upgrade) to a larger resource package without downtime.<br>- Configured automated email alerts when the system's CPU burst capacity percentage drops to a critical level. | 15/05/2026 | 15/05/2026      | https://000045.awsstudygroup.com/vi/ |

### Week 4 Achievements:

- Efficient Resource Governance:
  - Successfully implemented a systematic tagging system at scale, facilitating rapid resource querying and categorization.
  - Effectively operated AWS Resource Groups to centrally manage resources by department or project, simplifying the operational workflow.

- Intelligent Monitoring and Alerting System:
  - Proficient in metric visualization techniques, customizing advanced charts (secondary Y-axis, annotations), and utilizing mathematical expressions (Math Expressions) for data analysis.
  - Successfully configured CloudWatch Logs Insights to query application errors from log files and set up Metric Filters to convert logs into measurable metrics.
  - Built CloudWatch Alarms integrated with AWS SNS to send timely notifications during system incidents, ensuring high uptime.

- Scalable Application Architecture Deployment:
  - Successfully packaged applications (Custom AMI) and initialized a Multi-AZ architecture, enabling applications to be fault-tolerant and capable of handling high loads.
  - Configured Auto Scaling Groups in coordination with Application Load Balancers to automatically adjust server capacity based on actual CPU loads, optimizing the user experience.

- Operational Optimization with Amazon Lightsail:
  - Simultaneously deployed multiple applications (WordPress, PrestaShop, Akaunting) along with a shared database at optimized costs.
  - Successfully applied security best practices (disabling SSH and unnecessary ports) and operational management strategies (snapshot tier transitions, zero-downtime instance upgrades).
  - Established an alerting system based on CPU burst capacity metrics to monitor server resource health in real time.
