# Product Requirements Document: AI-Powered Essay Verification System

**Document Version:** 1.0  
**Last Updated:** November 22, 2025  
**Product Owner:** [To Be Assigned]  
**Target Release:** V0 Prototype

---

## Executive Summary

### Elevator Pitch
A smart assistant that helps university professors verify student learning by automatically conducting oral interviews about submitted essays, scoring responses, and generating actionable feedback.

### Problem Statement
University professors struggle to distinguish whether students genuinely understand the content in their submitted essays or have relied heavily on AI writing tools without developing true comprehension. Traditional essay grading cannot effectively assess a student's actual knowledge and understanding of the material they've submitted.

### Target Audience

**Primary Users:**
- **Professors/Instructors** at university level across all academic disciplines
- **Teaching Assistants** who grade assignments
- **Course Coordinators** managing assessment integrity

**Secondary Users:**
- **Students** submitting essays and completing verification interviews
- **Academic Administration** monitoring course quality and academic integrity

**User Demographics:**
- University-level educators (varied technical proficiency)
- Students across all majors (STEM, Humanities, Social Sciences, Arts)
- Institutions seeking scalable academic integrity solutions

### Unique Selling Proposition
Unlike plagiarism detection tools that only identify copied content, this system actively tests student comprehension through adaptive oral questioning, providing professors with both quantitative scores (0-100) and qualitative insights into student understanding before final grading decisions.

### Success Metrics

**Primary Metrics:**
- **Professor Adoption Rate:** 60% of pilot professors use system for at least 3 assignments
- **Student Completion Rate:** 85% of students complete the verification interview within 48 hours
- **Professor Satisfaction Score:** 4.0+ out of 5.0 rating on usefulness
- **Time Savings:** 30% reduction in professor time spent on integrity-related concerns

**Secondary Metrics:**
- Average system score accuracy (compared to professor final judgment)
- Question completion rate per student
- System uptime and response time
- Feedback edit rate (% of AI feedback edited by professors)

---

## Problem Analysis

### Core Problem
Professors cannot efficiently and scalably verify that students genuinely understand the content in their submitted written work, especially in an era where AI writing assistants are widely available.

### User Pain Points

**Professor Pain Points:**
1. Time-consuming to conduct individual viva examinations for all students
2. Difficulty identifying AI-assisted writing that lacks genuine understanding
3. Lack of objective tools to assess comprehension beyond written work
4. Inconsistent assessment standards across large class sizes
5. Limited scalability for comprehensive knowledge verification

**Student Pain Points:**
1. Concern about being falsely accused of academic dishonesty
2. Limited opportunity to demonstrate understanding beyond written submissions
3. Anxiety about subjective grading criteria

### Why This Solution?

**Alternatives Considered:**
- **Plagiarism Detection Tools:** Only catch copied content, not AI-assisted writing or lack of understanding
- **Manual Viva Exams:** Time-intensive, doesn't scale, inconsistent across students
- **Proctored Exams:** Requires infrastructure, doesn't assess essay-specific knowledge
- **AI Detection Tools:** High false positive rates, doesn't actually test comprehension

**Our Approach:**
Combines automated question generation, voice-based assessment, and AI evaluation to create a scalable, consistent, and comprehensive knowledge verification system that augments (not replaces) professor judgment.

---

## User Personas

### Persona 1: Dr. Sarah Chen - The Overwhelmed Professor

**Demographics:**
- Age: 42
- Position: Associate Professor, Computer Science
- Institution: Mid-size state university
- Class Size: 150 students per semester

**Goals:**
- Ensure students understand programming concepts, not just submit AI-generated code
- Reduce time spent investigating potential academic dishonesty
- Provide constructive feedback efficiently

**Pain Points:**
- Grading 150 essays takes weeks
- Can't conduct individual interviews with all students
- Uncertain which submissions reflect genuine understanding

**Technical Proficiency:** Moderate (comfortable with LMS, basic tools)

**Quote:** *"I need a way to verify understanding that doesn't add hours to my already overloaded schedule."*

---

### Persona 2: Marcus Johnson - The Diligent Student

**Demographics:**
- Age: 20
- Year: Junior, Biology major
- Learning Style: Visual and auditory learner
- GPA: 3.6

**Goals:**
- Demonstrate genuine understanding of coursework
- Receive constructive feedback to improve
- Clear his name if accused of using AI inappropriately

**Pain Points:**
- Worried about being falsely accused of AI usage
- Limited opportunities to show understanding beyond writing
- Wants more interactive assessment methods

**Technical Proficiency:** High (digital native, comfortable with video/audio tools)

**Quote:** *"I actually studied hard for this essay. I want a chance to prove I understand the material."*

---

### Persona 3: Dr. Patricia Rodriguez - The Academic Integrity Coordinator

**Demographics:**
- Age: 55
- Position: Dean of Academic Affairs
- Scope: Oversees 5,000 students across 12 departments

**Goals:**
- Implement scalable solutions for academic integrity
- Reduce administrative burden of integrity investigations
- Support faculty with effective assessment tools

**Pain Points:**
- Rising cases of AI-assisted assignments
- Faculty lack tools for efficient verification
- Need data-driven insights on assessment effectiveness

**Technical Proficiency:** Moderate-Low (relies on support staff for implementation)

**Quote:** *"We need institutional solutions that scale while maintaining educational quality."*

---

## Feature Specifications

### Feature 1: Student Essay Submission Portal

**User Story:**  
As a student, I want to submit my essay through a simple interface, so that I can begin the verification process without technical difficulties.

**Acceptance Criteria:**
- Given a student is logged in, when they navigate to the submission page, then they see an upload interface accepting .txt, .docx, .pdf files up to 10MB
- Given a student uploads a valid file, when the upload completes, then they receive confirmation with estimated wait time for questions (2-3 minutes)
- Given a student uploads an invalid file format, when the system detects this, then an error message displays supported formats
- Given a file exceeds size limit, when upload is attempted, then a clear error message explains the 10MB limit
- Edge case: If upload fails mid-transfer, system allows retry without losing previous data
- Edge case: If essay is too short (<500 words), system notifies student that minimum length requirement not met

**Priority:** P0 (Must-have for V0)

**Dependencies:**
- Authentication system integration
- File storage service (Supabase)
- Document parsing library

**Technical Constraints:**
- Must handle multiple file formats (.txt, .docx, .pdf)
- Need to extract plain text from formatted documents
- Maximum file size: 10MB

**UX Considerations:**
- Clear progress indicators during upload
- Drag-and-drop functionality
- Mobile-responsive design
- Accessible file selection for screen readers

---

### Feature 2: AI Question Generation Engine

**User Story:**  
As a professor, I want the system to automatically generate relevant questions about each student's essay, so that I don't have to manually create questions for every submission.

**Acceptance Criteria:**
- Given an essay is submitted, when text extraction completes, then system generates 3-5 questions within 2 minutes
- Given questions are generated, when displayed to student, then each question is clear, grammatically correct, and relevant to essay content
- Given the essay contains technical terms, when generating questions, then system includes at least one question asking student to explain those terms
- Given essay has a clear argument/conclusion, when generating questions, then system includes at least one question about reasoning or methodology
- Edge case: If essay is too short (<500 words), generate minimum 3 questions
- Edge case: If essay is very long (>3000 words), cap at 5 questions focusing on main themes

**Priority:** P0 (Must-have for V0)

