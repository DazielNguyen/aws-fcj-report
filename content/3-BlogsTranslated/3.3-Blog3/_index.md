---
title: "Blog 3"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# **AWS Weekly Roundup: AWS Transform, Amazon Neptune, and more (September 8, 2025)**

by Esra Kayabali | on September 8, 2025 | in [Amazon Bedrock](https://aws.amazon.com/blogs/aws/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Elastic Container Service](https://aws.amazon.com/blogs/aws/category/compute/amazon-elastic-container-service/), [Amazon Neptune](https://aws.amazon.com/blogs/aws/category/database/amazon-neptune/), [Announcements](https://aws.amazon.com/blogs/aws/category/post-types/announcements/), [AWS Transform](https://aws.amazon.com/blogs/aws/category/artificial-intelligence/generative-ai/aws-transform/), [AWS User Notifications](https://aws.amazon.com/blogs/aws/category/management-and-governance/aws-user-notifications/), [Launch](https://aws.amazon.com/blogs/aws/category/news/launch/), [News](https://aws.amazon.com/blogs/aws/category/news/) | [Permalink](https://aws.amazon.com/blogs/aws/aws-weekly-roundup-aws-transform-amazon-neptune-and-more-september-8-2025/) | Comments | Share

Summer has come to an end in Utrecht, where I live in the Netherlands. In two weeks, I will attend [AWS Community Day 2025](https://awscommunityday.nl/2025/), hosted at Kinepolis Jaarbeurs Utrecht on September 24. This one-day event will bring together over 500 cloud professionals from across the Netherlands, with 25 breakout sessions spanning 5 technical tracks. The day will kick off with virtual keynotes at 9:00 AM, followed by parallel sessions focusing on practical implementations of serverless architectures and container optimization strategies, delivering value for all experience levels.

Last year's AWS Community Day Netherlands 2024 brought together a diverse community of practitioners, speakers and AWS enthusiasts, creating a community-led conference with high knowledge-sharing value. If you plan to attend, feel free to find me to discuss **AWS** services or share your cloud deployment experiences!

![0-AWSNEWS-2266](/images/3-BlogsTranslated/3.1-Blog3/0-AWSNEWS-2266.png)

## **Last week's launches**

Let's review last week's new announcements.

[AWS Transform assessments now include detached storage](https://aws.amazon.com/about-aws/whats-new/2025/09/aws-transform-assessments-detached-storage/) – AWS Transform has expanded its assessment capabilities to analyze on-premises detached storage infrastructure, helping customers identify migration total cost of ownership (TCO). Assessments now evaluate Storage Area Network (SAN), Network Attached Storage (NAS), file servers, object storage, and virtual environments, while recommending appropriate target AWS services like Amazon S3, Amazon EBS, and Amazon FSx. The tool provides comprehensive TCO comparison between current environments and AWS, with performance and cost optimization recommendations. Since storage can represent up to 45% of total migration opportunities, this upgrade helps customers visualize migration options on AWS. AWS Transform assessment is now available in US East (N. Virginia) and Europe (Frankfurt).

[Amazon Bedrock now supports global cross-region inference for Anthropic Claude Sonnet 4](https://aws.amazon.com/about-aws/whats-new/2025/09/amazon-bedrock-global-cross-region-inference-anthropic-claude-sonnet-4/) – The Anthropic Claude Sonnet 4 model in Amazon Bedrock now supports Global cross-Region inference, allowing inference requests to be routed to any supported commercial AWS Region for processing. This upgrade optimizes available resources and increases model throughput by distributing traffic across multiple Regions. Previously, you could select cross-Region inference profiles tied to each region (US, EU, APAC). The new Global cross-Region inference profile provides additional flexibility for generative AI without geographic constraints, helping handle unplanned traffic bursts and increase throughput. Detailed implementation guidance is available in [Amazon Bedrock documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/cross-region-inference.html).

[Amazon Neptune Database now supports Public Endpoints, simplifying development access](https://aws.amazon.com/about-aws/whats-new/2025/09/aws-neptune-database-public-endpoints/) – Amazon Neptune now supports Public Endpoints, allowing direct connections to Neptune databases from outside VPC without complex network configuration. This feature enables developers to securely access graph databases from personal development machines without VPN or bastion hosts, while still ensuring security through IAM authentication, VPC security groups, and encryption in transit. You can enable Public Endpoints for Neptune clusters running engine version 1.4.6 or later through AWS Management Console, AWS CLI, or AWS SDK. This feature has no additional charges beyond standard Neptune pricing, and is available in all AWS Regions where Neptune Database is offered. Implementation details are in [Amazon Neptune documentation](https://docs.aws.amazon.com/neptune/latest/userguide/intro.html).

[ECS Exec now supported on AWS Management Console](https://aws.amazon.com/about-aws/whats-new/2025/09/ecs-exec-aws-management-console/) – Amazon ECS now supports ECS Exec directly in AWS Management Console, enabling secure, interactive shell access to running containers without opening inbound ports or managing SSH keys. Previously only available via API/CLI/SDK, this feature makes troubleshooting convenient by accessing containers directly in the console. You can enable ECS Exec when creating/updating services and standalone tasks, then connect to containers by selecting "Connect" on the task details page, opening an interactive session via CloudShell. The console also displays corresponding AWS CLI commands for use on local machines. The feature is available in all AWS commercial Regions and documented in the [ECS developer guide](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-exec.html).

[General availability of organizational notification configurations for AWS User Notifications](https://aws.amazon.com/about-aws/whats-new/2025/09/general-availability-organizational-notification-configurations-aws-user-notifications/) – AWS User Notifications now supports Organizational Notification Configurations, enabling AWS Organizations users to configure and observe notifications centrally across the organization. Management accounts or delegated administrators can configure notifications for specific organizational units or for all accounts in the organization. The service supports configuring notifications for any supported Amazon EventBridge event, such as console sign-ins without MFA, with notifications appearing in administrators' Console Notifications Center and AWS Console Mobile Application. User Notifications supports up to 5 delegated administrators and is available in all AWS Regions where the service is offered. Implementation details are in [AWS User Notifications user guide](https://docs.aws.amazon.com/notifications/latest/userguide/managing-org-notifications.html).

[For a full list of AWS announcements, follow the What's New at AWS page.](https://aws.amazon.com/new/)

## **Upcoming AWS events**

Mark your calendar and register for upcoming AWS events.

[AWS Summits](https://aws.amazon.com/events/summits/) – Free online and in-person events that bring the cloud computing community together to connect, collaborate and learn about AWS. Register in a city near you: [Zurich](https://aws.amazon.com/events/summits/zurich/) (September 11), [Los Angeles](https://aws.amazon.com/events/summits/los-angeles/) (September 17), and [Bogotá](https://aws.amazon.com/es/events/summits/bogota/) (October 9).

[AWS re:Invent 2025](https://reinvent.awsevents.com/?trk=ba8b32c9-8088-419f-9258-82e9375ad130&sc_channel=ell) – See you in Las Vegas from December 1–5, where cloud pioneers from around the world gather to get AWS innovation updates, learn from peers, expert-led in-depth discussions and expand connections. Don't forget to explore the [event catalog](https://registration.awsevents.com/flow/awsevents/reinvent2025/eventcatalog/page/eventcatalog?trk=ba8b32c9-8088-419f-9258-82e9375ad130).

[AWS Community Days](https://aws.amazon.com/events/community-day/?trk=e61dee65-4ce8-4738-84db-75305c9cd4fe&sc_channel=el&?trk=ba8b32c9-8088-419f-9258-82e9375ad130&sc_channel=el) – A series of community-led conferences featuring technical discussions, workshops, and hands-on labs led by expert AWS users and industry leaders sharing: [Baltic](https://awsbaltic.eu/) (September 10), [Aotearoa](https://aws-community-day.nz/inperson.html) (September 18), [South Africa](https://www.awscommunityday.co.za/) (September 20), [Bolivia](https://www.facebook.com/awscommunitydaybolivia/) (September 20), [Portugal](https://awscommunityday.pt/) (September 27).

Browse all [in-person and virtual events organized by AWS here.](https://aws.amazon.com/events/explore-aws-events/)

That's all for this week. See you next Monday in the Weekly Roundup!

[— Esra](https://www.linkedin.com/in/esrakayabali/)

_This post is part of the [Weekly Roundup](https://aws.amazon.com/blogs/aws/tag/week-in-review/) series. Come back every week for a quick overview of interesting news and announcements from AWS!_

TAGS: [Week in Review](https://aws.amazon.com/blogs/aws/tag/week-in-review/)

| <img src="/images/3-BlogsTranslated/3.1-Blog3/esrakayabali11-400x400-1.jpg" alt="Esra_Kayabali" width="350" style="float: left; margin-right: 15px;"/> | **Esra Kayabali** <br/> Esra Kayabali is a Senior Solutions Architect at AWS, specializing in analytics including data warehousing, data lakes, big data analytics, batch and real-time data streaming, and data integration. She has over ten years of experience in software development and solution architecture. She is passionate about learning collaboratively, sharing knowledge and leading the community on their cloud technology journey. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
