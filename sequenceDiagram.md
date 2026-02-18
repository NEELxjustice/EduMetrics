
---

# ✅ sequenceDiagram.md  
(Main end-to-end flow: session attendance → late rule → correction → approval → analytics)

```md
# Sequence Diagram – Attendance & Performance Flow

```mermaid
sequenceDiagram
    autonumber

    actor Student
    actor Teacher
    actor Admin

    participant UI as Frontend
    participant API as Backend API
    participant AttendanceSvc as Attendance Service
    participant RuleSvc as Late Rule Engine
    participant WorkflowSvc as Correction Workflow
    participant AnalyticsSvc as Analytics Service
    participant DB as Database

    %% Session attendance
    Teacher ->> UI: Start session & mark attendance
    UI ->> API: POST /sessions/{id}/attendance
    API ->> AttendanceSvc: markAttendance()

    AttendanceSvc ->> RuleSvc: applyLateEntryRules()
    RuleSvc -->> AttendanceSvc: late / present

    AttendanceSvc ->> DB: save attendance records
    API -->> UI: attendance marked

    %% Student requests correction
    Student ->> UI: Request attendance correction
    UI ->> API: POST /attendance/correction
    API ->> WorkflowSvc: createCorrectionRequest()
    WorkflowSvc ->> DB: store request
    API -->> UI: request submitted

    %% Teacher approval
    Teacher ->> UI: Review correction
    UI ->> API: POST /corrections/{id}/approve
    API ->> WorkflowSvc: processApproval()
    WorkflowSvc ->> DB: update approval step

    %% Admin approval (if required)
    Admin ->> UI: Final approval
    UI ->> API: POST /corrections/{id}/final-approve
    API ->> WorkflowSvc: finalizeRequest()
    WorkflowSvc ->> DB: update attendance record

    %% Analytics
    Teacher ->> UI: View class performance
    UI ->> API: GET /analytics/class
    API ->> AnalyticsSvc: generateClassReport()
    AnalyticsSvc ->> DB: fetch attendance, marks, participation
    AnalyticsSvc -->> API: report
    API -->> UI: dashboard data