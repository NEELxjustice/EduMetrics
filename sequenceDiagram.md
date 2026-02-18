# Sequence Diagram – HireLens AI

## Main End-to-End Flow

Resume Upload → Job Upload → Matching → Feedback → Adaptive Update

---

## Actors

- Candidate
- Recruiter

---

## Flow Description

1. Candidate uploads a resume.
2. The system extracts text from the resume.
3. The system extracts skills and experience.
4. The system generates a semantic embedding.
5. The resume profile is stored.

6. Recruiter uploads a job description.
7. The system extracts required skills and experience level.
8. The system generates a semantic embedding.
9. The job profile is stored.

10. Recruiter requests ranked candidates for a job.
11. The system fetches all resumes.
12. The matching engine computes similarity and weighted scores.
13. The ranked list is generated and stored.
14. The ranked candidates are returned to the recruiter.

15. Recruiter submits feedback on a candidate.
16. Feedback is stored.

17. The adaptive scoring engine analyses historical feedback.
18. The scoring weights are updated.
19. A new scoring profile becomes active for future matches.