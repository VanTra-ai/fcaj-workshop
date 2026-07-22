---
title: "Week 5 Worklog"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

- Mastered static website distribution, leveraging CDN to accelerate and secure data, while mastering advanced features like Versioning for robust data protection.
- Thoroughly understood disaster recovery methodologies (RPO/RTO) and how to automate backup, recovery, and status notification processes for the entire cloud resource ecosystem.
- Proficient in the virtual machine migration process between on-premises virtualization environments (VMware) and Amazon EC2.
- Understood how to seamlessly connect and synchronize data between corporate network file shares and S3 cloud storage.
- Mastered fully managed shared file storage solutions integrated with Windows Active Directory for large enterprise applications, utilizing both the console and CLI.

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                   |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------ |
| 2   | - Researched S3 Object Storage theory, Storage Classes, and Access Points features.<br>- Initialized an S3 Bucket in Singapore, uploaded source code, and configured Static Website Hosting.<br>- Configured public access permissions for website files via Block Public Access and Object ACLs.<br>- Integrated Amazon CloudFront CDN to accelerate static website loading and block direct access to S3.<br>- Enabled S3 Versioning for multi-version storage, practiced deleting and recovering original data.<br>- Performed object migration (Move) to a new bucket and cleaned up all lab resources.                                                                                                            | 18/05/2026 | 18/05/2026      | https://000057.awsstudygroup.com/vi/ |
| 3   | - Researched centralized backup management theory, RPO/RTO recovery metrics, and Disaster Recovery strategies.<br>- Rapidly deployed automated Lab infrastructure (EC2, SNS, Lambda) using AWS CloudFormation.<br>- Initialized a Backup Vault and set up a Backup Plan configuring automated backup schedules based on tags.<br>- Integrated AWS SNS to automatically send email notifications when backup/restore statuses are completed.<br>- Performed data recovery testing from backups and monitored operation logs on CloudWatch Logs.                                                                                                                                                                         | 19/05/2026 | 19/05/2026      | https://000013.awsstudygroup.com/vi/ |
| 4   | - Researched VM Import/Export theory and system migration processes to the cloud.<br>- Configured a local Ubuntu virtual machine on VMware Workstation and exported it as a virtual disk file in .ova/.vmdk format.<br>- Created an S3 Bucket and used the AWS CLI to upload the virtual disk file from a personal computer to cloud storage.<br>- Set up an IAM Role (vmimport) and assigned a Trust Relationship to allow the service to access files on S3.<br>- Used the aws ec2 import-image command to convert the virtual disk file into a Custom AMI and tracked progress via the CLI.<br>- Launched a new EC2 instance from the successfully converted AMI, checked the system, and cleaned up lab resources. | 20/05/2026 | 20/05/2026      | https://000014.awsstudygroup.com/vi/ |
| 5   | - Researched Hybrid Storage theory and types of AWS Storage Gateway.<br>- Initialized an S3 Bucket as the primary raw data repository for the Storage Gateway connection.<br>- Launched an EC2 instance using a dedicated Gateway AMI image and attached a 150 GiB EBS volume for caching.<br>- Configured Storage Gateway, created an SMB File Share linked to the S3 Bucket, and enabled Guest access.<br>- Mounted the File Share as network drive Z: on a Windows workstation and verified synchronization to S3.                                                                                                                                                                                                  | 21/05/2026 | 21/05/2026      | https://000024.awsstudygroup.com/vi/ |
| 6   | - Researched Amazon FSx for Windows File Server theory, the SMB protocol, and data deduplication features.<br>- Deployed VPC network infrastructure and set up Directory Service (AWS Managed Microsoft AD).<br>- Initialized the Amazon FSx file system, configured storage capacity, and integrated it into the Active Directory domain.<br>- Launched a Windows Client EC2 instance and joined it to the AD domain for authentication.<br>- Mounted the FSx shared drive on the Windows Client via the SMB protocol and verified data read/write operations.                                                                                                                                                        | 22/05/2026 | 22/05/2026      | https://000025.awsstudygroup.com/vi/ |

### Week 5 Achievements:

- Mastering S3 Static Hosting and CDN CloudFront:
  - Successfully deployed a static travel website to S3, configuring acceleration via CloudFront to optimize page load latency from ~600ms down to an impressive ~13ms using Edge Locations in Vietnam.
  - Successfully enabled S3 Versioning to store multiple versions of files, granting the system the ability to fully recover original data even when overwritten by a ransomware attack.
  - Successfully migrated (moved) all objects to a new bucket within the same region quickly.

- Data Automation with AWS Backup:
  - Successfully set up an automated infrastructure cluster via CloudFormation. Accurately initialized a Backup Vault and a Backup Plan to automatically scan resources based on tags.
  - Successfully configured AWS SNS to automatically send email notifications to the Operations team upon the completion of backup creation or data restoration.

- On-Premise Virtual Machine Migration to Cloud via VM Import/Export:
  - Successfully built a local Ubuntu virtual machine on VMware Workstation, packaged and exported it as a .vmdk virtual disk file, and uploaded it to S3.
  - Successfully created the vmimport IAM role and used the AWS CLI to convert the virtual disk file into a Custom AMI, successfully launching a stable EC2 instance on the cloud.

- Hybrid Network File Share Deployment with Storage Gateway:
  - Successfully configured a Storage Gateway virtual server cluster on EC2 combined with a 150 GiB caching EBS volume.
  - Successfully created an SMB File Share cluster linked to S3, mounted it as network drive Z: on a local computer, and synchronized data directly to the cloud

- Enterprise File Server Operations with Amazon FSx:
  - Successfully deployed an AWS Managed Microsoft Active Directory directory management cluster and a high-reliability Amazon FSx for Windows Multi-AZ file system.
  - Launched a Windows Client EC2 instance, joined it to the AD domain, and successfully mounted the FSx network drive for secure file reading and writing.