**V0 Implementation:** Template-based question bank (10 templates) + essay keyword extraction

**V1 Enhancement:** Dynamic question generation using RAG on essay content

**Dependencies:**
- LLM API access (for keyword extraction)
- Template question bank (10 questions)
- Text analysis library

**Technical Constraints:**
- Response time <2 minutes for question generation
- Must handle essays from 500-5000 words
- Questions must be universally applicable across disciplines

**UX Considerations:**
- Show loading state to student while questions generate
- Allow professor to view generated questions before student sees them (V1 feature)

---

### Feature 3: Voice Recording Interface

**User Story:**  
As a student, I want to record my verbal answers to questions one at a time, so that I can demonstrate my understanding without technical difficulties.

**Acceptance Criteria:**
- Given questions are generated, when student navigates to interview page, then they see Question 1 of 5 with clear recording instructions
- Given student clicks "Start Recording," when recording begins, then a 60-second countdown timer displays prominently
- Given the 60-second timer expires, when time runs out, then recording automatically stops and saves
- Given student finishes answering early, when they click "Stop & Submit," then recording stops and advances to next question
- Given student wants to review, when on question screen, then they can replay their answer before submitting
- Given all questions are answered, when student completes final question, then they see confirmation and estimated scoring time
- Edge case: If microphone access denied, show clear error with instructions to enable permissions
- Edge case: If recording quality is too low (inaudible), flag for manual review
- Edge case: If browser tab closes mid-recording, save progress and allow resume

**Priority:** P0 (Must-have for V0)

**Dependencies:**
- Browser Web Audio API
- Audio storage service (Supabase)
- Microphone permission handling

**Technical Constraints:**
- Must work on Chrome, Firefox, Safari (latest 2 versions)
- Maximum recording length: 60 seconds per question
- Audio format: WebM or WAV
- Minimum supported browsers must have Web Audio API

**UX Considerations:**
- Large, clear "Record" button
- Visual waveform indicator showing recording is active
- Countdown timer prominently displayed
- "Redo" option for each question (allow 1 redo per question)
- Progress indicator (Question 2 of 5)
- Clear instructions: "Take a moment to think, then press Record"

---

### Feature 4: Speech-to-Text Transcription Service

**User Story:**  
As the system, I need to convert student voice recordings to text accurately, so that the AI evaluation engine can analyze responses.

**Acceptance Criteria:**
- Given a voice recording is submitted, when transcription begins, then text output is generated within 30 seconds
- Given transcription completes, when stored, then it maintains speaker intent and technical vocabulary accuracy >90%
- Given audio quality is poor, when transcription confidence is low, then flag recording for manual professor review
- Given student has accent or speech pattern, when transcribing, then system handles diverse speech patterns
- Edge case: If transcription service fails, retry up to 3 times before flagging for manual review
- Edge case: If recording is complete silence, flag as "no response" rather than attempt transcription

**Priority:** P0 (Must-have for V0)

**Dependencies:**
- Speech-to-text API (OpenAI Whisper, Google Speech-to-Text, or similar)
- Audio file storage
- Error handling and retry logic

**Technical Constraints:**
- Must support audio files up to 60 seconds
- Must handle educational/technical vocabulary
- Transcription accuracy target: >90% for clear audio
- API rate limits and costs

**UX Considerations:**
- N/A (backend service, no direct user interaction)
- System must store both audio and transcript for professor review

---

### Feature 5: AI Evaluation & Scoring Engine

**User Story:**  
As a professor, I want the system to evaluate student responses against their essay and generate a meaningful score, so that I can quickly identify which students need closer review.

**Acceptance Criteria:**
- Given all transcriptions are complete, when evaluation runs, then system generates a score between 0-100 within 2 minutes
- Given a student demonstrates clear understanding, when evaluated, then score reflects accuracy, depth, and consistency (score >80)
- Given a student's answers contradict the essay, when evaluated, then score reflects discrepancy (score <50)
- Given a student uses technical terms correctly, when evaluated, then score includes bonus for terminology mastery
- Given scoring completes, when displayed to professor, then it shows: overall score, per-question breakdown, and rationale
- Edge case: If transcription quality is flagged as poor, reduce confidence score and note in rationale
- Edge case: If student provides no answer (silence), assign 0 for that question

**Priority:** P0 (Must-have for V0)

**Scoring Factors (Weighted):**
1. **Accuracy (40%):** Does answer align with essay content?
2. **Depth of Understanding (30%):** Can student explain concepts beyond surface level?
3. **Consistency (20%):** Do answers align with each other and the essay?
4. **Technical Mastery (10%):** Correct use of discipline-specific terminology

**Dependencies:**
- LLM API for evaluation (GPT-4 or Claude)
- Essay text storage
- Transcription storage
- Scoring algorithm/prompt engineering

**Technical Constraints:**
- Evaluation must complete within 2 minutes for 5 questions
- Must work across all academic disciplines
- Scoring must be reproducible (same input → same score)

**UX Considerations:**
- Score displayed with color coding (0-50 red, 51-75 yellow, 76-100 green)
- Per-question breakdown visible to professor
- Clear rationale explaining score

---

### Feature 6: AI-Generated Feedback Paragraph

**User Story:**  
As a professor, I want the AI to generate a feedback paragraph about the student's performance, so that I can quickly edit and send constructive feedback without writing from scratch.

**Acceptance Criteria:**
- Given scoring completes, when feedback is generated, then it includes: overall assessment, specific strengths, areas for improvement, and next steps
- Given a high score (>80), when feedback generates, then it emphasizes strengths while suggesting minor improvements
- Given a low score (<50), when feedback generates, then it identifies specific knowledge gaps and suggests resources/strategies
- Given feedback is displayed, when professor views it, then they can edit in a rich text editor before sending
- Given professor edits feedback, when they save changes, then edited version is stored and sent to student
- Edge case: If AI feedback is generic or unhelpful, professor can completely rewrite
- Edge case: Feedback must be 150-300 words (not too brief, not overwhelming)

**Priority:** P0 (Must-have for V0)

**Feedback Structure:**
1. Opening statement (overall performance)
2. Specific strengths (2-3 points)
3. Areas for improvement (2-3 points with examples)
4. Actionable next steps
5. Encouraging closing

**Dependencies:**
- LLM API for feedback generation
- Rich text editor component
- Feedback storage
- Student notification system

**Technical Constraints:**
- Feedback generation <30 seconds
- Must be editable and saveable
- Support basic formatting (bold, italics, lists)

**UX Considerations:**
- Side-by-side view: original essay, scores, and feedback editor
- Clear "Edit Feedback" button
- Autosave while editing
- Preview before sending to student
- Template option for common feedback patterns

---

### Feature 7: Professor Dashboard

**User Story:**  
As a professor, I want to view all student submissions, scores, and feedback in one place, so that I can efficiently review and make final grading decisions.

**Acceptance Criteria:**
- Given professor logs in, when they access dashboard, then they see a list of all student submissions with status (pending questions, interview complete, scored, feedback sent)
- Given professor selects a student, when they click to view details, then they see: original essay, all questions asked, transcripts, audio playback, score breakdown, and AI feedback
- Given professor reviews a submission, when they make final judgment, then they can adjust score and/or feedback before finalizing
- Given professor wants to compare students, when viewing dashboard, then they can sort by score, submission date, or student name
- Given professor needs to export data, when they click export, then they receive a CSV with all scores and timestamps
- Edge case: If student hasn't completed interview, show "pending" status with time elapsed since essay submission
- Edge case: Professor can manually trigger re-scoring if needed

