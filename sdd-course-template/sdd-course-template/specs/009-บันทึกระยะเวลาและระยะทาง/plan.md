# Plan: บันทึกระยะเวลาและระยะทาง

## 1. Objective
ให้ผู้ใช้เพิ่มข้อมูลระยะเวลาและระยะทางให้กับ workout เพื่อใช้ในการประวัติและสถิติ

## 2. Scope
- บันทึกระยะเวลาในการออกกำลังกาย
- บันทึกระยะทางที่เคลื่อนที่ไปได้
- ตรวจสอบข้อมูลว่าถูกต้องหรือไม่

## 3. Out of Scope
- วิเคราะห์ความเร็วหรือพลังงานแบบละเอียด
- เชื่อมกับ sensor ภายนอกแบบเต็ม

## 4. Dependencies
- SPEC-008 Workout

## 5. Database Changes
- Tables:
  - workouts
- Columns to update:
  - duration_seconds
  - distance_meters
- Constraints:
  - duration_seconds >= 0
  - distance_meters >= 0
  - max reasonable duration limit enforced
- Indexes:
  - workouts.user_id, started_at

## 6. Backend Changes
- Endpoint:
  - PATCH /workouts/{id}/metrics
- Request:
  - durationSeconds, distanceMeters
- Response:
  - updated workout summary
- Business Logic:
  - duration stored in seconds
  - distance stored in meters
  - invalid negative or unrealistic values rejected

## 7. Frontend/Mobile Changes
- Components:
  - duration input
  - distance input
  - validation banner
- User Flow:
  - กรอกค่า -> validate -> save -> show summary

## 8. External Services
- none

## 9. Security
- Only owner of workout can update metrics
- Validate ranges before persistence

## 10. Testing
- Unit Test: duration/distance validation
- API Test: negative value rejection
- UI Test: invalid value message

## 11. Acceptance Criteria
- Given ผู้ใช้งานบันทึกกิจกรรม
- When กรอกระยะเวลาและระยะทาง
- Then ระบบต้องบันทึกค่าเหล่านั้นพร้อมกับกิจกรรมที่เลือก

- Given ผู้ใช้งานกรอกค่าที่ไม่ถูกต้อง
- When ส่งข้อมูล
- Then ระบบต้องปฏิเสธและแสดงข้อผิดพลาด

## 12. Implementation Tasks
- [ ] Extend workout model with metrics fields
- [ ] Add validation logic for duration and distance
- [ ] Add metrics update API
- [ ] Add frontend form fields and validation
- [ ] Add tests for valid and invalid metric input

---

