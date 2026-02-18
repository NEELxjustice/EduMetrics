sequenceDiagram

actor Student
actor Teacher
actor Admin

participant Frontend
participant AuthController
participant AttendanceController
participant CorrectionController
participant AnalyticsController

participant AttendanceService
participant CorrectionService
participant SessionService
participant AnalyticsService
participant LateRuleEngine
participant AttendanceLockPolicy
participant AuditService
participant NotificationService

participant AttendanceRepository
participant SessionRepository
participant CorrectionRepository
participant AuditRepository
participant Database


%% =========================
%% 1️⃣ Attendance Marking Flow
%% =========================

Student ->> Frontend: Mark Attendance
Frontend ->> AttendanceController: POST /attendance/mark

AttendanceController ->> AttendanceService: markAttendance(sessionId, studentId)

AttendanceService ->> SessionService: validateSession(sessionId)
SessionService ->> SessionRepository: findById(sessionId)
SessionRepository ->> Database: query session
Database -->> SessionRepository: session

AttendanceService ->> AttendanceLockPolicy: checkLock(session)
AttendanceService ->> LateRuleEngine: evaluateLateStatus(session, currentTime)

AttendanceService ->> AttendanceRepository: save(attendance)
AttendanceRepository ->> Database: insert attendance
Database -->> AttendanceRepository: success

AttendanceService ->> AuditService: logCreation()
AuditService ->> AuditRepository: save(log)
AuditRepository ->> Database: insert audit log
Database -->> AuditRepository: success

AttendanceService -->> AttendanceController: attendanceMarked
AttendanceController -->> Frontend: Attendance marked successfully


%% =========================
%% 2️⃣ Attendance Correction Request Flow
%% =========================

Student ->> Frontend: Submit Correction Request
Frontend ->> CorrectionController: POST /attendance/correction

CorrectionController ->> CorrectionService: createRequest(attendanceId, reason)

CorrectionService ->> AttendanceRepository: findById(attendanceId)
AttendanceRepository ->> Database: query attendance
Database -->> AttendanceRepository: attendanceRecord

CorrectionService ->> CorrectionRepository: save(request)
CorrectionRepository ->> Database: insert correction request
Database -->> CorrectionRepository: success

CorrectionService ->> NotificationService: notifyTeacher()
NotificationService -->> Teacher: New correction request

CorrectionService -->> CorrectionController: requestCreated
CorrectionController -->> Frontend: Request submitted


%% =========================
%% 3️⃣ Teacher Review & Decision Flow
%% =========================

Teacher ->> Frontend: Review Correction Request
Frontend ->> CorrectionController: POST /attendance/correction/{id}/decision

CorrectionController ->> CorrectionService: processDecision(requestId, decision)

CorrectionService ->> CorrectionRepository: findById(requestId)
CorrectionRepository ->> Database: query request
Database -->> CorrectionRepository: request

CorrectionService ->> AttendanceService: applyCorrection(attendanceId, newStatus)

AttendanceService ->> AttendanceRepository: update(attendance)
AttendanceRepository ->> Database: update attendance
Database -->> AttendanceRepository: success

AttendanceService ->> AuditService: logUpdate()
AuditService ->> AuditRepository: save(log)
AuditRepository ->> Database: insert audit log
Database -->> AuditRepository: success

CorrectionService ->> CorrectionRepository: updateStatus()
CorrectionRepository ->> Database: update request
Database -->> CorrectionRepository: success

CorrectionService -->> CorrectionController: decisionProcessed
CorrectionController -->> Frontend: Decision recorded


%% =========================
%% 4️⃣ Admin Override Flow
%% =========================

Admin ->> Frontend: Override Correction Decision
Frontend ->> CorrectionController: POST /attendance/correction/{id}/override

CorrectionController ->> CorrectionService: overrideDecision(requestId)

CorrectionService ->> AttendanceService: forceApplyCorrection()
AttendanceService ->> AttendanceRepository: update(attendance)
AttendanceRepository ->> Database: update attendance
Database -->> AttendanceRepository: success

AttendanceService ->> AuditService: logOverride()
AuditService ->> AuditRepository: save(log)
AuditRepository ->> Database: insert audit log
Database -->> AuditRepository: success

CorrectionService ->> CorrectionRepository: updateStatus()
CorrectionRepository ->> Database: update request
Database -->> CorrectionRepository: success

CorrectionService -->> CorrectionController: overrideCompleted
CorrectionController -->> Frontend: Override successful


%% =========================
%% 5️⃣ Performance Analytics Flow
%% =========================

Teacher ->> Frontend: View Class Performance
Frontend ->> AnalyticsController: GET /analytics/class

AnalyticsController ->> AnalyticsService: generateClassReport()

AnalyticsService ->> AttendanceRepository: fetchAttendanceData()
AttendanceRepository ->> Database: query attendance
Database -->> AttendanceRepository: attendanceData

AnalyticsService ->> AnalyticsService: calculateAttendancePercentage()
AnalyticsService ->> AnalyticsService: calculateLateFrequency()

AnalyticsService -->> AnalyticsController: analyticsReport
AnalyticsController -->> Frontend: Display analytics