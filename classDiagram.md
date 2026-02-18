# Class Diagram – HireLens AI

## Core Domain Classes

### User
- id
- email
- role

### Candidate (extends User)

### Recruiter (extends User)

### Admin (extends User)

---

### Resume
- id
- candidateId
- rawText
- skills
- experienceSummary
- embeddingVector

---

### JobDescription
- id
- recruiterId
- title
- requiredSkills
- experienceLevel
- embeddingVector

---

### MatchResult
- id
- jobId
- resumeId
- finalScore
- rank
- scoreBreakdown

---

### Feedback
- id
- matchResultId
- recruiterId
- decision
- createdAt

---

### ScoringProfile
- id
- skillWeight
- experienceWeight
- semanticWeight
- effectiveFrom

---

## Service Layer

### ResumeService
- processResume()

### JobService
- processJobDescription()

### MatchService
- generateMatches()

### FeedbackService
- recordFeedback()

---

## Domain Engines

### MatchingEngine
- computeSimilarityScore()
- computeWeightedScore()
- rankCandidates()

### AdaptiveScoringEngine
- analyseFeedbackHistory()
- updateScoringWeights()

---

## Relationships

- Candidate owns many Resume
- Recruiter owns many JobDescription
- JobDescription produces many MatchResult
- Resume participates in many MatchResult
- MatchResult has one Feedback
- MatchingEngine is used by MatchService
- AdaptiveScoringEngine is used by FeedbackService