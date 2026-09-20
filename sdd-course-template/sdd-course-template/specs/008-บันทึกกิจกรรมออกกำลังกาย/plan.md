# Plan: บันทึกกิจกรรมออกกำลังกาย

## 1. Objective
ให้ผู้ใช้บันทึกกิจกรรมการออกกำลังกายที่ทำไปแล้วเพื่อดูประวัติและติดตามความก้าวหน้า

## 2. Scope
- บันทึกประเภทกิจกรรม
- ระบุวันที่และเวลา
- บันทึกสถานที่ (optional)
- แจ้งผลสำเร็จ/ข้อผิดพลาด

## 3. Out of Scope
- Auto-generated workout plan
- Advanced workout analysis

## 4. Dependencies
- SPEC-001 Authentication
- SPEC-007 Recommendation

## 5. Database Changes
- Tables:
  - workouts
  - workout_activity_types
- Columns:
  - workouts: id, user_id, activity_type_id, place_id, started_at, duration_seconds, distance_meters, notes
  - workout_activity_types: id, name
- Constraints:
  - user_id required
  - activity_type_id required
  - place_id optional
- Indexes:
  - workouts.user_id
  - workouts.started_at

## 6. Backend Changes
- Endpoint:
  - POST /workouts
- Request:
  - activityType, startTime, placeId optional, notes optional
- Response:
  - workout summary and created record id
- Validation:
  - reject incomplete record
  - validate date/time format

## 7. Frontend/Mobile Changes
- Screens:
  - Add Workout screen
- Components:
  - activity selector
  - date/time picker
  - optional place selector
  - notes field
- States:
  - success banner
  - validation error

## 8. External Services
- none required

## 9. Security
- user can only create/update own records
- validate payload before save

## 10. Testing
- Unit Test: payload validation
- API Test: successful create and failed create
- UI Test: workout form and validation

## 11. Acceptance Criteria
- Given ผู้ใช้งานเข้าสู่ระบบและเลือกบันทึกกิจกรรม
- When กรอกข้อมูลและบันทึก
- Then ระบบต้องบันทึกกิจกรรมและยืนยันความสำเร็จ

- Given ผู้ใช้งานส่งข้อมูลไม่ครบหรือไม่ถูกต้อง
- When บันทึกกิจกรรม
- Then ระบบต้องปฏิเสธและแจ้งให้กรอกข้อมูลใหม่

## 12. Implementation Tasks
- [ ] Create workout tables and activity type master data
- [ ] Add workout create API
- [ ] Add validation service
- [ ] Build workout form UI
- [ ] Add success and error states
- [ ] Add tests for valid and invalid workout submission

---