**Priority:** P0 (Must-have for V0)

**Dashboard Views:**
1. **Overview:** List of all submissions with key metrics
2. **Detail View:** Individual student submission with all data
3. **Comparison View:** Side-by-side comparison of multiple students (V1)

**Dependencies:**
- Authentication and authorization
- Data retrieval from database
- Audio playback component
- Export functionality

**Technical Constraints:**
- Must load within 3 seconds for classes up to 200 students
- Support pagination for large classes
- Audio playback must work in-browser

**UX Considerations:**
- Search and filter functionality
- Clear visual hierarchy
- Mobile-responsive for on-the-go reviews
- Keyboard shortcuts for power users
- Bulk actions (send feedback to multiple students)

---

### Feature 8: Student Feedback Delivery

**User Story:**  
As a student, I want to receive my score and professor's feedback after completing the interview, so that I understand how I performed and how to improve.

**Acceptance Criteria:**
- Given professor finalizes feedback, when they click "Send," then student receives notification (email + in-app)
- Given student logs in, when they navigate to results, then they see: overall score, feedback paragraph, and next steps
- Given student wants context, when viewing feedback, then they can see which questions they answered and their transcripts
- Given student disagrees with evaluation, when they need to appeal, then clear instructions for academic appeals process are provided
- Edge case: Student cannot see scores/feedback until professor explicitly releases them
- Edge case: If student never completed interview, they see "incomplete" status with option to restart

**Priority:** P1 (Important for V0, but can be manual initially)

**Dependencies:**
- Email notification service
- Student-facing portal
- Professor approval workflow

**Technical Constraints:**
- Real-time notification delivery
- Secure access to student's own data only

**UX Considerations:**
- Clear, encouraging tone in feedback display
- Visual score representation (progress bar)
- Downloadable feedback PDF for student records
- Hide audio recordings from students (privacy consideration)

---

## Template Question Bank (V0)

These 10 template questions form the foundation of the V0 question generation system. The system will select 3-5 questions that best match the essay's content and structure.

### Question Categories & Templates

**Category 1: Conceptual Understanding (Deep Comprehension)**

1. **Concept Explanation**  
   *"In your essay, you discussed [KEY CONCEPT/TERM from essay]. Can you explain this concept in your own words, as if teaching it to someone unfamiliar with the topic?"*
   
   **Purpose:** Tests ability to articulate core ideas without relying on memorized phrases
   
   **Evaluation Focus:** Clarity, accuracy, simplification without losing meaning

---

2. **Technical Terminology**  
   *"You used the term '[TECHNICAL TERM from essay]' in your work. What does this term mean in the context of your topic, and why is it significant?"*
   
   **Purpose:** Verifies understanding of discipline-specific vocabulary
   
   **Evaluation Focus:** Definition accuracy, contextual application, relevance

---

**Category 2: Process & Methodology (How You Got Here)**

3. **Argument Development**  
   *"Walk me through how you arrived at your main argument or thesis. What was your thinking process from initial idea to final conclusion?"*
   
   **Purpose:** Assesses whether student actually developed the argument themselves
   
   **Evaluation Focus:** Logical progression, awareness of decision points, genuine ownership

---

4. **Challenging Sections**  
   *"What was the most challenging part of writing this essay, and how did you work through that challenge?"*
   
   **Purpose:** Reveals authentic engagement with the material
   
   **Evaluation Focus:** Specific examples, problem-solving approach, intellectual honesty

---

5. **Research & Source Integration**  
   *"You referenced [SPECIFIC SOURCE/DATA] in your essay. How did you find this source, and why did you choose to include it?"*
   
   **Purpose:** Verifies genuine research process and source evaluation
   
   **Evaluation Focus:** Research methodology, source credibility assessment, integration strategy

---

**Category 3: Critical Thinking (Beyond the Essay)**

6. **Counterfactual Exploration**  
   *"If you were to write this essay again, what would you approach differently? What would you change and why?"*
   
   **Purpose:** Tests reflective thinking and understanding of weaknesses
   
   **Evaluation Focus:** Self-awareness, critical analysis, depth of reflection

---

7. **Alternative Perspectives**  
   *"What is the strongest counterargument to your main thesis, and how would you respond to it?"*
   
   **Purpose:** Assesses ability to consider opposing viewpoints
   
   **Evaluation Focus:** Awareness of limitations, intellectual humility, critical engagement

---

**Category 4: Knowledge Application (Transfer Learning)**

8. **Real-World Application**  
   *"Can you give me a real-world example or scenario where the concepts you discussed in your essay would be relevant or applicable?"*
   
   **Purpose:** Tests ability to connect theory to practice
   
   **Evaluation Focus:** Practical understanding, creativity, relevance of examples

---

9. **Scenario Adaptation**  
   *"Imagine [HYPOTHETICAL SCENARIO related to essay topic]. How would the ideas in your essay apply to this situation?"*
   
   **Purpose:** Evaluates flexible application of knowledge
   
   **Evaluation Focus:** Adaptability, problem-solving, conceptual transfer

---

**Category 5: Meta-Analysis (Big Picture Understanding)**

10. **Key Takeaway Synthesis**  
    *"If you had to explain the single most important idea from your essay to someone in 30 seconds, what would you say and why is it important?"*
    
    **Purpose:** Tests ability to synthesize and prioritize information
    
    **Evaluation Focus:** Clarity of thought, understanding of significance, communication skills

---

### Question Selection Algorithm (V0)

**For each essay submission:**

1. **Extract Keywords:** Identify 5-10 key concepts, technical terms, and themes
2. **Match Templates:** Map keywords to question templates using simple string matching
3. **Prioritize Diversity:** Select 3-5 questions ensuring at least 3 different categories represented
4. **Customize Questions:** Replace [PLACEHOLDERS] with actual essay content
   - [KEY CONCEPT] → extracted main topic
   - [TECHNICAL TERM] → identified specialized vocabulary
   - [SPECIFIC SOURCE] → citation or reference mentioned
   - [HYPOTHETICAL SCENARIO] → related situation based on essay domain

**Example for Computer Science Essay on "Machine Learning Algorithms":**
- Question 2: "You used the term 'gradient descent' in your work..."
- Question 3: "Walk me through how you arrived at comparing supervised vs unsupervised learning..."
- Question 8: "Can you give me a real-world example where gradient descent optimization would be critical?"
- Question 10: "If you had to explain the single most important idea about ML algorithms in 30 seconds..."

---

## Functional Requirements

### FR-1: User Authentication & Authorization

**Requirements:**
- Students can create accounts with university email addresses
- Professors can create accounts with verified faculty credentials
- Role-based access control (student vs professor views)
- Integration with university SSO (Single Sign-On) if available
- Password requirements: minimum 8 characters, 1 uppercase, 1 number
- Two-factor authentication optional for professors

**User Flows:**
1. New user registration → email verification → role selection → dashboard access
2. Returning user login → credential validation → dashboard redirect
3. Forgot password → email reset link → create new password

---

### FR-2: Essay Submission & Storage

**Requirements:**
- Support file formats: .txt, .docx, .pdf
- Maximum file size: 10MB
- Minimum essay length: 500 words
- Maximum essay length: 5000 words (warn if exceeded, but allow)
- Extract plain text from all formats
- Store original file + extracted text in database
- Associate submission with student ID and course ID
- Timestamp all submissions

