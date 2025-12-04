---
title: "Event 3"
date: "2025-10-16"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Summary Report: WORKSHOP "DATA SCIENCE ON AWS PLATFORM"

### Event Objectives

- Introduce an overview of the ecosystem of artificial intelligence (AI) services available on AWS.
- Guide practical processes for building and training AI models using Amazon SageMaker.
- Demonstrate how to deploy AI models from laboratory to production and integrate them into applications through APIs.

### Speaker List

- **Mr. Van Hoang Kha** - Cloud Solutions Architect, Leader of AWS User Group (Sharing solution architecture perspective).
- **Mr. Bach Doan Vuong** - Cloud DevOps Engineer, AWS Community Builder (Sharing operations and deployment perspective).

### In-Depth Content

#### **The Importance of Cloud Computing in Data Science**

- Analysis of the core role of **Cloud Computing**: Not just storage, Cloud provides unlimited computing power to process Big Data and train complex AI models that personal computers struggle to handle.
- Efficiency comparison between **Cloud and On-premise (Physical servers)**:

  - **Cloud:** Strengths lie in Elasticity — can scale resources up/down instantly, extremely fast deployment, convert CAPEX (Capital Expenditure) to OPEX (Operating Expenditure), and easily integrate new technologies.
  - **On-premise:** Faces major barriers in initial hardware costs, difficulty expanding infrastructure when data surges, and expensive maintenance personnel.

- **AWS** plays the role of backbone for the entire **Data Science pipeline**: Provides a closed-loop process from raw data collection, cleaning, training to when the model is put into practical use.

#### **AI Architecture Layers on AWS**

AWS categorizes AI services into **3 separate layers**, designed to suit different user audiences with varying technical levels and control needs:

**1. AI Services (Fully Managed Service Layer)**

> _"Instant noodle" solution for Developers who want to integrate intelligence into applications without deep ML algorithm knowledge._

- These are pre-trained models by AWS with billions of data points.
- Users only need to send data via API and receive analysis results.
- **Notable services:**

  - **Amazon Comprehend:** Understand and analyze text meaning, user sentiment (NLP).
  - **Amazon Translate:** Remove language barriers with automatic translation capabilities.
  - **Amazon Textract:** "Read" documents, extract text and tables from scanned files/images.
  - **Amazon Rekognition:** Computer vision, recognize objects, faces in images/videos.
  - **Amazon Polly:** Natural artificial voice reading (Text-to-Speech).
  - **Amazon Bedrock:** Gateway to today's leading Large Language Models (LLMs).

**Benefits:** Extremely fast time-to-market, no effort building models from scratch.

**2. ML Services (Semi-Managed Layer)**

> _Powerful tool for Data Scientists & ML Engineers needing professional environments to build their own models._

- **Amazon SageMaker** is the heart of this layer, providing a unified platform to manage ML model lifecycle (ML Ops).
- Key modules:

  - **Data Wrangler:** Minimize time for data preparation and cleaning (typically 80% of project time).
  - **Feature Store:** Repository for storing data features for reuse, avoiding waste of computing resources.
  - **AutoML (SageMaker Autopilot):** Automatically test multiple algorithms to find the best model without manual intervention.
  - **Model Registry & Monitoring:** Manage model versions and monitor model accuracy in real-time (avoid model drift phenomenon).

**Benefits:** Perfect balance between convenience and deep customization capability in training processes.

**3. AI Infrastructure (Self-Managed Infrastructure Layer)**

> _For researchers needing deep hardware intervention and lowest-level optimization._

- Provides "building blocks" to build custom AI systems:

  - **Amazon EC2 P5/G6/Inferentia:** Virtual machines with dedicated chips (GPU/ASIC) for extremely high computing performance.
  - **Amazon EKS / ECS:** Container management for large-scale ML applications.
  - **AWS Lambda:** Run inference code serverless, cost-effective for small tasks.
  - **Amazon S3 / EFS:** Massive "Data Lake" storage system.

**Benefits:** Not limited by templates, thoroughly optimize costs for super-large systems, but requires high DevOps skills.

#### Popular AI Services Supporting Students & Researchers

**1. Amazon SageMaker**

- An IDE (Integrated Development Environment) dedicated to ML on cloud:

  - Integrates everything from raw data processing to hyperparameter tuning.
  - Provides CI/CD capability for Machine Learning, automating train and deploy processes.
  - Supports Notebooks (Jupyter) familiar to students.

**2. Amazon Comprehend**

- Brings "reading comprehension" capability to applications:

  - **Sentiment analysis:** Know if customers are happy, angry, or satisfied through emails/comments.
  - **Entity recognition:** Automatically detect names of people, places, organizations in text.
  - **Security:** Automatically find and mask personal information (PII) in data.

**3. Amazon Translate**

- High-quality translation based on Deep Learning (Neural Network).
- Ability to customize specialized vocabulary (e.g., correctly translate medical or technical terms).
- Helps expand application user base globally.

**4. Amazon Textract**

