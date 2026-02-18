
---

# ✅ ErDiagram.md

```md
# ER Diagram – Digital Attendance & Performance Monitoring Platform

```mermaid
erDiagram

    USERS {
        string id
        string email
        string passwordHash
        string role
    }

    COURSES {
        string id
        string name
        string description
        string teacherId
    }

    SESSIONS {
        string id
        string courseId
        datetime sessionDate
        string status
    }

    ATTENDANCE_RECORDS {
        string id
        string studentId
        string sessionId
        datetime markedAt
        string status
        boolean lateEntry
    }

    LATE_ENTRY_RULES {
        string id
        int allowedMinutes
        boolean autoMarkLate
        boolean blockAfterLimit
    }

    ATTENDANCE_CORRECTION_REQUESTS {
        string id
        string attendanceId
        string studentId
        string reason
        string status
        datetime createdAt
    }

    APPROVAL_STEPS {
        string id
        string requestId
        string approverId
        string decision
        datetime actionTime
    }

    ASSIGNMENTS {
        string id
        string courseId
        string title
        datetime dueDate
        int maxMarks
    }

    SUBMISSIONS {
        string id
        string assignmentId
        string studentId
        datetime submittedAt
    }

    MARKS {
        string id
        string submissionId
        int score
        string feedback
    }

    PARTICIPATION_RECORDS {
        string id
        string studentId
        string sessionId
        int interactionCount
        float participationScore
    }

    PERFORMANCE_REPORTS {
        string id
        string studentId
        float attendanceRate
        float averageMarks
        float participationScore
        datetime generatedAt
    }

    USERS ||--o{ COURSES : teaches
    COURSES ||--o{ SESSIONS : has
    USERS ||--o{ ATTENDANCE_RECORDS : marks
    SESSIONS ||--o{ ATTENDANCE_RECORDS : contains

    ATTENDANCE_RECORDS ||--o{ ATTENDANCE_CORRECTION_REQUESTS : has
    ATTENDANCE_CORRECTION_REQUESTS ||--o{ APPROVAL_STEPS : includes

    COURSES ||--o{ ASSIGNMENTS : contains
    ASSIGNMENTS ||--o{ SUBMISSIONS : receives
    SUBMISSIONS ||--|| MARKS : results_in

    USERS ||--o{ PARTICIPATION_RECORDS : generates
    USERS ||--o{ PERFORMANCE_REPORTS : has