**Data Model:**
```
Submission {
  id: UUID
  student_id: UUID (foreign key)
  course_id: UUID (foreign key)
  original_filename: string
  file_url: string (Supabase storage)
  extracted_text: text
  word_count: integer
  submitted_at: timestamp
  status: enum (uploaded, questions_generated, interview_complete, scored, feedback_sent)
}
```

**State Management:**
- uploaded → questions_generated → interview_complete → scored → feedback_sent

---

### FR-3: Question Generation System

**Requirements:**
- Generate 3-5 questions per essay within 2 minutes
- Use template question bank (10 templates)
- Extract keywords/concepts from essay using keyword extraction algorithm
- Match templates to essay content
- Replace placeholders with actual essay content
- Ensure question diversity (minimum 3 categories)
- Store generated questions with submission ID

**Algorithm Steps:**
1. Parse essay text
2. Extract keywords using TF-IDF or simple frequency analysis
3. Identify technical terms using discipline-specific dictionaries (optional for V0)
4. Map keywords to question templates
5. Select 3-5 best-matching templates
6. Customize questions with essay-specific content
7. Validate question grammaticality
8. Store in database

**Data Model:**
```
Question {
  id: UUID
  submission_id: UUID (foreign key)
  question_text: text
  question_category: enum (conceptual, process, critical, application, meta)
  order: integer (1-5)
  template_id: integer (1-10)
}
```

---

### FR-4: Voice Recording Interface

**Requirements:**
- Display one question at a time
- 60-second recording limit per question
- Visual countdown timer
- Start/Stop recording controls
- Waveform visualization during recording
- "Redo" option (1 retry per question)
- Save audio to Supabase storage
- Progress indicator (Question X of Y)
- Automatic advance to next question after successful recording
- Resume capability if session interrupted

**Recording Specifications:**
- Audio format: WebM (primary), WAV (fallback)
- Sample rate: 44.1kHz or 48kHz
- Bitrate: 128kbps minimum
- Channels: Mono

**Data Model:**
```
Recording {
  id: UUID
  question_id: UUID (foreign key)
  student_id: UUID (foreign key)
  audio_url: string (Supabase storage)
  duration: integer (seconds)
  recorded_at: timestamp
  attempt_number: integer (1 or 2)
  status: enum (recorded, transcribed, evaluated)
}
```

---

### FR-5: Transcription Pipeline

**Requirements:**
- Automatically trigger transcription when recording submitted
- Use speech-to-text API (OpenAI Whisper recommended)
- Store transcript with recording ID
- Flag low-confidence transcriptions for manual review
- Retry logic: 3 attempts on failure
- Handle diverse accents and speech patterns
- Preserve technical vocabulary accuracy
- Complete transcription within 30 seconds

**Transcription Confidence Thresholds:**
- High confidence: >85% → proceed with evaluation
- Medium confidence: 70-85% → proceed but flag in professor view
- Low confidence: <70% → flag for manual professor review

**Data Model:**
```
Transcript {
  id: UUID
  recording_id: UUID (foreign key)
  transcript_text: text
  confidence_score: float (0-100)
  transcription_service: string
  transcribed_at: timestamp
  flagged_for_review: boolean
}
```

---

### FR-6: AI Evaluation & Scoring System

**Requirements:**
- Evaluate student responses against original essay
- Generate score 0-100 based on weighted criteria
- Provide per-question scoring breakdown
- Generate rationale explaining score
- Complete evaluation within 2 minutes for all questions
- Store scores and rationale in database

**Scoring Criteria (Weighted):**

1. **Accuracy (40 points):**
   - Does verbal answer align with essay content?
   - Are facts and concepts correctly stated?
   - Subscore per question: 0-8 points

2. **Depth of Understanding (30 points):**
   - Can student explain concepts beyond surface level?
   - Do answers show synthesis and analysis?
   - Subscore per question: 0-6 points

3. **Consistency (20 points):**
   - Do answers align with each other?
   - Do verbal explanations match written essay logic?
   - Subscore per question: 0-4 points

4. **Technical Mastery (10 points):**
   - Correct use of discipline-specific terminology?
   - Appropriate depth of technical detail?
   - Subscore per question: 0-2 points

**Evaluation Process:**
1. Load essay text and all transcripts
2. For each question/answer pair:
   - Compare answer to relevant essay sections
   - Assess accuracy, depth, consistency, technical mastery
   - Generate per-question score
3. Aggregate scores across all questions
4. Generate overall rationale paragraph (150-250 words)
5. Store results

**Data Model:**
```
Evaluation {
  id: UUID
  submission_id: UUID (foreign key)
  overall_score: integer (0-100)
  accuracy_score: integer (0-40)
  depth_score: integer (0-30)
  consistency_score: integer (0-20)
  technical_score: integer (0-10)
  rationale: text
  evaluated_at: timestamp
  evaluation_model: string (e.g., "gpt-4-turbo")
}

QuestionScore {
  id: UUID
  evaluation_id: UUID (foreign key)
  question_id: UUID (foreign key)
  score: integer (0-20)
  feedback: text
}
```

---

### FR-7: Feedback Generation & Editing

**Requirements:**
- Auto-generate feedback paragraph (150-300 words) after scoring
- Structure: overall assessment → strengths → improvements → next steps
- Adapt tone based on score (encouraging for all, constructive for low scores)
- Professor can edit feedback in rich text editor
- Autosave edits every 30 seconds
- Support basic formatting (bold, italics, bullet points)
- Preview before sending to student

**Feedback Generation Prompts (by Score Range):**

**High Score (80-100):**
```
Tone: Congratulatory, encouraging
Focus: Affirm strengths, suggest minor refinements
Structure:
- Strong opening acknowledging excellent work
- 2-3 specific strengths with examples
- 1-2 minor areas for growth
- Encouraging closing
```

**Medium Score (50-79):**
```
Tone: Balanced, constructive
Focus: Recognize effort, identify gaps, provide guidance
Structure:
- Acknowledge effort and partial understanding
- 2 strengths with examples
- 2-3 areas needing improvement with specific examples
- Actionable next steps
```

**Low Score (<50):**
```
Tone: Supportive, developmental
Focus: Identify fundamental gaps, provide clear path forward
Structure:
- Empathetic opening acknowledging difficulty
- 1-2 positives (effort, attempt at engagement)
- 3 specific knowledge gaps with examples
- Concrete resources and strategies for improvement
- Encouraging closing emphasizing growth mindset
```

**Data Model:**
```
Feedback {
  id: UUID
  evaluation_id: UUID (foreign key)
  ai_generated_feedback: text
  professor_edited_feedback: text (nullable)
  final_feedback: text
  edited_by_professor: boolean
  sent_to_student: boolean
  sent_at: timestamp (nullable)
}
```

---

### FR-8: Professor Dashboard & Review Interface

**Requirements:**
- List all submissions for professor's courses
- Filter by status, score, student name, submission date
- Sort by any column
- Search functionality
- Detail view for individual submissions showing:
  - Original essay (full text or download)
  - Generated questions
  - Audio playback for each answer
  - Transcripts for each answer
  - Score breakdown (overall + per-question)
  - AI-generated feedback
- Edit feedback interface
- Approve/adjust score interface
- Send feedback to student
- Export data to CSV
- Pagination for large classes (25 submissions per page)

**Dashboard Views:**

