# Class Diagram – Major Backend Classes

## User (abstract)
- id
- name
- email
- role

Methods:
- getRole()

## Student extends User
- rollNumber
- batchId

## Teacher extends User
- department

## Admin extends User

## Session
- id
- courseId
- teacherId
- startTime
- endTime

## Attendance
- id
- sessionId
- studentId
- status (PRESENT, LATE, ABSENT)
- markedAt

## AttendanceCorrectionRequest
- id
- attendanceId
- studentId
- reason
- status
- reviewedBy
- decisionAt

## Assignment
- id
- courseId
- createdBy
- dueDate

## Submission
- id
- assignmentId
- studentId
- submittedAt
- marks

## Service Layer

AttendanceService
- markAttendance()
- applyCorrection()
- calculateAttendanceStats()

CorrectionService
- createRequest()
- processDecision()
- overrideDecision()

AssignmentService
- createAssignment()
- evaluateSubmission()

AnalyticsService
- generateStudentReport()
- generateClassReport()

## Repository Layer

UserRepository
SessionRepository
AttendanceRepository
CorrectionRepository
AssignmentRepository
SubmissionRepository

## Utility / Domain Services

LateRuleEngine
AttendanceLockPolicy
AuditService
NotificationService