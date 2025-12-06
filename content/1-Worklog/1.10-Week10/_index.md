---
title: "Week 10 Worklog"
date: "2025-11-10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

- Improve and optimize OCR model for various types of invoices
- Enhance Voice processing quality with Vietnamese numbers and compound phrases
- Deploy Confidence Scoring system for both Voice and Bill
- Smart category detection and context recognition
- Comprehensive error handling and performance optimization
- Multi-dimensional testing with edge cases

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Start Date | Completion Date | Reference Material                                                                                      |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------------------------------------------------------------------------- |
| 2   | - Participate in Cloud Mastery Series #2<br><br>OCR Enhancement<br>- Detect and extract line items in proper JSON format<br>- Extract multiple items in invoice<br>- Count components in invoice<br>- Test with various bill types<br><br>Voice Model Quality Improvement<br>- Handle Vietnamese numbers (e.g., "hai mươi hai" to 22)<br>- Recognize compound phrases<br>- Fix spelling errors and handle noise<br>- Improve JSON response format<br>- Testing                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | 10/11/2025 | 10/11/2025      | [Sprint 02 - Day 06](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-6.md)  |
| 3   | Check OCR model confidence score<br>- Calculate Field-level Confidence<br>- Calculate confidence score for each extracted field:<br>- Amount/Total confidence<br>- Date confidence<br>- Text clarity<br>- Clear line separation<br>- Price alignment<br>- Quantity detection<br>- Overall confidence algorithm<br>- Calculate Low Confidence Threshold<br>- Test with over 30 bills<br><br>Check Voice Confidence Scoring<br>- Test multi-layer confidence scoring<br>- Test overall confidence algorithm<br>- Test Voice Low Confidence Thresholds<br>- Performance check (over 50 samples, <4 seconds)<br><br>Comprehensive testing of Voice and Bill systems                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 11/11/2025 | 11/11/2025      | [Sprint 02 - Day 07](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-7.md)  |
| 4   | Smart category detection and context recognition in Voice<br>- Advanced category detection such as merchant name analysis, keyword extraction based on categories<br>- Determine context<br>- Testing<br><br>Extract new invoice types<br>- Test with supermarket invoices<br>- Test with restaurant invoices<br>- Test with coffee shop and beverage store invoices<br>- Extraction rules for each specific type<br>- Improve Bill endpoint JSON response<br><br>Backend integration and testing<br>- Integrate transaction functions<br>- Error handling<br>- Return correct JSON values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | 12/11/2025 | 12/11/2025      | [Sprint 02 - Day 08](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-8.md)  |
| 5   | Error Handling, Optimization & Monitoring<br>Voice processing optimization<br>- Optimize Voice model performance<br>Error Handling & Resilience<br>- Handle Corrupted Audio:<br>- Validate audio format (WAV, MP3, M4A)<br>- Check audio duration (minimum 0.5 seconds, maximum 30 seconds)<br>- Detect corrupted/incomplete files<br>- Return clear error: "Invalid audio format or corrupted file"<br>- Handle STT Timeout:<br>- Set timeout for STT processing (maximum 30 seconds)<br>- If timeout, return partial result with warning<br>- Log timeout events for monitoring<br><br>Retry Logic:<br>- Retry STT on temporary errors (maximum 3 retries)<br>- Exponential backoff: 1 second, 2 seconds, 4 seconds<br>- Return error after maximum retries<br><br>Exception Cases:<br>- Empty/silent audio → Error: "No speech detected"<br>- Non-Vietnamese speech → Low confidence warning<br>- Multiple speakers → Warning + best effort extraction<br>- Very long audio (>30 seconds) → Error: "Audio too long"<br><br>Graceful Degradation:<br>- If category detection fails → Return "Uncategorized"<br>- If quantity extraction fails → Return null value with warning<br>- If date not detected → Use current date with warning<br>- Always return partial results when possible | 13/11/2025 | 13/11/2025      | [Sprint 02 - Day 09](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-9.md)  |
| 6   | Comprehensive testing and documentation<br>- Prepare data for testing both Voice and Bill models<br>- Test Voice API<br>- Test Bill OCR API<br><br>Voice test cases<br>- Test with background noise<br>- Test with fast or slow speech<br>- Test with invalid input, such as nonsense speech<br>- Test multiple transactions in one recording<br>- Test ambiguous input<br><br>Bill processing test cases<br>- Test images rotated in various directions<br>- Test image quality<br>- Test inputs that are not invoice images<br>- Test with highly complex invoices<br>- Test with invoices containing many items                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | 14/11/2025 | 14/11/2025      | [Sprint 02 - Day 10](https://gitlab.com/vicobi/vicobi-docs/-/blob/main/dev-plans/ai/sprint-2/day-10.md) |

### Week 10 Achievements:

#### 1. OCR Model Improvements

- Detect and extract line items in proper JSON format
- Extract multiple items in a single invoice
- Automatically calculate quantity of components in invoice
- Successfully tested with various invoice types: supermarket, restaurant, coffee shop, beverage stores
- Built extraction rules for specific invoice types
- Improved JSON response format for Bill endpoint

#### 2. Voice Processing Quality Enhancement

- Handle Vietnamese numbers (convert "hai mươi hai" → "22")
- Recognize Vietnamese compound phrases
- Fix spelling errors and handle audio noise
- Improved JSON response format
- Optimized Voice processing performance

#### 3. Confidence Scoring System

**OCR Confidence:**

- Calculate field-level confidence
- Confidence for Amount/Total
- Confidence for Date
- Evaluate text clarity and line separation
- Detect price alignment and quantity
- Build overall confidence algorithm
- Set Low Confidence Threshold
- Tested on over 30 real invoices

**Voice Confidence:**

- Deploy multi-layer confidence scoring
- Overall confidence algorithm for Voice
- Set Low Confidence Thresholds
- Performance check on over 50 samples (processing time <4 seconds)

#### 4. Smart Category Detection

- Merchant/seller name analysis
- Keyword extraction based on categories
- Transaction context determination
- Advanced Category Detection

#### 5. Error Handling & Resilience

**Audio Error Handling:**

- Validate audio format (WAV, MP3, M4A)
- Check duration (min: 0.5s, max: 30s)
- Detect corrupted/incomplete files
- Handle STT timeout (max: 30s)
- Retry logic with exponential backoff (3 times, 1s-2s-4s)

**Exception Handling:**

- Empty/silent audio → Error: "No speech detected"
- Non-Vietnamese speech → Low confidence warning
- Multiple speakers → Warning + best effort extraction
- Audio too long (>30s) → Error: "Audio too long"

**Graceful Degradation:**

- Category not detected → Return "Uncategorized"
- Quantity not extracted → Return null + warning
- Date not detected → Use current date + warning
- Always return partial results when possible

#### 6. Comprehensive Testing

**Voice Testing:**

- Test with background noise
- Test speech speed (fast/slow)
- Test invalid input (nonsense speech)
- Test multiple transactions in one recording
- Test ambiguous input

**Bill OCR Testing:**

- Test images rotated in various directions
- Test diverse image quality
- Test input not in invoice format
- Test highly complex invoices
- Test invoices with many items

#### 7. Backend Integration

- Integrate transaction functions with Backend
- Comprehensive error handling
- Return standardized JSON values

**Summary:** Week 10 focused on enhancing quality and reliability of both Voice and OCR models. Successfully deployed confidence scoring system, comprehensive error handling, and multi-dimensional testing with various edge cases. The system is ready for Backend integration and handling complex real-world scenarios.
