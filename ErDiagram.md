# ER Diagram – HireLens AI

## users
- _id
- email
- passwordHash
- role

---

## resumes
- _id
- candidateId (FK → users._id)
- rawText
- skills
- experienceSummary
- embeddingVector
- createdAt

---

## jobs
- _id
- recruiterId (FK → users._id)
- title
- requiredSkills
- experienceLevel
- embeddingVector
- createdAt

---

## match_results
- _id
- jobId (FK → jobs._id)
- resumeId (FK → resumes._id)
- finalScore
- rank
- scoreBreakdown

---

## feedback
- _id
- matchResultId (FK → match_results._id)
- recruiterId (FK → users._id)
- decision
- createdAt

---

## scoring_profiles
- _id
- skillWeight
- experienceWeight
- semanticWeight
- effectiveFrom

---

## Relationships

- One candidate (user) can have many resumes
- One recruiter (user) can create many jobs
- One job can have many match results
- One resume can appear in many match results
- One match result can have one feedback