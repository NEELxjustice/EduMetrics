# Use Case Diagram – Digital Attendance & Performance Monitoring Platform

## Actors

1. Student
2. Teacher
3. Admin

## Student Use Cases
- Register / Login
- View assigned sessions
- Mark attendance (auto captured)
- View attendance history
- Submit attendance correction request
- Submit assignments
- View marks and performance analytics

## Teacher Use Cases
- Create academic sessions
- Mark attendance for a session
- View and edit attendance before lock
- Review correction requests
- Approve / Reject correction requests
- Create assignments
- Evaluate assignments
- View class analytics

## Admin Use Cases
- Manage users
- Manage courses / batches
- Configure late entry rules
- Configure attendance lock rules
- Override attendance decisions
- View institute-level analytics
- Audit attendance changes

## Relationships

Student -> Attendance, Assignment, Performance
Teacher -> Sessions, Attendance, Corrections, Assignments
Admin -> Configuration, Audit, Overrides