**1. Submissions List View:**
```
Columns: Student Name | Submission Date | Status | Score | Actions
Status indicators: 
  - Gray: Awaiting student interview
  - Blue: Interview complete, awaiting review
  - Yellow: Review in progress
  - Green: Feedback sent
```

**2. Detail View:**
```
Tabs:
  - Essay: Full text with download option
  - Interview: Q&A pairs with audio playback
  - Evaluation: Scores and rationale
  - Feedback: Edit and send
```

**3. Batch Actions:**
- Select multiple submissions
- Bulk send feedback
- Bulk export

---

### FR-9: Student Results Portal

**Requirements:**
- Student can view only their own submissions
- Display submission status (pending interview, interview complete, awaiting feedback, feedback available)
- Once feedback released:
  - Overall score with visual representation
  - Professor's feedback paragraph
  - Transcripts of their answers (optional visibility)
  - Next steps and resources
- Download feedback as PDF
- Clear path for academic appeals if needed
- Email notification when feedback available

**Student Results View:**
```
Components:
  - Score Card (large, centered)
  - Feedback Section (professor's edited feedback)
  - Interview Recap (questions asked + student's transcripts)
  - Next Steps (professor recommendations)
  - Download PDF button
```

---

### FR-10: Notification System

**Requirements:**
- Email notifications for:
  - Student: Questions ready for interview
  - Student: Feedback available
  - Professor: Student completed interview
  - Professor: System error or manual review needed
- In-app notifications (bell icon with count)
- Notification preferences (email on/off per type)

**Notification Triggers:**
```
Event: Essay submitted → Notify: Student (questions generating)
Event: Questions ready → Notify: Student (begin interview)
Event: Interview complete → Notify: Professor (review available)
Event: Feedback sent → Notify: Student (view results)
Event: System error → Notify: Both parties + admin
```

---

## Non-Functional Requirements

### NFR-1: Performance

**Response Times:**
- Essay upload: <5 seconds for 10MB file
- Question generation: <2 minutes
- Audio upload: <3 seconds per recording
- Transcription: <30 seconds per 60-second recording
- Evaluation & scoring: <2 minutes for 5 questions
- Dashboard load: <3 seconds for classes up to 200 students
- Page transitions: <1 second

**Throughput:**
- Support 500 concurrent students during peak submission periods
- Handle 100 simultaneous professor dashboard sessions
- Process 1000 essay submissions per day

---

### NFR-2: Scalability

**Horizontal Scaling:**
- Stateless application tier (can add servers as needed)
- Distributed task queue for transcription and evaluation
- CDN for audio file delivery
- Database read replicas for professor dashboard queries

**Capacity Planning:**
- Initial target: 10 courses, ~500 students
- 6-month target: 50 courses, ~2500 students
- 1-year target: 200 courses, ~10,000 students

**Resource Limits:**
- Maximum essay size: 10MB
- Maximum audio recording: 60 seconds
- Maximum concurrent recordings: 500
- Maximum questions per essay: 5

---

### NFR-3: Reliability & Availability

**Uptime Target:** 99.5% (excluding planned maintenance)

**Failure Handling:**
- Automatic retry for failed transcriptions (3 attempts)
- Automatic retry for failed AI evaluations (3 attempts)
- Graceful degradation: if AI evaluation fails, allow professor to manually score
- Audio file redundancy (stored in multiple locations)
- Database backup every 24 hours with 30-day retention

**Error Recovery:**
- Student can resume incomplete interview from last saved question
- Auto-save professor feedback edits every 30 seconds
- Transaction rollback on database errors

---

### NFR-4: Security

**Authentication:**
- Secure password hashing (bcrypt or Argon2)
- JWT tokens with 24-hour expiration
- Session invalidation on logout
- HTTPS required for all connections

**Authorization:**
- Role-based access control (RBAC)
- Students can only access their own submissions
- Professors can only access submissions for their courses
- Admin role for system management

**Data Protection:**
- Encryption at rest for audio files and essays
- Encryption in transit (TLS 1.3)
- API keys stored in environment variables (not in code)
- Input validation on all user inputs to prevent injection attacks

**Audit Logging:**
- Log all access to student data
- Log all professor actions (view, edit, send feedback)
- Log all system errors and failures
- Retain logs for 1 year

---

### NFR-5: Accessibility

**WCAG 2.1 Level AA Compliance:**
- Keyboard navigation for all interactive elements
- Screen reader compatibility (ARIA labels)
- Sufficient color contrast (4.5:1 minimum)
- Focus indicators on all interactive elements
- Alt text for all images and icons
- Captions/transcripts available for audio content (ironic but important)

**Responsive Design:**
- Mobile-friendly interface (students may submit from phones)
- Touch-friendly buttons and controls
- Adaptive layouts for tablets and desktops

**Assistive Technology Support:**
- Students with speech disabilities can request accommodation (manual interview)
- Students with hearing disabilities receive visual feedback during recording
- Students with vision disabilities can use screen readers throughout

---

### NFR-6: Usability

**User Experience Principles:**
- Minimize clicks to complete tasks
- Clear error messages with actionable solutions
- Progressive disclosure (show complexity only when needed)
- Consistent UI patterns across all pages
- Confirmation dialogs for destructive actions

**Onboarding:**
- First-time student: guided tutorial for essay submission and interview
- First-time professor: sample submission walkthrough
- Context-sensitive help tooltips

**Mobile Experience:**
- Students can complete entire workflow on mobile
- Professors can review submissions on mobile (with desktop recommended for efficiency)

---

### NFR-7: Maintainability

**Code Quality:**
- Modular architecture (separate services for upload, transcription, evaluation)
- Comprehensive error handling and logging
- Unit test coverage >80%
- Integration test coverage for critical user flows
- API documentation (Swagger/OpenAPI)

**Monitoring:**
- Application performance monitoring (APM)
- Error tracking (Sentry or similar)
- Usage analytics (submission volumes, completion rates)
- API latency monitoring
- Database query performance monitoring

**DevOps:**
- CI/CD pipeline (automated testing and deployment)
- Staging environment for testing
- Feature flags for gradual rollouts
- Database migration scripts

---

## Technical Architecture

### High-Level System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Frontend Layer                        │
├──────────────────────┬──────────────────────────────────────┤
│  Student Interface   │      Professor Dashboard             │
│  - Essay Upload      │      - Submission Review             │
│  - Voice Recording   │      - Feedback Editor               │
│  - Results View      │      - Analytics                     │
└──────────────────────┴──────────────────────────────────────┘
                              ↓ ↑
┌─────────────────────────────────────────────────────────────┐
│                     API Gateway Layer                        │
│              (Authentication, Rate Limiting)                 │
└─────────────────────────────────────────────────────────────┘
                              ↓ ↑
┌─────────────────────────────────────────────────────────────┐
│                    Application Services                      │
├──────────────────┬──────────────────┬──────────────────────┤
│  Submission      │  Interview       │  Evaluation          │
│  Service         │  Service         │  Service             │
│  - File Upload   │  - Recording     │  - Scoring           │
│  - Text Extract  │  - Transcription │  - Feedback Gen      │
│  - Question Gen  │  - Storage       │  - Review            │
└──────────────────┴──────────────────┴──────────────────────┘
                              ↓ ↑
