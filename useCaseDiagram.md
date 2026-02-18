# Use Case Diagram – HireLens AI System

```mermaid
flowchart LR

%% Actors
Candidate[Candidate]
Recruiter[Recruiter]
Admin[Admin]

%% System boundary
subgraph HireLens_AI_System[HireLens AI System]

    UC1((Register / Login))
    UC2((Upload Resume))
    UC3((View Resume Insights))
    UC4((Upload Job Description))
    UC5((View Ranked Candidates))
    UC6((View Match Explanation))
    UC7((Give Feedback on Match))
    UC8((Manage Users))
    UC9((Monitor Model Performance))

end

%% Candidate interactions
Candidate --> UC1
Candidate --> UC2
Candidate --> UC3

%% Recruiter interactions
Recruiter --> UC1
Recruiter --> UC4
Recruiter --> UC5
Recruiter --> UC6
Recruiter --> UC7

%% Admin interactions
Admin --> UC8
Admin --> UC9