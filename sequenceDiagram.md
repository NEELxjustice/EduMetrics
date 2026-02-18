# Sequence Diagram – Attendance and Correction Workflow

## Main Flow – Attendance Marking

Student -> Frontend:
Request to mark attendance

Frontend -> API Gateway:
POST /attendance/mark

API Gateway -> AttendanceController:
markAttendance()

AttendanceController -> AttendanceService:
validateSessionAndTime()

AttendanceService -> SessionRepository:
getSessionDetails()

AttendanceService:
checkLateRule()

AttendanceService -> AttendanceRepository:
saveAttendance()

AttendanceService -> AuditService:
logAttendanceCreation()

AttendanceController -> Frontend:
attendance marked response


## Correction Request Flow

Student -> Frontend:
Submit correction request

Frontend -> API:
POST /attendance/correction-request

CorrectionController -> CorrectionService:
createRequest()

CorrectionService -> AttendanceRepository:
validateOriginalRecord()

CorrectionService -> CorrectionRepository:
saveRequest()

CorrectionService -> NotificationService:
notifyTeacher()

Teacher -> Frontend:
Review request

Frontend -> API:
POST /attendance/correction/{id}/decision

CorrectionController -> CorrectionService:
processDecision()

CorrectionService:
validateTeacherAuthority()

CorrectionService -> AttendanceService:
applyCorrection()

AttendanceService -> AttendanceRepository:
updateAttendance()

AttendanceService -> AuditService:
logAttendanceChange()

CorrectionService -> CorrectionRepository:
updateStatus()

Admin Override (optional):

Admin -> API:
POST /attendance/correction/{id}/override

CorrectionService:
forceApplyCorrection()