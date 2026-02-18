# Use Case Diagram – Digital Attendance & Performance Monitoring Platform

```mermaid
flowchart LR

Student[Student]
Teacher[Teacher]
Admin[Admin]

subgraph System[Digital Attendance & Performance Monitoring Platform]

    UC1((Login))
    UC2((Mark Session Attendance))
    UC3((View Attendance))
    UC4((Request Attendance Correction))
    UC5((Approve / Reject Correction))
    UC6((Create Session))
    UC7((Create Assignment))
    UC8((Submit Assignment))
    UC9((Grade Assignment))
    UC10((View Performance Analytics))
    UC11((Track Participation))
    UC12((Manage Late Entry Rules))
    UC13((Manage Users))

end

Student --> UC1
Student --> UC3
Student --> UC4
Student --> UC8
Student --> UC10

Teacher --> UC1
Teacher --> UC2
Teacher --> UC6
Teacher --> UC7
Teacher --> UC9
Teacher --> UC5
Teacher --> UC10
Teacher --> UC11

Admin --> UC5
Admin --> UC12
Admin --> UC13
Admin --> UC10