---
title: "Week 9 Worklog"
date: "2025-11-03"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

- FastAPI project with MongoDB
- Vietnamese STT library selected and integrated
- Vietnamese OCR library selected and tested
- NLP extraction: amount, category, date, jar detection (REQ-027)
- Detect multiple transactions (REQ-027)
- Publish events to RabbitMQ

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Start Date | Completion Date | Reference Material and Learning Notes                                                                  |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------------------------------------------------------------------------ |
| 2   | Project Setup<br>- Create FastAPI project structure (/app, /models, /services, /utils, /routers, /schemas, /ai-models)<br>- Setup virtual environment (Python 3.11+)<br>- Install FastAPI, Uvicorn, Pydantic<br>- Install local MongoDB (Docker)<br>- Create database: ai_service_db (configured in docker-compose.yml)<br>- Collections: Bills, Voices (using MongoEngine models)<br>- Setup MongoDB connection with MongoEngine<br>- Test connection (lifecycle management in database.py)<br>Technology Research<br>- For Bill: Try various OCR models that best solve Vietnamese extraction<br>- For Voice: Search for Speech-to-Text models in Vietnamese language                                                                   | 03/11/2025 | 03/11/2025      | [Sprint 01 - Day 01](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-1.md) |
| 3   | Core API Structure and Endpoints<br>- Shared API infrastructure<br>- Setup Voice and Bill APIs<br>- Create basic API endpoint structure<br>- Setup Pydantic models for request/response<br>- Add CORS middleware<br>- Add error handling middleware<br>- Create health check endpoint (GET /health)<br>- Setup logging (structlog)                                                                                                                                                                                                                                                                                                                                                                                                        | 04/11/2025 | 04/11/2025      | [Sprint 01 - Day 02](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-2.md) |
| 4   | Voice Processing Pipeline<br>- Install Vietnamese STT Library<br>- Audio preprocessing<br>- Voice-to-Text integration<br>- Implement STT functionality<br>- Test Voice Model<br><br>OCR Preparation for Bill Extraction<br>- Install OCR library selected from Day 1<br>- Research image preprocessing techniques<br>- Create sample preprocessing pipeline<br>- Test with bill images                                                                                                                                                                                                                                                                                                                                                    | 05/11/2025 | 05/11/2025      | [Sprint 01 - Day 03](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-3.md) |
| 5   | Text Processing for Vietnamese Language<br>- Test model accuracy and select appropriate model, team uses PhoWhisper from VinAI<br>- Check model detection, whether it receives voice and returns text<br>- Adjust endpoint to return correct categories defined by team<br>- Test processing multiple transactions simultaneously, check if model can handle<br>- Setup detection of transaction time from speech<br>- Create transaction object<br><br>OCR Preprocessing<br>- Process images when user inputs and process that bill. Enhance image to best quality before feeding to OCR model<br>- Collect Vietnamese bills (electricity bills, shopping mall bills, restaurant bills, convenience store bills, coffee shop bills, ...) | 06/11/2025 | 06/11/2025      | [Sprint 01 - Day 04](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-4.md) |
| 6   | Integration and Testing<br>- Handle background tasks for Voice and Bill<br>- Setup event publishing<br>Speech to Text<br>- End-to-end testing of Voice<br>- Pipelines running as Recording -> Processing -> Return Endpoint, check and improve Voice processing accuracy<br>Bill Detection<br>- Deploy and test OCR models: Tesseract, EasyOCR,...                                                                                                                                                                                                                                                                                                                                                                                        | 07/11/2025 | 07/11/2025      | [Sprint 01 - Day 05](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-1/day-5.md) |

### Week 9 Achievements:

#### 1. Project Setup and Infrastructure

- Completed FastAPI project structure with standard directories (/app, /models, /services, /utils, /routers, /schemas, /ai-models)
- Setup Python 3.11+ environment with virtual environment
- Installed and configured local MongoDB using Docker
- Created `ai_service_db` database and collections for Bills and Voices
- Setup MongoDB connection with MongoEngine and lifecycle management

#### 2. API Structure and Middleware

- Setup API endpoints for Voice and Bill processing
- Created Pydantic models for request/response validation
- Configured CORS middleware and error handling middleware
- Implemented health check endpoint (GET /health)
- Integrated structlog for logging system

#### 3. Voice Processing (Speech-to-Text)

- Researched and selected **PhoWhisper from VinAI** for Vietnamese STT
- Implemented audio preprocessing and Voice-to-Text integration
- Tested model accuracy and voice detection capability
- Configured endpoint to return correct defined categories
- Tested processing multiple transactions simultaneously
- Setup time detection for transactions from speech
- Created transaction objects from voice data

#### 4. Bill Processing (OCR)

- Researched and selected appropriate OCR libraries (Tesseract, EasyOCR)
- Implemented image preprocessing to optimize quality before OCR
- Collected diverse Vietnamese bill dataset (electricity, supermarket, restaurants, convenience stores, coffee shops)
- Tested OCR models with real bill images

#### 5. NLP Extraction and Data Processing

- Implemented information extraction: amount, category, date (REQ-027)
- Jar detection
- Multiple transaction detection in a single request

#### 6. RabbitMQ Integration

- Setup event publishing to RabbitMQ
- Handled background tasks for Voice and Bill processing

#### 7. Testing and Quality Assurance

- End-to-end testing for Voice processing pipeline (Recording → Processing → Return Endpoint)
- Evaluated and improved Voice processing accuracy
- Tested OCR models with real dataset

**Summary:** Week 9 successfully completed all objectives, including FastAPI-MongoDB infrastructure setup, PhoWhisper model integration for Vietnamese STT, OCR implementation for bill processing, and event publishing system with RabbitMQ. NLP functions for transaction information extraction were implemented and successfully tested.
