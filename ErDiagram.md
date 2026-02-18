# ER Diagram – Digital Attendance & Performance Platform

## users
- _id
- name
- email
- passwordHash
- role
- rollNumber
- department
- batchId

## sessions
- _id
- courseId
- teacherId (FK -> users)
- startTime
- endTime

## attendance
- _id
- sessionId (FK -> sessions)
- studentId (FK -> users)
- status
- markedAt

## attendance_corrections
- _id
- attendanceId (FK -> attendance)
- studentId (FK -> users)
- reason
- status
- reviewedBy (FK -> users)
- decisionAt

## assignments
- _id
- courseId
- createdBy (FK -> users)
- dueDate

## submissions
- _id
- assignmentId (FK -> assignments)
- studentId (FK -> users)
- submittedAt
- marks

## audit_logs
- _id
- entityType
- entityId
- action
- performedBy (FK -> users)
- timestamp

## Relationships

users (Teacher) 1 -> N sessions
users (Student) 1 -> N attendance
sessions 1 -> N attendance
attendance 1 -> 0..1 attendance_corrections
assignments 1 -> N submissions
users 1 -> N submissions
users 1 -> N audit_logs