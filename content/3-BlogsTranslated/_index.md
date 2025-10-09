---
title: "Translated Blogs"
date: "2025-09-09"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

This section will list and introduce the blogs you have translated. For example:

### [Blog 1 - Building resilient multi-Region Serverless applications on AWS](3.1-Blog1/)

Mission-critical applications demand high availability and resilience against potential disruptions. In online gaming, millions of players connect simultaneously, making availability challenges evident. When gaming platforms experience outages, players lose progress, tournaments get disrupted, and brand reputation suffers. Traditional environments often overprovision compute to address these challenges, resulting in complex setups and high infrastructure and operation costs. Modern Amazon Web Services (AWS) serverless infrastructure offers a more efficient approach. This post presents architectural best practices for building resilient serverless applications, demonstrated through a multi-Region serverless authorizer implementation.

### [Blog 2 - Redirecting internet bound traffic through a transparent forward proxy](3.2-Blog2/)

Centralized egress is the principle of using a single, common inspection point for all network traffic destined for the internet. This approach is beneficial from a security perspective because it limits exposure to externally accessible malicious resources, such as malware command and control (C&C) infrastructure. This inspection is generally done by a firewall like AWS Network Firewall and customers often also want to insert a forward proxy in the path with or without firewalls. Proxies can work in two modes: explicit proxy mode, where all clients needing access to the internet are configured with explicit proxy and send supported outbound traffic using explicit proxy configuration. One such implementation is described in the post, How to set up an outbound VPC proxy with domain whitelisting and content filtering. However, there are systems that cannot be configured with explicit proxy, and customers often look for a way to transparently redirect traffic from such systems going toward the internet through a proxy. In this post I explain an architecture that can be used to deploy a proxy in internet egress path and redirect traffic to it transparently using Web Cache Communication Protocol (WCCP). I’ll walk through a conceptual overview of implementing transparent proxies with WCCP in an AWS Transit Gateway based architecture. Specific implementation details may vary based on your organization’s requirements and chosen technologies.

### [Blog 3 - AWS Weekly Roundup: AWS Transform, Amazon Neptune, and more (September 8, 2025)](3.3-Blog3/)

This blog introduces AWS Community Day Netherlands 2025

### [Blog 4 - ...](3.4-Blog4/)

This blog introduces how to start building a data lake in the healthcare sector by applying a microservices architecture. You will learn why data lakes are important for storing and analyzing diverse healthcare data (electronic medical records, lab test data, medical IoT devices…), how microservices help make the system more flexible, scalable, and easier to maintain. The article also guides you through the steps to set up the environment, organize the data processing pipeline, and ensure compliance with security & privacy standards such as HIPAA.

### [Blog 5 - ...](3.5-Blog5/)

This blog introduces how to start building a data lake in the healthcare sector by applying a microservices architecture. You will learn why data lakes are important for storing and analyzing diverse healthcare data (electronic medical records, lab test data, medical IoT devices…), how microservices help make the system more flexible, scalable, and easier to maintain. The article also guides you through the steps to set up the environment, organize the data processing pipeline, and ensure compliance with security & privacy standards such as HIPAA.

### [Blog 6 - ...](3.6-Blog6/)

This blog introduces how to start building a data lake in the healthcare sector by applying a microservices architecture. You will learn why data lakes are important for storing and analyzing diverse healthcare data (electronic medical records, lab test data, medical IoT devices…), how microservices help make the system more flexible, scalable, and easier to maintain. The article also guides you through the steps to set up the environment, organize the data processing pipeline, and ensure compliance with security & privacy standards such as HIPAA.
