erDiagram

    USERS {
        string _id
        string email
        string passwordHash
        string role
    }

    RESUMES {
        string _id
        string candidateId
        string rawText
        string skills
        string experienceSummary
        string embeddingVector
        date createdAt
    }

    JOBS {
        string _id
        string recruiterId
        string title
        string requiredSkills
        string experienceLevel
        string embeddingVector
        date createdAt
    }

    MATCH_RESULTS {
        string _id
        string jobId
        string resumeId
        float finalScore
        int rank
        string scoreBreakdown
    }

    FEEDBACK {
        string _id
        string matchResultId
        string recruiterId
        string decision
        date createdAt
    }

    SCORING_PROFILES {
        string _id
        float skillWeight
        float experienceWeight
        float semanticWeight
        date effectiveFrom
    }

    USERS ||--o{ RESUMES : owns
    USERS ||--o{ JOBS : creates
    JOBS ||--o{ MATCH_RESULTS : produces
    RESUMES ||--o{ MATCH_RESULTS : participates
    MATCH_RESULTS ||--|| FEEDBACK : has