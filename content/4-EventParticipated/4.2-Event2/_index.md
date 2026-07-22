---
title: "Event 2"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Summary Report: “FCAJ Community Day: Data Driven, AI Risen”

### Event Objectives

- Share real-world perspectives and enterprise use cases on applying Artificial Intelligence (AI) and Cloud technologies.
- Update participants on the latest trends in AI Agents (Voice AI, DevOps AI, Amazon Q) and how AI is reshaping the IT job market.
- Introduce architectural and technical solutions, from choosing between Single-Agent and Multi-Agent architectures to implementing secure connectivity for enterprise AI systems.

### Speakers

- **Steve Tran** – CTO/Founder, Cloud Thinker
- **Danh Hieu Nghi** – AI Engineer, Renova Cloud
- **Tran Tuan Kiet** – AI Engineer, AWS Student Builder Group
- **Vu Quoc Trung** – CEO, Revve AI
- **Phan Thi Bao** & **Nguyen Dinh Nguyen** – Cloud Engineers, Cloud Kinetics
- **Tran Nhat Truong (Wayne)** & **Dang Thi Minh Anh** – Solution Sales, Noventiq
- **Nguyen Tan Toan** – AWS Security Builder

### Key Highlights

#### Career Transformation and AI Solutions for Cloud Operations (Agentic Platform)

- AI is significantly accelerating software development but is also creating bottlenecks in quality assurance (QA/QC) and infrastructure operations.
- Cloud Thinker introduced AI Agent solutions that automate incident management, infrastructure code review, FinOps, and security testing.
- **Single-Agent vs. Multi-Agent:** A well-designed Single-Agent system can solve approximately 95% of common use cases. Multi-Agent architectures are more complex but become necessary for implementing Role-Based Access Control (RBAC) and overcoming context window limitations.

#### Building Voice AI Agents

- Compared two architectures:
  - Direct Speech-to-Speech
  - Three-stage pipeline: **Speech-to-Text (STT) → Large Language Model (LLM) → Text-to-Speech (TTS)**
- For Vietnamese, a low-resource language, the three-stage architecture provides better content control and more accurate tool calling for banking and enterprise applications.
- Practical challenges include reducing latency through streaming, recognizing speaker gender for appropriate pronouns, and handling interruptions during conversations.

#### AWS DevOps AI Agent for Automated System Troubleshooting

- Addressed the issue of fragmented telemetry, where scattered logs make troubleshooting inefficient.
- Introduced a four-stage AI workflow:
  - **Triage**
  - **Investigation**
  - **Mitigation**
  - **Improvement**
- Emphasized an important safety principle: AI should only provide recommendations, while humans remain responsible for approving and executing actions.

#### Amazon Q Business for Human Resources

- Demonstrated how Amazon Q addresses the inefficiencies of manual resume screening, reduces the risk of overlooking qualified candidates, and minimizes subjective evaluation.
- Amazon Q can automatically generate job descriptions (JDs), extract information from resumes, score candidates against job requirements, and produce comparison reports quickly while maintaining data security.

#### Securing Connectivity Between Amazon Q and MCP Servers

- Enterprise AI systems should not expose public endpoints due to risks such as Distributed Denial-of-Service (DDoS) attacks and Man-in-the-Middle (MitM) attacks.
- The recommended solution is to deploy the MCP Server inside a **Private Subnet**, using **VPC Interface Endpoints**, **Route 53 Resolver**, and an **Application Load Balancer (ALB)** to establish secure private communication with Amazon Q.

### Key Takeaways

#### Design and Operations Mindset

- **AI Supports Rather Than Replaces Humans:** AI should improve productivity rather than replace human decision-making, especially in high-risk production environments.
- **Understand the Fundamentals:** Developers should never rely solely on AI-generated outputs. Strong foundational knowledge is essential for validating AI-generated results, particularly in DevOps and Data Engineering.

#### Technical Architecture

- **Observability Is the Foundation:** DevOps AI Agents can only operate effectively when systems provide comprehensive logs, metrics, and traces.
- **Voice AI Architecture:** Learned the complete streaming workflow from Speech-to-Text through LLM processing to Text-to-Speech, enabling low-latency real-time interactions.
- **Zero Trust Security:** Any SaaS service, such as Amazon Q, accessing internal systems should communicate through private infrastructure, including Virtual Private Clouds (VPCs) and Private Subnets.

#### AI Integration Strategy

- AI applications should mitigate hallucination risks by restricting the Agent's operational scope and incorporating deterministic rules wherever possible.

### Applying to Work

- **Enhancing Personal Projects:** Instead of building only traditional CRUD applications, I plan to integrate the **Model Context Protocol (MCP)** so AI can securely interact with databases and external systems.
- **Security-First Design:** Apply Private Subnet and VPC networking principles when developing cloud-based academic projects rather than exposing unnecessary public endpoints.
- **Improving My Resume:** Optimize my CV using relevant technical keywords because many companies now use AI-powered resume screening before human review.

### Event Experience

Participating in the **"FCAJ Community Day"** workshop provided me with a completely new perspective on how AI is applied in enterprise environments. The event demonstrated that AI is far more than a chatbot—it has become an essential component of modern software systems and business operations.

#### Learning from Industry Experts

- Listening directly to founders, CTOs, and senior engineers helped me recognize the gap between academic knowledge and real-world enterprise requirements, particularly in system operations, cost optimization, and security.

#### Hands-on Technical Experience

- I was highly impressed by the live demonstration of a Voice AI Agent answering questions about MacBook products entirely through voice interaction. It clearly illustrated the technical challenges of minimizing latency and handling conversational interruptions.
- Another memorable demonstration simulated a Distributed Denial-of-Service (DDoS) attack and showed how a DevOps AI Agent analyzed system logs to identify the actual root cause, providing a realistic view of production-level operations.

#### Modern AI Tools in Practice

- I was amazed by Amazon Q's ability to automatically analyze dozens of resumes and generate candidate evaluation reports within seconds, demonstrating the practical value of AI in recruitment.

#### Networking and Discussion

- The event featured many insightful questions from attendees, helping me realize that while technical knowledge is important, understanding and solving business problems is the ultimate objective of technology.

#### Key Takeaways

- AI is evolving at an extraordinary pace. Instead of using AI merely to automate traditional tasks, developers should leverage AI to amplify their capabilities and solve more complex problems.
- Technologies and tools may change rapidly, but architectural principles and security best practices remain fundamental and timeless.
- Career opportunities are not disappearing; however, employer expectations are increasing significantly. Modern software engineers are expected to possess both advanced technical expertise and practical AI experience. Therefore, students should continuously improve their skills and build high-quality side projects that demonstrate real-world capabilities.

#### Some event photos

