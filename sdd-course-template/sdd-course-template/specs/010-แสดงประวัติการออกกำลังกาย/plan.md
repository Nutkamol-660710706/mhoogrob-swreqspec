# Plan: แสดงประวัติการออกกำลังกาย

## 1. Objective
ให้ผู้ใช้ดูประวัติการออกกำลังกายย้อนหลังแบบเรียงลำดับเวลา เพื่อประเมินความก้าวหน้าและดูกิจกรรมที่ผ่านมา

## 2. Scope
- แสดงรายการ workout ที่บันทึกแล้ว
- แสดงวันที่, เวลา, ประเภท, สถานที่, ระยะเวลา, ระยะทาง
- จัดเรียงจากล่าสุดก่อน
- ให้เลือกช่วงเวลา เช่น 7/30/90/All

## 3. Out of Scope
- Machine analysis แบบละเอียด
- Analytics dashboard แบบเดียวกันกับ statistics

## 4. Dependencies
- SPEC-008 Workout
- SPEC-009 Duration and Distance

## 5. Database Changes
- No new table required beyond workouts and lookup tables
- Optional: history view materialization for performance

## 6. Backend Changes
- Endpoint:
  - GET /workouts?range=7|30|90|all
- Response:
  - workouts list with summary fields
- Validation:
  - user can only access own history
  - range default = 30 days
- Sorting:
  - newest first

## 7. Frontend/Mobile Changes
- Screens:
  - History screen
- Components:
  - filter chips for 7/30/90/all
  - workout cards
  - empty state
- States:
  - loading
  - empty
  - pagination/infinite scroll

## 8. External Services
- none

## 9. Security
- Require auth
- Ensure only own workout history is shown

## 10. Testing
- API Test: valid range filtering and ownership checks
- UI Test: empty state and ordering

## 11. Acceptance Criteria
- Given ผู้ใช้งานมีประวัติการออกกำลังกาย
- When เปิดหน้าประวัติ
- Then ระบบต้องแสดงรายการเรียงตามเวลาจากล่าสุดก่อน และมีข้อมูลที่เกี่ยวข้องครบถ้วน

- Given ผู้ใช้งานยังไม่มีประวัติ
- When เปิดหน้า history
- Then ระบบต้องแจ้งว่าหาไม่พบข้อมูลประวัติ

## 12. Implementation Tasks
- [ ] Add workout history query API
- [ ] Add range filter logic
- [ ] Add history list UI
- [ ] Add empty state
- [ ] Add sorting and pagination/infinite scroll
- [ ] Write tests for ownership and ordering

---

