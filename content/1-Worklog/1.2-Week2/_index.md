---
title: "Week 2 Worklog"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

- Mastered the design and deployment of isolated network environments in AWS, understanding routing mechanisms, subnetting, and Internet connectivity.
- Mastered two firewall tools: Security Groups (Stateful) and Network ACLs (Stateless) to protect resources at the Instance and Subnet levels.
- Practiced building complex connectivity models: Site-to-Site VPN (Hybrid Cloud), VPC Peering (internal connection between VPCs), and Transit Gateway.
- Integrated the DNS system between a simulated on-premise environment (Managed AD) and AWS using Route 53 Resolver (Inbound/Outbound Endpoints).

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Start Date | Completion Date | Reference Material                                                                                               |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ---------------------------------------------------------------------------------------------------------------- |
| 2   | - Overview of Amazon VPC: isolated virtual network architecture, IP address ranges (CIDR), network segmentation with Subnets, Route Tables, and Internet Gateway.<br>- Researched firewall mechanisms within VPC: Security Groups (stateful) and Network ACLs (stateless) for resource protection.<br>- Explored Multi-AZ architecture and NAT Gateway to enable one-way Internet access from Private Subnets.                                                                  | 27/04/2026 | 27/04/2026      | https://000003.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |
| 3   | - Practiced VPC & EC2 creation:<br>+Initialized VPC ASG (10.10.0.0/16), created 2 Public Subnets and 2 Private Subnets across 2 different AZs.<br>+ Configured Route Tables: Public (connected to IGW) and Private (connected to NAT Gateway).<br>+ Deployed 2 EC2 instances: Public EC2 (direct Internet connection) and Private EC2 (SSH via Public EC2).<br>+ Configured Security Groups to allow SSH and ICMP, and verified network connectivity between the two instances. | 28/04/2026 | 28/04/2026      | https://000003.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |
| 4   | - Researched Hybrid Cloud model and AWS Site-to-Site VPN: Roles of Virtual Private Gateway (VGW) and Customer Gateway (CGW).<br>- Practiced VPN:<br>+ Established a VPN tunnel connection between 2 VPCs (simulating an on-premise branch).<br>+ Configured VPN using an EC2 instance running StrongSwan/Libreswan software.<br>+ Practiced configuring ipsec.conf and ipsec.secrets files and verified successful tunnel connection via Private IP Ping commands.              | 29/04/2026 | 29/04/2026      | https://000003.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |
| 5   | - Set up Hybrid DNS with Route 53:<br>+ Researched Hybrid DNS mechanisms: Outbound/Inbound Endpoints and Resolver Rules.<br>+ Initialized AWS Managed Microsoft AD to simulate an on-premise DNS system.<br>+ Configured Outbound Endpoint and Resolver Rule to forward onprem.example.com queries to the AD.<br>+ Configured Inbound Endpoint for reverse DNS resolution from the AD back to AWS.<br>+ Tested DNS via nslookup and Resolve-DnsName.                            | 30/04/2026 | 30/04/2026      | https://000010.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |
| 6   | - Practiced VPC Peering & NACL:<br>+ Established VPC Peering between My VPC and HG VPC.<br>+ Configured NACL for HG VPC subnet, restricting source IPs to allow traffic only from My VPC (172.31.0.0/16).<br>+ Enabled Cross-Peer DNS resolution to resolve Private IPs via DNS names across the peering connection.<br>+ Clean-up: Terminated EC2 instances, deleted Peering Connections, Security Groups, and related CloudFormation Stacks.                                  | 01/05/2026 | 01/05/2026      | https://000019.awsstudygroup.com/vi/<br>https://www.youtube.com/playlist?list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i |

### Week 2 Achievements:

- VPC & Network Knowledge:
  - Thoroughly understood network design according to the Well-Architected Framework standards: utilizing Multi-AZ and separating Public/Private Subnets.
  - Proficient in firewall management: Setting up Security Groups for application tiers (Web server, Database) and applying NACLs to filter traffic at the Subnet level.
  - Successfully configured NAT Gateways and Internet Gateways to manage Internet traffic flow for resources.

- Hybrid & Peering Connectivity Knowledge:
  - Successfully implemented Site-to-Site VPN using the IPsec Tunnel model (StrongSwan), enabling secure communication between the simulated on-premise environment and AWS.
  - Established VPC Peering, understood the limitations of transitive peering, and how to enable Cross-Peer DNS for name resolution between VPCs.
  - Mastered Route Table and Route Propagation administration to direct internal traffic.

- Systems & Tools Skills:
  - Built a Hybrid DNS system with Route 53 Resolver, effectively connecting to the AWS Managed Microsoft AD service.
  - Familiarized with VPC Reachability Analyzer to inspect packet paths and VPC Flow Logs to monitor/detect anomalous traffic.
  - Proficiently operated Infrastructure as Code (CloudFormation) to deploy network infrastructure consistently and reproducibly.
  - Practiced resource clean-up (Terminating EC2 instances, Releasing EIPs, Deleting Gateways/Peerings) to optimize internship costs.
