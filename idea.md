# Digital Attendance & Performance Monitoring Platform

## Problem Statement
Institutes and training centers struggle with maintaining reliable attendance records, managing late entries, handling correction requests, and tracking student performance in a centralized and auditable system.

Existing solutions are either manual or lack proper approval workflows and analytics.

## Project Objective
Build a full-stack system where students, teachers, and administrators can manage session-based attendance, assignment performance, and approval workflows with proper business rules.

Backend reliability, structure, and system design are the primary focus.

## Scope

The system supports:
- Session-based attendance
- Late entry rules
- Attendance correction requests
- Multi-level approval workflow
- Assignment and marks tracking
- Performance analytics dashboards

## Actors
- Student
- Teacher
- Admin

## Key Features

### Authentication & Roles
- Student, Teacher, Admin roles
- Role-based access control

### Attendance Management
- Session-based attendance marking
- Automatic late marking based on session start time
- Lock attendance after configurable cutoff time

### Attendance Correction Workflow
- Student submits correction request
- Teacher reviews and approves/rejects
- Admin can override decisions
- Full audit history maintained

### Assignment & Performance
- Teacher creates assignments
- Students submit assignments
- Teachers assign marks
- Performance aggregation per student and class

### Analytics
- Attendance percentage
- Late entry frequency
- Performance trends
- Class-wise and subject-wise summaries

## Out of Scope
- Online exams
- Video conferencing
- Proctoring

## Tech Stack

Frontend:
- React

Backend:
- Node.js
- Express
- MongoDB (Mongoose)

Architecture:
- Controller – Service – Repository pattern
- REST APIs

Design Principles
- SOLID principles
- Clean architecture
- Proper separation of concerns
- Reusable domain services

## Success Criteria
- Proper approval workflow
- Correct rule enforcement for late entries
- Clean backend architecture
- Easily extensible for future academic modules