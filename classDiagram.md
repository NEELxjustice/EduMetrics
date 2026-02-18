# Class Diagram – Digital Attendance & Performance Monitoring Platform

```mermaid
classDiagram

%% =========================
%% Core Users
%% =========================

class User {
  +String id
  +String email
  +String passwordHash
  +String role
}

class Student
class Teacher
class Admin

User <|-- Student
User <|-- Teacher
User <|-- Admin


%% =========================
%% Academic Structure
%% =========================

class Course {
  +String id
  +String name
  +String description
}

class Session {
  +String id
  +Date sessionDate
  +Time startTime
  +Time endTime
  +String status
}

Teacher "1" --> "0..*" Course
Course "1" --> "0..*" Session


%% =========================
%% Attendance
%% =========================

class AttendanceRecord {
  +String id
  +String studentId
  +String sessionId
  +DateTime markedAt
  +String status
  +Boolean lateEntry
}

Student "1" --> "0..*" AttendanceRecord
Session "1" --> "0..*" AttendanceRecord


%% =========================
%% Late Entry Rules
%% =========================

class LateEntryRule {
  +String id
  +int allowedMinutes
  +Boolean autoMarkLate
  +Boolean blockAfterLimit
}

Session --> LateEntryRule


%% =========================
%% Attendance Correction Workflow
%% =========================

class AttendanceCorrectionRequest {
  +String id
  +String attendanceId
  +String studentId
  +String reason
  +String status
  +Date createdAt
}

class ApprovalStep {
  +String id
  +String requestId
  +String approverId
  +String decision
  +DateTime actionTime
}

AttendanceRecord "1" --> "0..*" AttendanceCorrectionRequest
AttendanceCorrectionRequest "1" --> "1..*" ApprovalStep
Teacher --> ApprovalStep
Admin --> ApprovalStep


%% =========================
%% Assignments & Marks
%% =========================

class Assignment {
  +String id
  +String courseId
  +String title
  +Date dueDate
  +int maxMarks
}

class Submission {
  +String id
  +String assignmentId
  +String studentId
  +Date submittedAt
}

class Mark {
  +String id
  +String submissionId
  +int score
  +String feedback
}

Course "1" --> "0..*" Assignment
Assignment "1" --> "0..*" Submission
Submission "1" --> "0..1" Mark
Student --> Submission


%% =========================
%% Participation Tracking
%% =========================

class ParticipationRecord {
  +String id
  +String studentId
  +String sessionId
  +int interactionCount
  +float participationScore
}

Student --> ParticipationRecord
Session --> ParticipationRecord


%% =========================
%% Performance & Analytics
%% =========================

class PerformanceReport {
  +String id
  +String studentId
  +float attendanceRate
  +float averageMarks
  +float participationScore
  +Date generatedAt
}

Student "1" --> "0..*" PerformanceReport


%% =========================
%% Application Layer
%% =========================

class StudentController {
  +viewAttendance()
  +viewPerformance()
  +submitCorrectionRequest()
}

class TeacherController {
  +markAttendance()
  +publishAssignment()
  +approveCorrection()
  +viewClassAnalytics()
}

class AdminController {
  +manageUsers()
  +manageRules()
  +monitorSystem()
}


%% =========================
%% Service Layer
%% =========================

class AttendanceService {
  +markAttendance()
  +applyLateRules()
}

class CorrectionWorkflowService {
  +createRequest()
  +processApproval()
}

class AssignmentService {
  +createAssignment()
  +gradeSubmission()
}

class ParticipationService {
  +trackParticipation()
}

class AnalyticsService {
  +generateStudentReport()
  +generateClassReport()
}


%% =========================
%% Repository Layer
%% =========================

class AttendanceRepository
class CorrectionRepository
class AssignmentRepository
class SubmissionRepository
class PerformanceRepository
class UserRepository


%% =========================
%% Dependencies
%% =========================

StudentController --> AttendanceService
StudentController --> AnalyticsService
StudentController --> CorrectionWorkflowService

TeacherController --> AttendanceService
TeacherController --> AssignmentService
TeacherController --> CorrectionWorkflowService
TeacherController --> AnalyticsService

AdminController --> UserRepository
AdminController --> AttendanceService

AttendanceService --> AttendanceRepository
AttendanceService --> LateEntryRule

CorrectionWorkflowService --> CorrectionRepository
CorrectionWorkflowService --> ApprovalStep

AssignmentService --> AssignmentRepository
AssignmentService --> SubmissionRepository

ParticipationService --> ParticipationRecord

AnalyticsService --> PerformanceRepository
AnalyticsService --> AttendanceRepository
AnalyticsService --> SubmissionRepository
