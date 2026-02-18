@startuml
left to right direction

actor Student
actor Teacher
actor Admin

Student --> (Login)
Student --> (Mark Attendance)
Student --> (View Attendance History)
Student --> (Submit Correction Request)
Student --> (Submit Assignment)
Student --> (View Performance Analytics)

Teacher --> (Create Session)
Teacher --> (Mark Session Attendance)
Teacher --> (Review Correction Request)
Teacher --> (Approve / Reject Correction)
Teacher --> (Create Assignment)
Teacher --> (Evaluate Assignment)
Teacher --> (View Class Analytics)

Admin --> (Manage Users)
Admin --> (Configure Late Rules)
Admin --> (Configure Attendance Lock Rules)
Admin --> (Override Attendance Decision)
Admin --> (View Institute Analytics)
Admin --> (View Audit Logs)

@enduml