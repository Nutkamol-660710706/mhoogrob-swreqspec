# Plan: กำหนดเป้าหมายการออกกำลังกาย

## 1. Objective
ให้ผู้ใช้ตั้งเป้าหมายการออกกำลังกายและติดตามความคืบหน้าอย่างต่อเนื่อง

## 2. Scope
- สร้างเป้าหมายใหม่
- ดูสถานะเป้าหมาย
- ปรับเป้าหมายได้
- แจ้งเมื่อเป้าหมายสำเร็จหรือเกินกำหนด

## 3. Out of Scope
- Automated workout plan generation
- Health coach advice

## 4. Dependencies
- SPEC-001 Authentication

## 5. Database Changes
- Tables:
  - goals
- Columns:
  - id, user_id, type, target_value, unit, start_date, end_date, status
- Constraints:
  - type must be distance|duration|frequency
  - status must be NOT_STARTED|IN_PROGRESS|ACHIEVED|OVERDUE
- Indexes:
  - goals.user_id
  - goals.status

## 6. Backend Changes
- Endpoints:
  - GET /goals
  - POST /goals
  - PATCH /goals/{id}
- Validation:
  - target value > 0
  - end_date must be after start_date
- Business Logic:
  - progress calculated based on actual workout data
  - status updated automatically based on completion and date

## 7. Frontend/Mobile Changes
- Screens:
  - Goal list screen
  - Create/edit goal modal or form
- Components:
  - goal cards
  - progress bar
  - overdue banner
- States:
  - not started
  - in progress
  - achieved
  - overdue

## 8. External Services
- none

## 9. Security
- user sees only own goals
- admin route not required for MVP

## 10. Testing
- Unit Test: status calculation and validation
- Integration Test: create and update goal
- UI Test: progress-state rendering

## 11. Acceptance Criteria
- Given ผู้ใช้งานเข้าสู่ระบบ
- When กำหนดเป้าหมายการออกกำลังกาย
- Then ระบบต้องบันทึกเป้าหมายและแสดงในรายชื่อเป้าหมายของผู้ใช้งาน

- Given เป้าหมายมีข้อมูลประวัติเพื่อวัดความคืบหน้า
- When ผู้ใช้งานเปิดหน้าเป้าหมาย
- Then ระบบต้องแสดงสถานะความคืบหน้าและแจ้งเมื่อเป้าหมายสำเร็จหรือเกินกำหนด

## 12. Implementation Tasks
- [ ] Create goals table and domain model
- [ ] Add goal API endpoints
- [ ] Add progress calculation logic
- [ ] Add goal management UI
- [ ] Add status state handling
- [ ] Write tests for goal creation and status transitions

---

