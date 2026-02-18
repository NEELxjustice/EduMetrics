# Sequence Diagram – HireLens AI Matching Flow

```mermaid
sequenceDiagram
    autonumber

    actor Candidate
    actor Recruiter
    actor Admin

    participant UI as Web App (Frontend)
    participant API as Backend API
    participant AI as Matching Engine
    participant DB as Database

    %% Candidate uploads resume
    Candidate ->> UI: Upload resume
    UI ->> API: POST /resumes
    API ->> AI: Generate resume embedding
    AI -->> API: Resume vector
    API ->> DB: Store resume + embedding
    API -->> UI: Upload success

    %% Recruiter uploads job
    Recruiter ->> UI: Upload job description
    UI ->> API: POST /jobs
    API ->> AI: Generate job embedding
    AI -->> API: Job vector
    API ->> DB: Store job + embedding
    API -->> UI: Job created

    %% Recruiter requests matching
    Recruiter ->> UI: View ranked candidates
    UI ->> API: GET /jobs/{id}/matches
    API ->> DB: Fetch resumes & job
    API ->> AI: Compute similarity scores
    AI -->> API: Scores + explanations
    API ->> DB: Store match results
    API -->> UI: Ranked candidates list

    %% Recruiter gives feedback
    Recruiter ->> UI: Submit feedback
    UI ->> API: POST /feedback
    API ->> DB: Save feedback

    %% Admin monitors system
    Admin ->> UI: View model performance
    UI ->> API: GET /admin/metrics
    API ->> DB: Fetch logs & stats
    API -->> UI: Metrics dashboard