---
title: "Blog 2"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# **Building resilient multi-Region Serverless applications on AWS**

by Vamsi Vikash Ankam | on 08 SEP 2025 | in [Advanced (300)](https://aws.amazon.com/blogs/compute/category/learning-levels/advanced-300/), [Resilience](https://aws.amazon.com/blogs/compute/category/resilience/), [Serverless](https://aws.amazon.com/blogs/compute/category/serverless/), [Technical How-to](https://aws.amazon.com/blogs/compute/category/post-types/technical-how-to/) | [Permalink](https://aws.amazon.com/blogs/compute/building-resilient-multi-region-serverless-applications-on-aws/) | Share

Mission-critical applications demand high availability and resilience against potential disruptions. In online gaming, millions of players connect simultaneously, making availability challenges particularly apparent. When gaming platforms fail, players lose progress, tournaments are disrupted, and brand reputation suffers. Traditional environments often over-provision compute resources to address these challenges, leading to complex setups along with high infrastructure and operational costs. Modern Amazon Web Services [(AWS) serverless](https://aws.amazon.com/serverless/) infrastructure offers a more efficient approach. This post presents architectural best practices for building resilient serverless applications, illustrated through implementing a multi-[Region](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) serverless authorization mechanism.

## **Overview**

Recognizing the importance of availability only after experiencing disaster is too late. Applications can fail for many reasons such as infrastructure failures, source code errors, configuration errors, unexpected traffic surges, or service disruptions at the regional level. Critical business services such as authentication systems, payment processors, and real-time gaming features require high availability. To minimize impact on user experience and business revenue, establish [bounded recovery times](https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-multi-region-fundamentals/fundamental-1.html) for critical services during incidents.

AWS serverless architectures inherently provide high availability through multi-Availability Zone (AZ) deployment and integrated scalability. These services minimize infrastructure management while operating on a pay-for-value pricing model at the Regional level. The AWS serverless pay-for-value model enables cost-effective multi-Region deployment, making it an ideal choice for building resilient architectures.

![Figure 1: Diagram showing failure causes, their impact and frequency of occurrence](/images/3-BlogsTranslated/3.1-Blog2/image-1-5.png)

<p style="text-align: center;">Figure 1: Diagram showing failure causes, their impact and frequency of occurrence</p>

The previous diagram maps failures—from common operational errors to rare catastrophic events. It guides organizations to prioritize multi-Region recovery strategies based on occurrence probability and potential business impact.

## **Regional decisions**

To determine the appropriate multi-Region approach, carefully evaluate the following factors:

1. Assess whether your [Recovery Time Objective (RTO) and Recovery Point Objective (RPO)](https://aws.amazon.com/blogs/mt/establishing-rpo-and-rto-targets-for-cloud-applications/) requirements can be met within a single Region, or if a multi-Region architecture is necessary to achieve your recovery objectives.
2. Whether the business benefits of multi-Region redundancy outweigh the operational costs of data replication, synchronization, and increased deployment costs and complexity.
3. Evaluate whether data sovereignty laws, compliance requirements, or geographic restrictions prevent data replication between specific AWS Regions.
4. Ensure that Regions selected in a "multi-Region" solution have compatible service capabilities, quota limits, and pricing appropriate to your needs.

After evaluating these requirements, if the organization determines the need for multi-Region workloads, they must choose between two architectural patterns: Active-Passive or Active-Active deployment. Each pattern offers distinct benefits and trade-offs regarding resilience, cost, and operational complexity.

## **Multi-Region deployment patterns**

The following sections outline different multi-Region deployment patterns: Active-Passive, and Active-Active.

### **Active-Passive**

In this pattern, one AWS Region serves as the "Active" Region, handling all production traffic, while other Region(s) remain in "Passive" state, as shown in the following figure. Passive Region(s) replicate data and configuration from the Active Region without serving requests, and are ready to handle when disruptions occur in the "Active" Region. Depending on application criticality, passive Regions deploy different levels of infrastructure readiness: fully deployed infrastructure (Hot Standby), partial deployment (Warm Standby), or minimal core infrastructure (Pilot Light).

Traditional Active-Passive architectures require significant investment in idle infrastructure: load balancers, auto-scaling groups, running compute resources, and monitoring systems. Organizations can use AWS serverless applications with pay-for-value pricing model to primarily pay for data replication costs, not idle compute resources. AWS manages the underlying infrastructure, eliminating most operational costs.

Service quotas, API limits, and concurrency settings must correspond across AWS Regions to provide seamless failover capability. [AWS Lambda](https://aws.amazon.com/lambda/) provides [provisioned concurrency](https://docs.aws.amazon.com/lambda/latest/dg/provisioned-concurrency.html) to keep functions warm and responsive, particularly useful for secondary Regions during failover. It helps reduce cold starts by maintaining warm execution environments, so the system can handle traffic surges with fewer cold starts. Note that provisioned concurrency incurs compute [costs](https://aws.amazon.com/lambda/pricing/) regardless of usage level. Consider implementing auto-scaling for provisioned concurrency based on traffic patterns to optimize costs during idle periods.

This pattern suits organizations seeking cost-effective disaster recovery (DR) solutions, because AWS serverless costs only apply when resources are actively used in the secondary Region. Managed services like [Amazon DynamoDB Global Tables](https://aws.amazon.com/dynamodb/) and [Amazon Aurora Global Database](https://aws.amazon.com/rds/aurora/) handle data replication, simplifying deployment. The serverless authorization mechanism presented in the following section illustrates this pattern in practice.

![Figure 2:](/images/3-BlogsTranslated/3.1-Blog2/image-2-4.png)

<p style="text-align: center;">Figure 2: Active-Passive pattern with dotted lines indicating standby Regions, while Active-Active pattern serves traffic simultaneously</p>

### **Active-Active**

In this pattern, multiple Regions serve traffic simultaneously, distributing load and providing rapid failover capability. Active-Active architecture is [expensive](https://aws.amazon.com/blogs/architecture/understand-resiliency-patterns-and-trade-offs-to-architect-efficiently-in-the-cloud/) and designed for the highest availability level. However, they don't by default provide DR for all potential failure types. This approach suits applications requiring geographic routing, or demanding the highest availability.

Active-Active deployment requires rigorous engineering to handle data synchronization and resolve conflicts. Each Region must be sized to carry the full application load if another Region experiences service degradation. Active users are distributed across AWS Regions, so disruption in one Region will redirect all traffic to remaining Regions, requiring them to handle the combined load. To improve application resilience, implement [retry mechanisms](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/), [circuit breaker](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/circuit-breaker.html), and fallback strategies. Plan for [static stability](https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/static-stability.html) by pre-provisioning capacity and applying client-side caching. Services like [Amazon Route 53](https://aws.amazon.com/route53/) with latency-based routing and [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) Global Tables with [strong consistency](https://aws.amazon.com/blogs/aws/build-the-highest-resilience-apps-with-multi-region-strong-consistency-in-amazon-dynamodb-global-tables/) provide foundation but require thorough testing under various failure scenarios. This post does not cover Active-Active deployment.

## **Multi-Region serverless authorizer**

To illustrate the Active-Passive scenario, we build a sample application showing how to build a multi-Region serverless authorizer using [Amazon API Gateway](https://aws.amazon.com/api-gateway/), [Lambda](https://aws.amazon.com/pm/lambda/?refid=1992d44e-5bf5-47d8-8711-4ea10542b61b) functions and Amazon Route53. Modern gaming and entertainment platforms host critical services like player matchmaking, live streaming, and real-time sports analytics. These services depend on robust authorization systems—when authorization fails, players cannot join matches, viewers lose stream access, and live events become unavailable. This post presents how to build a fault-tolerant, multi-Region serverless authorizer while maintaining lower costs compared to traditional approaches.

Serverless multi-Region architecture typically includes Routing, Compute, and Data layers. When implementing multi-Region deployments, data replication between AWS Regions is essential, regardless of compute services used. The compute layer must prioritize idempotency to ensure safe event processing across AWS Regions.

Use [Powertools for Lambda](https://docs.aws.amazon.com/powertools/python/latest/utilities/idempotency/) to handle idempotency efficiently, or implement custom solutions using unique event IDs with DynamoDB as an idempotent store. While the post focuses on authorizer service deployment, this pattern can be applied to build multi-Region microservices for various critical functions, such as game session management, content distribution orchestration, user preference management, and profile services.

## **Demo overview**

To illustrate multi-Region serverless authorizer operation, we can examine the workflow:

1. Frontend application authenticates with Identity Provider to obtain authentication token.

2. Authentication token is sent to a resilient multi-Region DNS endpoint, hosted on Route 53 in this demo.

3. Route 53 routes requests with token to API Gateway in primary Region.

4. Route 53 monitors application health using a Lambda function simulated in this demo. In production environments, implement deep health checks to monitor the entire service stack.

5. When authorization succeeds, application receives response. If Route 53 detects degradation in primary Region, it triggers [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) alarm, which application owners can use to evaluate and approve traffic redirection to secondary Region.

6. New traffic will be routed to API Gateway in secondary Region after manual failover approval.

7. Route 53 health checks continue monitoring primary Region health and restore traffic routing when this Region recovers.

![Figure 3](/images/3-BlogsTranslated/3.1-Blog2/image-3-4.png)

<p style="text-align: center;">Figure 3: Multi-Region serverless authorizer workflow with Route53 failover between primary and secondary Regions</p>

The previous figure shows architecture illustrating both failover and fallback capabilities through CloudWatch alarms and manual approval process. This approach aligns with best practices for critical applications, where automatic failover is not recommended despite being technically feasible. Teams can use this to assess technical readiness, business impact, and make informed decisions about timing and potential revenue impact.

The [demo](https://github.com/aws-samples/AWS_Serverless_Resiliency_Samples/tree/main/multi-region-authorizer) implements multi-Region serverless authorizer serving as reference architecture. Real-world implementations need careful evaluation of failover strategies based on business criticality and operational requirements.

**Testing multi-Region scenarios**

The demo application hosts frontend on [Amazon Elastic Container Service (Amazon ECS)](https://aws.amazon.com/ecs/). Route 53 health check configuration in this [GitHub](https://github.com/aws-samples/AWS_Serverless_Resiliency_Samples/blob/main/multi-region-authorizer/deployment/domain-deployments.yaml) defines key failover parameters:

1. FailureThreshold: Specifies the number of consecutive failed health checks before Route 53 marks endpoint as unhealthy.
2. RequestInterval:
   1. Standard: 30-second cycle ($0.50 per health check/month)
   2. Fast: 10-second cycle ($1.00 per health check/month)

```
Route53HealthCheck:
    Type: AWS::Route53::HealthCheck
    Properties:
      HealthCheckConfig:
        FailureThreshold: 2
        FullyQualifiedDomainName: !Ref DomainName
        Port: 443
        RequestInterval: 10
        ResourcePath: /failure
        Type: HTTPS
      HealthCheckTags:
        - Key: Environment
          Value: Production
        - Key: Name
          Value: multi-authorizer-health-check
```

Fast cycle enables faster failure detection. However, it increases health check costs through more logging operations, request processing, and backend compute resources. Temporary issues like network glitches, transient errors, or third-party latency may self-resolve within minutes. Implementing effective retry handling would introduce unnecessary complexity and potential data inconsistencies. Choose appropriate cycle based on business SLAs and cost considerations.

To test failover scenarios, the architecture uses a mock Lambda function as health check endpoint. We trigger CloudWatch alarm by simulating 500 response status code from this function, which will drive the manual failover decision process, as illustrated in the following figure.

![Figure 4](/images/3-BlogsTranslated/3.1-Blog2/image-4-3.png)

<p style="text-align: center;">Figure 4: Console screenshot showing multi-authorizer-health-check with "Unhealthy" status</p>

DNS caching occurs at multiple layers (browser, operating system, ISP, and VPN). To observe immediate failover behavior, clear DNS resolver cache at each layer.

For more comprehensive resilience testing, consider applying chaos engineering practices. You can use [chaos-lambda-extension](https://github.com/aws-cli-tools/chaos-lambda-extension) to introduce latency or modify function responses in a controlled manner. [AWS Fault Injection Service](https://aws.amazon.com/fis/) (AWS FIS), a fully managed service, enables executing fault injection experiments to improve resilience, performance and observability. Combining these tools helps validate multi-Region architecture under various controlled failure conditions.

## **Observability in multi-Region deployment**

Implementing multi-Region architecture is only the first step. Cross-Region observability requires monitoring Region A resources from Region B and vice versa. CloudWatch enables this through [cross-account and cross-Region](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Cross-Account-Cross-Region.html) monitoring, providing unified logs and metrics in a single dashboard. Implement deep operational health checks to verify critical application functionality across AWS Regions.

Although AWS serverless services are distributed, identifying exact failures requires combining multiple data points. CloudWatch [composite](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Create_Composite_Alarm.html) alarms help aggregate these signals, facilitating informed decisions. Consider implementing custom monitoring solutions to trace end-to-end requests across AWS Regions. This comprehensive view helps manage multi-Region complexity and respond quickly to potential issues.

## **Conclusion**

Building resilient multi-Region applications requires careful consideration of architectural patterns, costs, and operational complexity. AWS Serverless services, with their pay-for-value model, significantly reduce challenges when implementing multi-Region architecture. The authorizer pattern presented in this post shows how organizations can achieve high availability without bearing idle infrastructure costs like traditional approaches. Teams can follow these architectural patterns and best practices to build robust, cost-effective solutions that maintain service availability during disruptions.

To learn about resilience concepts, visit [AWS Developer Center](https://builder.aws.com/learn/topics). Full source code of the demo used in this post is available in our [GitHub repository](https://github.com/aws-samples/AWS_Serverless_Resiliency_Samples/tree/main/multi-region-authorizer). To expand serverless knowledge, visit [Serverless Land](https://serverlessland.com/).
