# Digital Attendance & Performance Monitoring Platform

## 1. Problem Statement

Educational institutes and training centres still rely on manual or partially automated systems to track student attendance and academic performance.  
These systems fail to capture:

- real-time, session-based attendance
- late entry handling
- correction and approval workflows
- participation tracking
- unified performance analytics

This leads to inaccurate attendance records, manual reconciliation work for teachers, and limited visibility into student performance trends.

The goal of this project is to build a full-stack Digital Attendance and Performance Monitoring Platform with strong backend design that supports real academic workflows and approval pipelines.

---

## 2. Objective

To design and implement a scalable backend-centric platform that allows institutes to:

- record real-time session-based attendance
- automatically apply late-entry rules
- manage attendance correction requests with multi-level approvals
- track student participation
- manage assignments and marks
- generate performance analytics for students and classes

---

## 3. Target Users

- Students
- Teachers
- Academic administrators

---

## 4. System Scope

This system covers the complete academic activity lifecycle of a class:

- user authentication and role-based access
- session creation and management
- attendance marking and late entry detection
- attendance correction and approval workflow
- participation tracking per session
- assignment creation, submission and grading
- performance reporting and analytics

The project focuses primarily on backend architecture, workflows and data integrity.

---

## 5. Core Functional Modules

### 5.1 Authentication & Role Management

- Student, Teacher and Admin login
- Role-based access control for all APIs

---

### 5.2 Session-Based Attendance

- Teachers create class sessions
- Teachers mark attendance for each session
- Attendance is recorded per student per session

---

### 5.3 Late Entry Rules Engine

- Configurable late-entry rules per institute
- Automatic classification of:
  - Present
  - Late
  - Absent
- Support for blocking attendance after a defined time window

---

### 5.4 Attendance Correction Workflow

- Students can raise attendance correction requests
- Each request contains:
  - affected attendance record
  - justification
- Multi-step approval pipeline:
  - teacher approval
  - optional admin approval
- Automatic update of attendance record after final approval

---

### 5.5 Participation Tracking

- Participation is tracked per student per session
- Stores interaction count and derived participation score
- Used as an input for performance analytics

---

### 5.6 Assignment and Marks Management

- Teachers create assignments per course
- Students submit assignments
- Teachers evaluate submissions and assign marks
- Feedback is stored with marks

---

### 5.7 Performance Analytics

- Student-level performance reports
- Class-level analytics for teachers
- Metrics include:
  - attendance rate
  - average marks
  - participation score
  - trends over time

---

## 6. Non-Trivial Backend Logic

This project intentionally includes complex backend workflows:

### Late Entry Rules Engine
- dynamic rule evaluation during attendance marking
- automatic late detection based on session start time

### Attendance Correction Pipeline
- state-based workflow for correction requests
- multiple approval steps
- audit trail of approvals

### Approval Pipeline
- role-based approval routing
- conditional escalation to admin
- transactional updates to attendance records

### Analytics Aggregation
- multi-table aggregation
- time-based and course-based metrics

---

## 7. Backend Architecture

The backend follows a layered and maintainable architecture:

- Controllers – API layer
- Services – business logic and workflows
- Repositories – data access layer
- Domain models – core entities
- Rule and workflow services – late entry rules and approval pipelines

Structure follows:

Controller → Service → Repository

---

## 8. Software Engineering Practices

The backend design explicitly applies:

- Encapsulation through service and repository layers
- Abstraction through domain-oriented interfaces
- Inheritance for user roles (Student, Teacher, Admin)
- Polymorphism in rule evaluation and approval workflows

Design patterns are used where suitable, such as:

- Strategy pattern for late-entry rule evaluation
- State-like handling for correction request workflow

---

## 9. Technology Stack

Frontend:
- React

Backend:
- Node.js
- Express.js

Database:
- MongoDB

Authentication:
- JWT based authentication

---

## 10. Deliverables

The GitHub repository contains:

- idea.md – project description and scope
- useCaseDiagram.md – use case diagram
- sequenceDiagram.md – end-to-end workflow diagram
- classDiagram.md – class design and architecture
- ErDiagram.md – database design

---