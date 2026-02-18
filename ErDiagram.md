erDiagram

    USERS {
        string id
        string email
        string passwordHash
        string role
    }

    RESUMES {
        string id
        string candidateId
        string rawText
        string skills
        string experienceSummary
        string embeddingVector
        datetime createdAt
    }

    JOBS {
        string id
        string recruiterId
        string title
        string requiredSkills
        string experienceLevel
        string embeddingVector
        datetime createdAt
    }

    MATCH_RESULTS {
        string id
        string jobId
        string resumeId
        float finalScore
        int rank
        string scoreBreakdown
    }

    FEEDBACK {
        string id
        string matchResultId
        string recruiterId
        string decision
        datetime createdAt
    }

    SCORING_PROFILES {
        string id
        float skillWeight
        float experienceWeight
        float semanticWeight
        datetime effectiveFrom
    }

    USERS ||--o{ RESUMES : owns
    USERS ||--o{ JOBS : creates
    JOBS ||--o{ MATCH_RESULTS : produces
    RESUMES ||--o{ MATCH_RESULTS : participates
    MATCH_RESULTS ||--|| FEEDBACK : has