┌─────────────────────────────────────────────────────────────┐
│                     External Services                        │
├──────────────────┬──────────────────┬──────────────────────┤
│  Supabase        │  OpenAI/Anthropic│  Email Service       │
│  - Auth          │  - Whisper (STT) │  - Notifications     │
│  - Database      │  - GPT-4 (Eval)  │  - Transactional     │
│  - Storage       │  - Embeddings    │                      │
└──────────────────┴──────────────────┴──────────────────────┘
```

### Technology Stack Recommendations

**Frontend:**
- Framework: React with TypeScript
- State Management: Redux or Zustand
- UI Library: Tailwind CSS + shadcn/ui components
- Audio Recording: Web Audio API + RecordRTC library
- Audio Playback: Howler.js or native HTML5 audio
- Rich Text Editor: Tiptap or Quill

**Backend:**
- Framework: Node.js with Express or Python with FastAPI
- Task Queue: Bull (Redis-based) for async jobs
- WebSocket: Socket.io for real-time updates (optional)

**Database & Storage:**
- Primary Database: Supabase (PostgreSQL)
- File Storage: Supabase Storage (S3-compatible)
- Caching: Redis (for session management and job queue)

**External APIs:**
- Speech-to-Text: OpenAI Whisper API
- AI Evaluation: OpenAI GPT-4 or Anthropic Claude
- Email: SendGrid or AWS SES

**DevOps:**
- Hosting: Vercel (frontend) + Railway/Render (backend)
- CI/CD: GitHub Actions
- Monitoring: Sentry (errors) + Vercel Analytics
- Logging: Winston or Pino

---

### Database Schema (Simplified)

**Users Table:**
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  role VARCHAR(20) NOT NULL CHECK (role IN ('student', 'professor', 'admin')),
  full_name VARCHAR(255),
  university_id VARCHAR(100),
  created_at TIMESTAMP DEFAULT NOW()
);
```

**Courses Table:**
```sql
CREATE TABLE courses (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  professor_id UUID REFERENCES users(id),
  course_code VARCHAR(50),
  course_name VARCHAR(255),
  created_at TIMESTAMP DEFAULT NOW()
);
```

**Submissions Table:**
```sql
CREATE TABLE submissions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  student_id UUID REFERENCES users(id),
  course_id UUID REFERENCES courses(id),
  original_filename VARCHAR(255),
  file_url TEXT,
  extracted_text TEXT,
  word_count INTEGER,
  status VARCHAR(50) DEFAULT 'uploaded',
  submitted_at TIMESTAMP DEFAULT NOW()
);
```

**Questions Table:**
```sql
CREATE TABLE questions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  submission_id UUID REFERENCES submissions(id),
  question_text TEXT NOT NULL,
  question_category VARCHAR(50),
  order_number INTEGER,
  template_id INTEGER
);
```

**Recordings Table:**
```sql
CREATE TABLE recordings (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  question_id UUID REFERENCES questions(id),
  audio_url TEXT NOT NULL,
  duration INTEGER,
  recorded_at TIMESTAMP DEFAULT NOW()
);
```

**Transcripts Table:**
```sql
CREATE TABLE transcripts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  recording_id UUID REFERENCES recordings(id),
  transcript_text TEXT,
  confidence_score FLOAT,
  flagged_for_review BOOLEAN DEFAULT FALSE,
  transcribed_at TIMESTAMP DEFAULT NOW()
);
```

**Evaluations Table:**
```sql
CREATE TABLE evaluations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  submission_id UUID REFERENCES submissions(id),
  overall_score INTEGER CHECK (overall_score BETWEEN 0 AND 100),
  accuracy_score INTEGER,
  depth_score INTEGER,
  consistency_score INTEGER,
  technical_score INTEGER,
  rationale TEXT,
  evaluated_at TIMESTAMP DEFAULT NOW()
);
```

**Feedback Table:**
```sql
CREATE TABLE feedback (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  evaluation_id UUID REFERENCES evaluations(id),
  ai_generated_feedback TEXT,
  professor_edited_feedback TEXT,
  final_feedback TEXT,
  edited_by_professor BOOLEAN DEFAULT FALSE,
  sent_to_student BOOLEAN DEFAULT FALSE,
  sent_at TIMESTAMP
);
```

---

## User Journey Maps

### Student Journey: Complete Workflow

**Step 1: Essay Submission**
- Student logs in → navigates to "Submit Essay"
- Uploads .docx file (2000 words)
- System confirms: "Upload successful! Questions will be ready in 2-3 minutes."
- Student receives email notification when questions ready

**Step 2: Interview Preparation**
- Student clicks notification link → redirected to interview page
- Instructions displayed: "Answer 4 questions about your essay. You'll have 60 seconds per question. Take a moment to read each question before recording."
- Student clicks "Start Interview"

**Step 3: Recording Answers**
- Question 1 appears: "In your essay, you discussed 'neural network architecture.' Can you explain..."
- Student clicks "Start Recording" → 60-second timer begins
- Student speaks for 45 seconds → clicks "Stop & Submit"
- System confirms: "Answer saved. Question 2 of 4"
- Process repeats for all 4 questions

**Step 4: Waiting for Feedback**
- After final question: "Interview complete! Your professor will review your responses within 48 hours."
- Student receives email when professor sends feedback

**Step 5: Viewing Results**
- Student logs in → sees notification "Feedback Available"
- Views score: 78/100
- Reads professor feedback (edited by professor from AI draft)
- Downloads PDF for records

**Estimated Time:** 15 minutes (2 min upload + 3 min wait + 8 min interview + 2 min review)

---

### Professor Journey: Review Workflow

**Step 1: Notification**
- Professor receives email: "5 students have completed interviews for CS101"
- Logs in to dashboard

**Step 2: Prioritized Review**
- Dashboard shows 30 submissions, sorted by score (lowest first)
- Notices flagged submission (low transcription confidence)
- Clicks on lowest-scored submission (Score: 42)

**Step 3: Detailed Review**
- Views original essay (well-written, 1800 words)
- Reads generated questions (4 questions)
- Plays audio recording for Question 1 → listens to student's answer
- Reads transcript → notices significant discrepancies with essay
- Reviews score breakdown:
  - Accuracy: 12/40 (many incorrect statements)
  - Depth: 8/30 (surface-level understanding)
  - Consistency: 6/20 (contradicts essay)
  - Technical: 4/10 (misuses terms)

**Step 4: Feedback Editing**
- Reads AI-generated feedback (constructive, identifies specific gaps)
- Edits opening sentence to be more encouraging
- Adds specific office hours invitation
- Previews feedback → clicks "Send to Student"

**Step 5: Bulk Actions**
- Reviews next 10 submissions (most scores 70-85, reasonable)
- Makes minor edits to 3 feedback paragraphs
- Selects 8 submissions → clicks "Send Feedback" (bulk action)

**Step 6: Export & Records**
- Exports all scores to CSV for gradebook integration
- Reviews analytics: average score 73, completion rate 95%

**Estimated Time:** 3 minutes per detailed review, 1 minute per quick review

---

## Implementation Roadmap

### V0 (MVP - Prototype) - 6 Weeks

**Goal:** Demonstrate core workflow with template-based questions

**Features:**
- Student essay upload (text extraction)
- Template question bank (10 questions)
- Simple keyword matching for question selection
- Voice recording interface (5 questions max)
- Manual transcription upload (workaround for API costs)
- Basic scoring algorithm (rule-based, not AI)
- Professor view of submissions and scores
- Simple feedback text area (no AI generation)

**Success Criteria:**
- 5 professors test with 20 students each
- 80% completion rate
- Basic functionality validation

