---
title: "Blog 1"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# **Redirecting Internet-bound traffic through a transparent forward proxy**

by Vijay Menon | on 08 SEP 2025 | in [Amazon VPC](https://aws.amazon.com/blogs/networking-and-content-delivery/category/compute/amazon-vpc/), [AWS Transit Gateway](https://aws.amazon.com/blogs/networking-and-content-delivery/category/networking-content-delivery/aws-transit-gateway/), [AWS Transit Gateway network manager](https://aws.amazon.com/blogs/networking-and-content-delivery/category/networking-content-delivery/aws-transit-gateway/aws-transit-gateway-network-manager/), [Networking & Content Delivery](https://aws.amazon.com/blogs/networking-and-content-delivery/category/networking-content-delivery/) | [Permalink](https://aws.amazon.com/blogs/networking-and-content-delivery/redirecting-internet-bound-traffic-through-a-transparent-forward-proxy/) | Share

Centralized egress is the principle of using a single, common inspection point for all network traffic going out to the Internet. This approach benefits security by limiting exposure to malicious resources accessible from outside, such as malware [command and control](https://en.wikipedia.org/wiki/Botnet#Command_and_control) (C&C) infrastructure. This inspection operation is typically performed by firewalls like [AWS Network Firewall](https://aws.amazon.com/network-firewall/), and customers often want to insert a forward proxy in the path with or without a firewall. Proxies can operate in two modes: [explicit proxy](https://en.wikipedia.org/wiki/Proxy_server) mode, where every client needing Internet access is configured to use an explicit proxy and sends supported outbound traffic through explicit proxy configuration. Such an implementation is described in [How to set up an outbound VPC proxy with domain whitelisting and content filtering](https://aws.amazon.com/blogs/security/how-to-set-up-an-outbound-vpc-proxy-with-domain-whitelisting-and-content-filtering/). However, there are systems that cannot be configured with explicit proxy, and customers often look for ways to transparently redirect traffic from such systems to the Internet through a proxy.

In this post, I explain an architecture that can be used to deploy a proxy on the egress path to the Internet and transparently redirect traffic to it using [Web Cache Communication Protocol (WCCP)](https://en.wikipedia.org/wiki/Web_Cache_Communication_Protocol). I will present a conceptual overview of implementing transparent proxy with WCCP in an [AWS Transit Gateway](https://aws.amazon.com/transit-gateway/)-based architecture. Specific implementation details may vary depending on your organization's requirements and chosen technology.

## **Real-world use cases**

Here are three real-world use cases.

1. **Secure internet access:** Organizations can use this architecture to ensure all outbound Internet traffic goes through security controls without requiring explicit proxy configuration on each client device.

2. **Data loss prevention:** Transparent traffic inspection allows businesses to detect and block sensitive data from leaving the network, even when endpoints don't support explicit proxy configuration.

3. **Regulatory compliance:** Industries with strict compliance requirements can perform continuous inspection and logging of all network traffic to meet regulatory standards.

## **Prerequisites**

Before starting, you should be familiar with the following AWS networking concepts and services:

- [Amazon Virtual Private Clouds (Amazon VPCs)](https://aws.amazon.com/vpc/)
- [Route tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
- [AWS Transit Gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html)
- [Transit Gateway Connect attachments](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-connect.html)
- [AWS Network Firewall](https://aws.amazon.com/network-firewall/)
- [NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)
- Third-party virtual appliances (WCCP-compliant routers and proxy servers) with WCCP functionality.

## **Architecture overview**

The architecture focuses on an Egress VPC containing WCCP-compliant virtual routers and proxy servers running on [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2/). These virtual routers redirect traffic to the proxy using WCCP. This setup allows transparent inspection and filtering of traffic without requiring client-side configuration changes. Figure 1 shows the diagram, followed by architectural details.

![Figure 1: Overall architecture diagram](/images/3-BlogsTranslated/3.1-Blog1/WCCPBlogArchitecture-v1-Page-1.jpg)

<p style="text-align: center;">Figure 1: Overall architecture diagram</p>

## **Key components**

**Transit Gateway:** Transit Gateway serves as the central hub for network connectivity, enabling simplified management of connections between VPCs and on-premises networks. In our architecture, Transit Gateway routes traffic between multiple Spoke VPCs, as well as between Spoke VPCs and the Internet through the Egress VPC for inspection.

**Transit Gateway Connect attachments:** Connect attachments provide the ability to integrate third-party virtual appliances with Transit Gateway. In our design, the attachments:

- Connect Transit Gateway with WCCP-compliant routers through [Generic routing encapsulation (GRE)](https://en.wikipedia.org/wiki/Generic_routing_encapsulation) running on Connect attachment
- Enable traffic redirection without modifying route tables in each VPC
- Provide flexibility for scaling and high availability

You can refer to [Simplify SD-WAN connectivity with AWS Transit Gateway Connect](https://aws.amazon.com/blogs/networking-and-content-delivery/simplify-sd-wan-connectivity-with-aws-transit-gateway-connect/) as a foundation for implementing Transit Gateway with Connect attachments. You can then modify the implementation to suit the requirements outlined in this post.

**Egress VPC:** The Egress VPC is a specialized environment:

- Contains WCCP-compliant routers and proxy servers running on Amazon EC2 in private subnets
- Contains firewalls in separate private subnets
- Enforces centralized security policies using proxies and firewalls
- Uses NAT Gateway in public subnets for Internet connectivity through Internet Gateway (IGW)

**WCCP-compliant routers running on Amazon EC2:** These are core components of the transparent proxy implementation:

- Located **inline** in the traffic path from Spoke VPCs to the Internet
- Intercept traffic based on configured policies
- Redirect specific traffic types to proxy servers
- Return processed traffic to the original path

**Proxy servers running on Amazon EC2:** These are Amazon EC2-based virtual appliances operating as forward proxies (e.g., [Squid](<https://en.wikipedia.org/wiki/Squid_(software)>)) that interact with and receive redirected traffic from the previously mentioned WCCP routing devices. Using WCCP, they apply configured policies to all egress traffic and forward to the next security function in the path. In this example, we use AWS Network Firewall. However, these proxies can be daisy-chained with other security/inspection systems, such as [Data Loss Protection](https://en.wikipedia.org/wiki/Data_loss_prevention_software) (DLP) systems, in the path before traffic is routed to the Internet.

## **Connectivity**

As shown in Figure 1, Spoke VPCs connect to Transit Gateway via VPC attachments. These attachments are associated with the Spoke VPC Route Table (routing will be explained in a later section). The Egress VPC connects to the same Transit Gateway via VPC attachment, and a Connect attachment is provisioned between Transit Gateway and Egress VPC through this VPC attachment. This Connect attachment is used to establish GRE tunnels between Transit Gateway and virtual appliances in the Egress VPC, acting as WCCP routers. This Egress VPC has Internet connectivity through an attached IGW.

## **Routing (refer to Figure 1)**

- Spoke VPCs: Each Spoke VPC needing Internet access has subnets attached to route tables containing a default route pointing to the Transit Gateway attached to that VPC. This configuration routes all Internet-bound traffic to the Transit Gateway, where the Spoke VPC's VPC attachment is associated with the Transit Gateway Spoke Route Table.

- Transit Gateway Configuration:

  - The Transit Gateway Spoke Route Table contains propagated routes for all Spoke VPCs and a default route propagated from the Connect attachment. This default route is created by the WCCP virtual appliance in the Egress VPC and advertised to Transit Gateway through BGP peering over the GRE tunnel.

  - On Transit Gateway, the Egress VPC attachment is associated with the Egress Route Table. This table contains routes propagated to the Egress VPC CIDR from the Egress VPC attachment, as well as routes propagated to all Spoke VPC CIDRs from their respective attachments.

  - The Connect attachment is associated with its own route table. This route table contains propagated Spoke VPC routes as well as the default route advertised by the WCCP router over the BGP session through the GRE tunnel.

- Egress VPC Configuration: The Egress VPC requires additional routing configuration to enable transparent proxy functionality.

  - WCCP router devices in private subnets establish GRE tunnels with Transit Gateway and create BGP peering sessions.

  - Through these BGP sessions, WCCP routers advertise the default route to Transit Gateway and receive all Spoke VPC prefixes.

  - WCCP routers redirect Internet-bound traffic to forward proxies in the same subnet using WCCP (detailed discussion will be provided later in this post).

- Subnet-specific Routing: private subnets (WCCP Router and Proxy servers).

  - Route tables have entries for Transit Gateway CIDR connect attachment peers pointing back to Transit Gateway.

  - Default route points to the firewall in a separate private subnet.

- Private subnets (firewalls):

  - Default route points to NAT Gateway in the public subnet of the corresponding [AWS Availability Zone (AZ)](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/).

  - Routes to WCCP router ENI in the same AZ for return traffic not matching WCCP redirect rules.

- Public Subnets (NAT Gateways):

  - Default route points to IGW.

  - Routes to firewall endpoint in the same AZ for return traffic not matching WCCP redirect rules.

## **WCCP redirection**

All Internet-bound traffic to WCCP routers is evaluated against configured WCCP redirect rules and forwarded to proxies in the same subnet. For redundancy, these WCCP routers configure **WCCP** redirection to connect with proxies in other AZs. WCCP redirection can be configured to handle all supported traffic or selected traffic types. Configuration mechanisms vary by WCCP virtual appliance vendor. Traffic to the proxy is evaluated and processed according to configuration, then forwarded to the firewall on the Internet egress path. As mentioned, if needed, proxies can be chained with other functions like DLP.

## **Packet walk-through**

The following figure outlines the packet journey.

![Figure 2: Architecture diagram with packet flow](/images/3-BlogsTranslated/3.1-Blog1/WCCPBlogArchitecture-v1-Page-2.jpg)

<p style="text-align: center;">Figure 2: Architecture diagram with packet flow</p>

**Forward path:** This section explains how packets travel from resources in Spoke VPCs to destinations on the Internet through proxies and firewalls in the Egress VPC.

- (A) Traffic from sources in Spoke VPCs destined for the Internet follows the default route in the subnet route table and enters Transit Gateway.

- (B) Once in Transit Gateway, it follows the route in the Spoke Route Table on Transit Gateway, which forwards traffic to the Transit Gateway Connect attachment. Multiple GRE tunnels run over the Connect attachment, all advertising default routes to Transit Gateway, so Transit Gateway uses Equal Cost Multi-Pathing (ECMP) to send traffic to WCCP virtual appliances in the Egress VPC.

- (C) The WCCP-virtual appliance intercepts traffic and determines if inspection is needed. Traffic requiring inspection is redirected to proxy servers, where security policies, content filtering, or other controls are applied before forwarding to Network Firewall.

- (CD) Traffic not matching WCCP redirect rules exits the WCCP virtual appliance and goes directly to Network Firewall according to the subnet route table.

- (D) Proxied traffic is Source NATed to the proxy's IP address and leaves the proxy for Network Firewall according to the subnet route table. This table has a default route pointing to the Network Firewall endpoint in the same AZ of the Egress VPC.

- (E) Network Firewall inspects the traffic and, if allowed, sends it to NAT Gateway in the same AZ of the Egress VPC according to the default route configured in its subnet route table.

- (F) NAT Gateway performs Source NAT on the traffic and sends it to the destination on the Internet.

**Reverse path:** This section explains how return packets travel from the Internet to resources in Spoke VPCs through proxies and firewalls in the Egress VPC.

- (G) Return traffic from the Internet enters the same NAT Gateway due to Source NAT.

- (H) According to the subnet route table, NAT Gateway forwards traffic to Network Firewall in the same AZ.

- (I) Network Firewall sends traffic to the proxy server in the same AZ if this flow in the forward direction matched WCCP redirect rules and was Source NATed by the proxy server.

- (J) The proxy server sends return traffic of the proxied flow to the WCCP router using WCCP configuration on the proxy server.

- (IJ) Return traffic of flows not matching redirect rules is sent by Network Firewall to the WCCP router according to the subnet route table.

- (K) Multiple GRE tunnels exist from WCCP routers to Transit Gateway via Connect attachment. Spoke VPC CIDRs are advertised to WCCP routers through these tunnels. WCCP routers use ECMP to send traffic to Transit Gateway through GRE tunnels.

- (L) Transit Gateway uses the Connect attachment route table to forward traffic to the corresponding Spoke VPC attachment.

- (M) In the Spoke VPC, traffic follows local routes to reach the destination from the Transit Gateway ENI.

## **Considerations**

Consider the following four points when implementing this solution.

1. **WCCP virtual appliance sizing**

- Ensure proper sizing of WCCP virtual appliances to handle expected traffic volumes. You can refer to [Amazon EC2 instance network bandwidth](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-network-bandwidth.html) documentation to select EC2 instances supporting your traffic requirements.
- Plan for redundancy by deploying across multiple AZs.
- Component-level redundancy (for WCCP routers or Proxy servers) can be implemented using [automatic instance recovery.](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-recover.html)

2. **WCCP configuration**

- Define service groups to classify traffic for different inspection policies as needed. Different service groups can be used for primary and secondary proxy servers.
- Configure redirection according to your requirements. You can use multiple attributes like port, protocol, source/destination addresses.
- Implement authentication between WCCP routers and proxy servers (outside the scope of this post).

3. **Proxy selection**

- Choose proxy solutions supporting WCCP integration.
- Consider performance requirements based on expected traffic volumes. Refer to [Amazon EC2 instance network bandwidth](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-network-bandwidth.html) documentation to select EC2 instances supporting your traffic requirements.

4. **Monitoring and logging**

- Implement comprehensive logging for both WCCP routers and proxy servers. Below are some examples of logs to collect. Since WCCP and proxy implementation depends on vendor/solution, these logs may be called by different names. Please refer to vendor documentation for details:

**On WCCP router:**

1. WCCP service status, packet redirection, and router-to-proxy communication logs
2. Interface traffic statistics
3. ACL match counts for WCCP-related rules
4. NetFlow/sFlow data for traffic analysis  
   **On proxy server:**
5. Access logs and Error logs (client IP, URL, status code, bytes transferred, timing, connection failures, timeouts)
6. WCCP service logs (service registration, group membership)
7. Cache performance logs (hit/miss ratio)
8. Connection handling logs (TCP connections, handshakes)
9. Authentication logs (if applicable)
10. SSL/TLS inspection logs (for HTTPS traffic)
11. System resource usage (CPU, memory, disk I/O)

- Set up alerts for traffic anomalies or proxy health issues, and create dashboards to visualize traffic patterns and security events. You can export the previously mentioned logs to [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) to set up alerts and create dashboards.

**Conclusion**

Implementing transparent proxies using WCCP with AWS Transit Gateway provides a powerful solution for organizations looking to enhance their security posture without disrupting user experience. Centralizing security controls in an egress VPC and using WCCP-compatible routers allows organizations to achieve comprehensive traffic inspection while maintaining network performance and scalability.

This architecture provides flexibility to adapt to changing security requirements and increasing network demands, making it an excellent choice for enterprises looking to strengthen their cloud security infrastructure. For more information and architectural options for centralized egress, visit the AWS Whitepaper, [Centralized egress to internet](https://docs.aws.amazon.com/whitepapers/latest/building-scalable-secure-multi-vpc-network-infrastructure/centralized-egress-to-internet.html).

<img src="/images/3-BlogsTranslated/3.1-Blog1/vijaymenon.jpeg" alt="Vijay_Menon" width="150" style="float: left; margin-right: 15px;"/>

**Vijay Menon**

Vijay Menon is a Principal Solutions Architect working in Singapore, with a background in large-scale networking and telecommunications infrastructure. He enjoys learning new technologies and helping customers solve complex technical problems by providing solutions using AWS products and services. When not supporting customers, he enjoys long-distance running and spending time with family and friends.