- Far surpasses traditional OCR technology thanks to document structure understanding.
- Preserves table and form formatting when extracting, helps digitize administrative documents quickly and accurately.

#### Standard Data Science Process on AWS

1. **Ingest & Store:** Collect data from multiple sources into Amazon S3 "warehouse".
2. **Prepare:** Clean and standardize data using AWS Glue or Lambda.
3. **Train & Tune:** Use SageMaker to train and optimize algorithms.
4. **Deploy:** Package model into API Endpoint or integrate into application.
5. **Monitor:** Use CloudWatch to monitor system health and model prediction quality.

#### **Demo 1: Optimizing Workflow with Low-Code/No-Code**

- **Objective:** Prove that technical barriers in AI are gradually being removed thanks to visual tools.
- **Tool:** Amazon SageMaker Canvas (Drag-and-drop interface).
- **Implementation process:**

  1. Upload raw dataset to S3.
  2. Use graphical interface to define processing flow: Input -> Handle missing data -> Select target column -> Train.
  3. System automatically runs experiments and returns evaluation metrics (Accuracy, F1-score...) in easy-to-understand charts.

- **Significance:** Helps students and Business Analysts create value from data immediately without writing thousands of lines of Python code.

#### **Demo 2: From Model to Real Application (Deployment)**

- **Objective:** Illustrate the "bridge" connecting mathematical models and end users.
- **Tools:** SageMaker Endpoint combined with API Gateway and Lambda.
- **Implementation process:**

  1. Convert trained model into an HTTP Endpoint (network address).
  2. Set up API Gateway to receive external requests (e.g., from mobile app).
  3. Process intermediate logic using AWS Lambda (serverless) to call model and return results to users.

- **Significance:** Shows the full picture of making AI products: Model is just one part, integration and serving the model creates complete products.

#### Comparison Table: Cloud vs. On-premise (Performance & Economics Perspective)

| Criteria               | Cloud (AWS)                                                      | On-premise (Private servers)                                                                |
| :--------------------- | :--------------------------------------------------------------- | :------------------------------------------------------------------------------------------ |
| **Scalability**        | **Unlimited & Instant:** Auto-scale according to actual traffic. | **Rigid:** Limited by current hardware quantity.                                            |
| **Cost Model**         | **OPEX (Operating Expenditure):** Pay as you go, no waste.       | **CAPEX (Capital Expenditure):** Must invest large sum buying equipment, depreciation risk. |
| **Deployment Speed**   | **Minutes:** Just a few clicks to have servers.                  | **Weeks/Months:** Must order, install, setup OS.                                            |
| **System Maintenance** | **AWS handles:** Focus entirely on application development.      | **DIY:** Spend IT personnel on electricity, cooling, hardware operations.                   |
| **Student-friendly**   | **High:** Utilize Free Tier for free learning.                   | **Low:** Requires expensive high-spec machines.                                             |

#### General Conclusion

- AWS provides a **comprehensive and seamless ecosystem**, blurring the gap between academic learning and practical applications. Whether beginners or large enterprises, AWS has appropriate tool sets (Layers) to solve data problems.

### Personal Reflections After the Event

The **"AI Services on AWS for Data Science"** workshop not only provided theoretical knowledge but also opened up new thinking about technology approaches, helping me better define the path from **data research** to **product development**.

#### Expanded thinking thanks to experts

- Clearly understand why the world is shifting to Cloud: It's liberation from infrastructure burden to focus on core value which is data.
- Grasped the overall picture of **3 AI layers**, thereby knowing how to choose appropriate services for each stage of personal projects.

#### Visualizing knowledge through Demos

- **Demo 1 (Canvas):** Impressed with AI "democratization" capability. Training models now is as visual as assembling lego, helping validate ideas extremely fast.
- **Demo 2 (Deployment):** This is the piece I often miss. Understanding how to create an API for others to use my model is a turning point from "doing homework" to "making products".

#### Accessing advanced technology

- Services like **Comprehend** or **Textract** show the power of Pre-trained models. They help solve difficult problems (like reading invoices, sentiment analysis) in an instant without building complex models yourself.

#### Connection value

- Opportunity to discuss Cost optimization issues is very practical, helping students like me know how to use Cloud without "burning money".
- Networking with industry professionals gives me more motivation and clearer career direction.

#### Core lessons

- **Cloud First:** Thinking of putting everything on cloud is an inevitable trend in modern Data Science.
- **Practicality:** An AI model only has value when deployed and solving problems for end users.
- **AWS Ecosystem:** A massive tool repository that I need to continue exploring to enhance my capabilities.

#### Some images captured at the event

<img src="/images/4-EventParticipated/4.3-Event3/Event_03_IMG_7059.jpeg" alt="Event_02" width="2000"/>

> **Image of knowledge transfer from 2 AWS representatives**

<img src="/images/4-EventParticipated/4.3-Event3/Event_03.JPG" alt="Event_02" width="2000"/>

> **Image of FPTers team check-in after the event**

> This is the check-in moment of all interns at AWS after the workshop ended.