**Technical Priorities:**
- Core database schema
- File upload and storage
- Recording interface
- Professor dashboard MVP

---

### V1 (Enhanced Evaluation) - 4 Weeks

**Goal:** Integrate AI transcription and evaluation

**Features:**
- Automated transcription (Whisper API)
- AI-powered evaluation and scoring (GPT-4)
- AI-generated feedback paragraphs
- Rich text feedback editor for professors
- Email notifications
- Per-question score breakdown

**Success Criteria:**
- AI evaluation accuracy >75% alignment with professor judgment
- Feedback generation quality rated 4+/5 by professors
- Transcription accuracy >90% for clear audio

**Technical Priorities:**
- API integration (OpenAI)
- Async job queue for transcription/evaluation
- Feedback editor UI

---

### V2 (Dynamic Questions & Scale) - 6 Weeks

**Goal:** Improve question relevance and support larger scale

**Features:**
- RAG-based question generation (essay-specific questions)
- Question difficulty adaptation
- Support for larger classes (500+ students)
- Analytics dashboard for professors
- Student performance trends
- Batch operations for professors
- Mobile app (optional)

**Success Criteria:**
- Questions rated as "highly relevant" by 80% of professors
- Support 50 courses simultaneously
- Dashboard load time <3 seconds for 200+ students

**Technical Priorities:**
- RAG implementation with vector database
- Performance optimization
- Caching layer
- Mobile responsiveness

---

### V3 (Advanced Features) - 8 Weeks

**Goal:** Enterprise features and integrations

**Features:**
- LMS integration (Canvas, Blackboard, Moodle)
- Multi-language support
- Advanced analytics and insights
- Plagiarism detection integration
- Student learning pathways based on feedback
- Peer comparison (anonymized)
- Video recording option (in addition to audio)

**Success Criteria:**
- LMS adoption by 3+ universities
- Multi-language support for 5 languages
- Student satisfaction >4/5

---

## Risk Assessment & Mitigation

### Risk 1: AI Evaluation Inaccuracy (High Impact, Medium Probability)

**Description:** AI scoring may not align with professor expectations, leading to distrust in the system.

**Impact:**
- Professors reject the tool
- Students feel unfairly evaluated
- Reputational damage

**Mitigation Strategies:**
1. Clearly position scores as "preliminary" requiring professor review
2. A/B testing of evaluation prompts with professor feedback loop
3. Allow professors to adjust scores and provide feedback to improve algorithm
4. Transparent score breakdown showing reasoning
5. Fallback to manual review for flagged cases

**Contingency Plan:**
- Offer "manual mode" where professors score with AI as reference only
- Continuous model fine-tuning based on professor corrections

---

### Risk 2: Poor Transcription Quality (Medium Impact, Medium Probability)

**Description:** Whisper or chosen STT service struggles with accents, technical vocabulary, or poor audio quality.

**Impact:**
- Inaccurate evaluation based on wrong transcripts
- Student frustration with misunderstood answers
- Increased manual review burden

**Mitigation Strategies:**
1. Audio quality checks before accepting recording
2. Confidence score thresholds for flagging
3. Allow students to review and confirm transcripts before submission (V1 feature)
4. Multiple STT service fallback (try alternative if confidence low)
5. Professor access to original audio for verification

**Contingency Plan:**
- Manual transcription service for flagged recordings
- Student option to re-record if transcription clearly wrong

---

### Risk 3: Student Gaming the System (Medium Impact, Low Probability)

**Description:** Students attempt to record essay text verbatim or use notes during "viva."

**Impact:**
- System fails to detect lack of understanding
- Defeats purpose of verification

**Mitigation Strategies:**
1. Questions designed to test understanding, not memorization (explanations, applications, counterfactuals)
2. Randomize question order and selection
3. Detection of overly scripted/read responses (V2 feature: prosody analysis)
4. Time pressure (60 seconds) makes reading difficult
5. Professor review of flagged "too perfect" responses

**Contingency Plan:**
- Proctoring option for high-stakes assessments
- Video recording to detect reading behavior (V3)

---

### Risk 4: Scalability Issues (High Impact, Low Probability)

**Description:** System cannot handle peak submission periods (end of semester) or large concurrent users.

**Impact:**
- Slow question generation, transcription, evaluation
- System downtime
- Student frustration and missed deadlines

**Mitigation Strategies:**
1. Async job queue architecture from day one
2. Auto-scaling infrastructure (serverless functions)
3. CDN for audio file delivery
4. Database optimization and indexing
5. Load testing before each semester
6. Staggered deadlines (encourage early submission)

**Contingency Plan:**
- Manual processing queue if automation fails
- Extended deadlines during outages
- Transparent status page for users

---

### Risk 5: Privacy & Data Security Concerns (High Impact, Low Probability)

**Description:** Student audio recordings or essays leaked, hacked, or misused.

**Impact:**
- Legal liability (FERPA violations in US)
- Loss of trust
- University partnership terminations

**Mitigation Strategies:**
1. Encryption at rest and in transit (already in NFRs)
2. Access control auditing
3. Regular security audits and penetration testing
4. Data retention policies (auto-delete after 1 year)
5. Clear privacy policy and terms of service
6. Compliance with FERPA, GDPR (even though initially deprioritized)

**Contingency Plan:**
- Incident response plan for data breaches
- Cyber insurance
- Legal counsel on retainer

---

### Risk 6: User Adoption Resistance (Medium Impact, Medium Probability)

**Description:** Professors or students resist using the system due to perceived complexity, unfairness, or additional workload.

**Impact:**
- Low adoption rates
- Negative word-of-mouth
- Product failure

**Mitigation Strategies:**
1. Extensive user testing and feedback loops during development
2. Clear value proposition communication (time savings for professors, fairness for students)
3. Onboarding tutorials and support documentation
4. Pilot program with champion professors
5. Gather and showcase testimonials
6. Make system optional initially, not mandatory

**Contingency Plan:**
- Simplified "lite mode" for hesitant users
- White-glove onboarding for early adopters
- Direct user support during pilot phase

---

## Success Metrics & KPIs

### Product-Market Fit Metrics

**Primary KPI: Professor Adoption Rate**
- Target: 60% of pilot professors use for ≥3 assignments within first semester
- Measurement: Track professor logins, submissions reviewed, feedback sent

**Secondary KPI: Student Completion Rate**
- Target: 85% of students complete interview within 48 hours of essay submission
- Measurement: Track interview completion vs total essay submissions

**Secondary KPI: Professor Satisfaction (NPS)**
- Target: Net Promoter Score ≥40
- Measurement: Quarterly survey asking "How likely are you to recommend this tool?"

---

### Operational Metrics

**System Performance:**
- Question generation time: <2 minutes (95th percentile)
- Transcription time: <30 seconds (95th percentile)
- Evaluation time: <2 minutes (95th percentile)
- Dashboard load time: <3 seconds (95th percentile)

**Reliability:**
- Uptime: ≥99.5%
- Transcription success rate: ≥95% (without manual intervention)
- Evaluation completion rate: ≥98%

**Quality Metrics:**
- AI evaluation accuracy: ≥75% alignment with professor final judgment
- Transcription accuracy: ≥90% (word error rate <10%)
- Feedback relevance: Professor edit rate <50% (meaning most feedback is kept as-is)

---

### User Engagement Metrics

**Student Metrics:**
- Average time to complete interview: Track median (target: <15 minutes)
- Redo rate: % of questions re-recorded (target: <20%)
- Feedback view rate: % of students who view feedback (target: >90%)

