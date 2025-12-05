---
title: "Week 2 Worklog"
date: "2025-09-15"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

- **Understand AWS VPC:** Grasp the basic concepts of VPC (Virtual Private Cloud) as an isolated logical network environment, including key components like Subnets (Public and Private), Route Tables, and ENI.
- **Traffic Control and Security:** Learn to configure security layers (Security Groups and NACLs) and control network traffic flow to/from the Internet (Internet Gateway and NAT Gateway).
- **Complex Network Connectivity:** Differentiate and know how to use methods for connecting VPCs (VPC Peering) and the central connection model (Transit Gateway).
- **Build a Hybrid Cloud Environment:** Learn about solutions for connecting on-premises networks with AWS, including VPN (Site-to-Site) and private connections (AWS Direct Connect).
- **Application Load Balancing:** Understand the function of Elastic Load Balancing (ELB) and differentiate between various load balancer types (ALB, NLB, CLB, GLB) to ensure high availability and scalability for applications.


### Tasks to be carried out this week:

| Day 	| Task 	| Start Date 	| Completion Date 	| Reference Material 	|
|---	|---	|---	|---	|---	|
| 2 	| - Learn about AWS Virtual Private Cloud (VPC)<br>+ What is VPC?<br>+ How does the VPC structure work?<br>- Learn about VPC-Subnets and Subnet architecture?<br>- Learn about VPC-Route Table?<br>- Learn about VPC-ENI and VPC-ENI architecture?<br>- Learn about VPC-Endpoint and VPC-Endpoint architecture?<br>- Learn about VPC-Internet Gateway and VPC-Internet Gateway architecture?<br>- Learn about VPC-NAT Gateway and VPC-NAT Gateway architecture?<br>- Learn about VPC-Security Group and VPC-Security Group architecture?<br>- Learn about VPC-NACL and VPC-NACL architecture?<br>- Learn about VPC-Flow Logs 	| 15/09/2025 	| 15/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md)  	|
| 3 	| - Learn about networking services on AWS?<br>- Learn about VPC Peering and its architecture?<br>- Learn about Transit Gateway and its architecture?<br>- Understand the concepts of VPN & Direct Connect services?<br>- What is Site-to-Site VPN? How to set it up?<br>- Learn about Client-to-Site VPN?<br>- What is AWS Direct Connect? 	| 16/09/2025 	| 16/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md) 	|
| 4 	|  - Learn about the concepts and overview of Elastic Load Balancing? And the current types of ELB?<br>- Learn about ELB - Application Load Balancer and its architecture?<br>- Learn about ELB - Network Load Balancer and understand the concept?<br>- Learn about ELB - Classic Load Balancer and understand the concept?<br>- Learn about ELB - Gateway Load Balancer and its architecture?  	| 17/09/2025 	| 17/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md)  	|
| 5 	| - **Lab 03** - VPC Initialization<br>  1. Configure VPC Firewall<br>  2. Practice Creating a VPC<br>  3. Configure Site to Site VPN<br>- **Lab 58** - System Manage - Session Manage<br>  1. Create Connection to EC2 Server<br>  2. Manage Session Logs <br>  3. Use Port Forwarding<br>- **Lab 19** - Set Up VPC Peering<br>  1. Update Network ACL<br>  2. Create Peering Connection <br>  3. Configure Route Tables<br>  4. Enable Cross-Peer DNS" 	| 18/09/2025 	| 18/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md)  	|
| 6 	| - **Lab 20** - Transit Gateway Setup<br>  1. Infrastructure Setup<br>  2. Create Transit Gateway -> Connect Multiple VPCs Together<br>  3. Transit Gateway Attachments<br>  4. Create Route Table for TGW<br>  5. Add Gateway to Route Tables & Check Results<br>- **Lab 10** - Hybrid DNS<br>  1. Hybrid DNS Setup<br>  2. Create Outbound Endpoint<br>  3. Create Route 53 Resolver Rule<br>  4. Create Inbound Endpoint.<br>- Additional research on **AWS Advanced Networking - Specialty Study Guid** 	| 19/09/2025 	| 19/09/2025 	| [Module 02](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_02/Take_notes_module_02.md) <br> [Research Link](https://www.amazon.com/Certified-Advanced-Networking-Official-Study/dp/1119439833)  	|

### Week 2 Achievements:

- **Explain** what VPC is, its role in AWS, and its core components (Subnet, Route Table, ENI).
- **Clearly differentiate** between a Public Subnet (with an Internet Gateway) and a Private Subnet (using a NAT Gateway for Internet access).
- **Compare and contrast** the two main firewall mechanisms: Security Group (stateful, applies to ENI) and NACL (stateless, applies to Subnet).
- **Present** how to privately connect from a VPC to AWS services (like S3) without going over the Internet using a VPC Endpoint.
- **Evaluate** the pros and cons of two VPC connection solutions: VPC Peering (1:1 connection, no transitive support) and Transit Gateway (hub-and-spoke model, simplifies management).
- **Describe** methods for establishing a hybrid cloud connection, including Site-to-Site VPN (over the Internet) and AWS Direct Connect (private physical connection).
- **Classify** and **select** the appropriate Elastic Load Balancer type for specific scenarios:
   + **Application Load Balancer (ALB):** For HTTP/HTTPS traffic (Layer 7), supports path-based routing.
   + **Network Load Balancer (NLB):** For TCP/TLS traffic (Layer 4), requires ultra-high performance and static IP.
   + **Gateway Load Balancer (GLB):** Used for integrating virtual appliances.
- **Identify** the necessary labs to reinforce knowledge of VPC, Peering, Transit Gateway, and related services.



