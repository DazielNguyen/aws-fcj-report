---
title: "Week 11 Worklog"
date: "2025-11-17"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

- Detect and handle multiple complex transactions
- Integrate PDF file support for Bill OCR
- Implement feedback system and model fine-tuning
- Enhance image and audio processing quality
- Integrate Backend and MongoDB storage
- Automated testing and Docker deployment
- Get acquainted with AWS and management tools

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Start Date | Completion Date | Reference Material and Learning Notes                                                                   |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ------------------------------------------------------------------------------------------------------- |
| 2   | Multiple transaction detection and PDF support<br>- Complex multi-transaction parsing<br>- Refine multi-transaction detection algorithm:<br>- Detect jar allocation in phrases<br>- Handle mixed transaction types:<br><br>Test complex phrases<br>- Test 1 transaction with 1 jar<br>- Test multiple transactions<br>- Test switching between jars<br>- Test mixed contexts<br><br>Improve PDF file support for Bill section<br>- Install libraries<br>- Test transactions with PDF files | 17/11/2025 | 17/11/2025      | [Sprint 03 - Day 11](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-11.md) |
| 3   | User feedback and learning system<br>- Handle user feedback system for Voice section<br>- Handle user feedback system for Bill section<br>- Fine-tune models based on feedback<br>- Improve syntax handling for incorrect inputs<br>Test improvements of Voice and Bill models                                                                                                                                                                                                             | 18/11/2025 | 18/11/2025      | [Sprint 03 - Day 12](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-12.md) |
| 4   | Advanced image/audio processing<br>- Detect and enhance Bill quality<br>- Detect image quality<br>- Auto-rotate and deskew images<br>- Detect ROI (Region of Interest)<br>- Integrate with OCR Pipeline<br>- Testing<br><br>Voice background noise handling<br>- Implement noise reduction<br>- Voice activity detection<br>- Silence trimming<br>- Reduce processing time<br>- Integrate with Voice Pipeline<br>- Testing                                                                 | 19/11/2025 | 19/11/2025      | [Sprint 03 - Day 13](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-13.md) |
| 5   | Backend Integration & File Storage<br>Backend service transaction integration<br>- Review Backend API<br>- Test AI and Backend flow<br>- Verify event consumption<br>- Check automatic transaction creation<br>- Troubleshoot integration<br><br>MongoDB storage integration<br>- Setup Database for Voice and Bill<br>- Prepare for Amazon S3 integration                                                                                                                                 | 20/11/2025 | 20/11/2025      | [Sprint 03 - Day 14](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-14.md) |
| 6   | Create automated tests<br>- Create tests for Voice and Bill<br>- Acceptance and verification of all tests<br>- Bug fixes<br>- Full regression testing<br><br>Setup and Deploy to Docker                                                                                                                                                                                                                                                                                                    | 21/11/2025 | 21/11/2025      | [Sprint 03 - Day 15](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-3/day-15.md) |

### Week 11 Achievements:

#### 1. Multiple Transaction Detection and PDF Support

- Complex multi-transaction parsing
- Refined multi-transaction detection algorithm
- Detected jar allocation in phrases
- Handled mixed transaction types

**Complex Phrase Testing:**

- Tested 1 transaction with 1 jar
- Tested multiple transactions
- Tested switching between jars
- Tested mixed contexts

**PDF Support:**

- Installed PDF processing libraries
- Tested transactions with PDF files
- Integrated PDF into OCR Pipeline

#### 2. Feedback and Learning System

- Handled user feedback system for Voice section
- Handled user feedback system for Bill section
- Fine-tuned models based on feedback
- Improved handling of incorrect input syntax
- Tested improvements of Voice and Bill models

#### 3. Advanced Image/Audio Processing

**Bill Quality Enhancement:**

- Detected and assessed image quality
- Auto-rotated and deskewed images
- Detected ROI (Region of Interest)
- Integrated with OCR Pipeline
- Tested with various image conditions

**Voice Background Noise Handling:**

- Implemented noise reduction
- Voice Activity Detection
- Silence trimming
- Reduced processing time
- Integrated with Voice Pipeline
- Tested with various audio environments

#### 4. Backend & Storage Integration

**Backend Integration:**

- Reviewed Backend API endpoints
- Tested AI and Backend workflow
- Verified event consumption
- Checked automatic transaction creation
- Troubleshot integration issues

**MongoDB Integration:**

- Setup Database for Voice and Bill
- Prepared schema for Amazon S3 integration
- Implemented storage strategy

#### 5. Automated Testing and Deployment

- Created automated tests for Voice and Bill
- Acceptance and verification of all test cases
- Fixed bugs discovered from testing
- Performed full regression testing
- Setup Docker environment
- Deployed to Docker container

#### 6. AWS Learning

- Understood AWS and basic service groups (Compute, Storage, Networking, Database)
- Created and configured AWS Free Tier account
- Became familiar with AWS Management Console
- Installed and configured AWS CLI (Access Key, Secret Key, Region)
- Performed basic operations with AWS CLI
- Connected and became familiar with First Cloud Journey community

**Summary:** Week 11 completed the enhancement of multi-transaction processing capabilities, integrated PDF support, implemented feedback system and model fine-tuning. Significantly improved image/audio processing quality with advanced techniques (ROI detection, noise reduction, VAD), successfully integrated with Backend and MongoDB, while completing automated testing and Docker deployment. Additionally, became familiar with AWS ecosystem and basic management tools, preparing for cloud infrastructure deployment.