**Professor Metrics:**
- Average review time per submission: Track median (target: <3 minutes)
- Feedback edit rate: % of feedback edited before sending (target: 30-70%)
- Bulk action usage: % of professors using batch send (target: >50%)
- Analytics dashboard usage: % of professors viewing analytics (target: >40%)

---

### Business Metrics (Future)

**Growth:**
- Monthly Active Professors (MAP)
- Monthly Active Students (MAS)
- Number of courses using system
- Number of universities using system

**Retention:**
- Professor retention (semester-over-semester)
- Course retention (% of courses that continue using after first semester)

**Revenue (if applicable):**
- Revenue per professor
- Customer acquisition cost (CAC)
- Lifetime value (LTV)

---

## Open Questions & Assumptions

### Critical Unknowns (Need User Feedback)

1. **Question Count Optimal Balance:**
   - Is 3-5 questions sufficient, or do professors want more depth?
   - Should question count vary by essay length?

2. **Scoring Transparency:**
   - Should students see their per-question scores, or only overall score?
   - Should students see the AI rationale, or only professor feedback?

3. **Time Pressure Trade-offs:**
   - Is 60 seconds per question the right balance between authenticity and stress?
   - Should different question types have different time limits?

4. **Feedback Iteration:**
   - Should students be able to respond to feedback or request clarification?
   - Should there be a "dispute score" mechanism?

5. **Integration Priorities:**
   - Which LMS integration is most critical first? (Canvas, Blackboard, Moodle)
   - Should we prioritize LMS integration over standalone product?

---

### Assumptions to Validate

**User Behavior Assumptions:**
- Students will complete interviews shortly after submission (within 48 hours)
- Professors will trust AI-generated scores as a starting point
- 60-second answers are sufficient for assessment
- Students have access to microphone-enabled devices

**Technical Assumptions:**
- OpenAI Whisper provides sufficient transcription accuracy for academic content
- GPT-4 evaluation prompts can be tuned to match professor standards
- Supabase can scale to 10,000+ students
- Web Audio API works reliably across all major browsers

**Market Assumptions:**
- Universities care enough about academic integrity to adopt this tool
- Professors will accept AI-assisted evaluation
- Students won't perceive this as "surveillance" or unfair
- The system provides value beyond existing plagiarism detection tools

---

## Appendices

### Appendix A: Competitor Analysis

**Existing Solutions:**

1. **Turnitin:**
   - Focus: Plagiarism detection, AI writing detection
   - Gap: Doesn't test comprehension, only detects copying

2. **Respondus LockDown Browser:**
   - Focus: Exam proctoring
   - Gap: Doesn't assess essay-specific knowledge, requires special software

3. **Honorlock / ProctorU:**
   - Focus: Live proctoring
   - Gap: Expensive, invasive, doesn't specifically test essay comprehension

4. **Manual Viva/Oral Exams:**
   - Focus: In-person knowledge verification
   - Gap: Time-intensive, doesn't scale, inconsistent

**Our Differentiation:**
- Automated oral examination specifically about submitted essays
- Scalable (handle hundreds of students)
- Augments professor judgment rather than replacing it
- Provides actionable feedback, not just detection

---

### Appendix B: Sample AI Evaluation Prompt (V1)

```
You are an expert academic evaluator assessing a university student's understanding of their submitted essay through a verbal interview.

CONTEXT:
- Student Essay: [FULL ESSAY TEXT]
- Question Asked: [QUESTION TEXT]
- Student's Verbal Answer (Transcript): [TRANSCRIPT TEXT]

TASK:
Evaluate the student's answer on a scale of 0-20 points based on:
1. Accuracy (8 points): Does the answer align with the essay content? Are facts correct?
2. Depth (6 points): Does the answer show deep understanding or just surface-level knowledge?
3. Consistency (4 points): Does the answer align with the essay's arguments and other answers?
4. Technical Mastery (2 points): Correct use of discipline-specific terminology?

Provide:
- Score: [0-20]
- Accuracy subscore: [0-8]
- Depth subscore: [0-6]
- Consistency subscore: [0-4]
- Technical subscore: [0-2]
- Brief rationale (50 words): Explain the score with specific examples

Be fair but discerning. A good answer should demonstrate genuine understanding, not just repeat essay phrases.
```

---

### Appendix C: Sample Feedback Generation Prompt (V1)

```
You are writing constructive feedback for a university student who completed an oral interview about their essay.

CONTEXT:
- Student Essay Topic: [TOPIC]
- Overall Score: [SCORE]/100
- Key Strengths: [LIST 2-3]
- Key Weaknesses: [LIST 2-3]
- Question Performance: [PER-QUESTION SCORES]

TASK:
Write feedback paragraph (150-300 words) that:
1. Opens with overall assessment (positive framing even for low scores)
2. Highlights 2-3 specific strengths with examples
3. Identifies 2-3 areas for improvement with specific examples
4. Provides actionable next steps
5. Closes with encouragement

TONE:
- High scores (80-100): Congratulatory but suggest refinements
- Medium scores (50-79): Balanced, constructive, supportive
- Low scores (<50): Empathetic, developmental, growth-focused

Remember: This is a learning opportunity. Be specific, constructive, and encouraging.
```

---

### Appendix D: Template Question Bank (Full Details)

*[See "Template Question Bank" section above for complete 10-question list with evaluation guidelines]*

---

### Appendix E: Glossary

- **Viva (Viva Voce):** Oral examination where student defends their work verbally
- **RAG (Retrieval-Augmented Generation):** AI technique combining retrieval of relevant documents with generation
- **STT (Speech-to-Text):** Technology converting spoken audio to written text
- **LMS (Learning Management System):** Platform like Canvas, Blackboard used for course management
- **NPS (Net Promoter Score):** Customer satisfaction metric (-100 to +100)
- **FERPA:** Family Educational Rights and Privacy Act (US student privacy law)
- **TF-IDF:** Term Frequency-Inverse Document Frequency (text analysis technique)
- **WCAG:** Web Content Accessibility Guidelines
- **P0/P1/P2:** Priority levels (P0 = critical, P1 = important, P2 = nice-to-have)

---

## Document Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | Nov 22, 2025 | Product Manager | Initial comprehensive PRD created from stakeholder meeting |

---

## Sign-Off & Approvals

**Product Owner:** _____________________________ Date: _________

**Engineering Lead:** _____________________________ Date: _________

**Design Lead:** _____________________________ Date: _________

**Stakeholder (Faculty Representative):** _____________________________ Date: _________

---

## Next Steps

1. **Review & Refinement:** Share with engineering, design, and key stakeholders for feedback (1 week)
2. **Technical Feasibility Assessment:** Engineering team evaluates architecture and API choices (1 week)
3. **Design Mockups:** UI/UX team creates wireframes for student and professor interfaces (2 weeks)
4. **Development Kickoff:** Begin V0 sprint planning with prioritized feature backlog (Week 4)
5. **Pilot Recruitment:** Identify 5 champion professors for V0 testing (concurrent with development)

**Target V0 Launch:** 6 weeks from kickoff  
**Target V1 Launch:** 10 weeks from kickoff

---

**Document Status:** ✅ READY FOR REVIEW  
**Confidence Level:** High (based on detailed stakeholder discussion)  
**Outstanding Questions:** See "Open Questions & Assumptions" section - recommend user research with professors and students during V0 development.
