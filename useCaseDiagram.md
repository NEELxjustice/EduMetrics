flowchart LR

    Candidate((Candidate))
    Recruiter((Recruiter))
    Admin((Admin))

    subgraph HireLens_AI_System
        UC1[Register / Login]
        UC2[Upload Resume]
        UC3[View Resume Insights]
        UC4[Upload Job Description]
        UC5[View Ranked Candidates]
        UC6[View Match Explanation]
        UC7[Give Feedback on Match]
        UC8[Manage Users]
        UC9[Monitor Model Performance]
    end

    Candidate --> UC1
    Candidate --> UC2
    Candidate --> UC3

    Recruiter --> UC1
    Recruiter --> UC4
    Recruiter --> UC5
    Recruiter --> UC6
    Recruiter --> UC7

    Admin --> UC8
    Admin --> UC9