# Plan: แสดงพัฒนาการของผู้ใช้

## 1. Objective
ให้ผู้ใช้เห็นแนวโน้มความก้าวหน้าแบบเปรียบเทียบระหว่างช่วงเวลา เพื่อประเมินว่ามีการพัฒนาเพิ่มขึ้น/คงที่/ลดลง

## 2. Scope
- เปรียบเทียบช่วงปัจจุบันกับช่วงก่อนหน้า
- สรุปว่าผู้ใช้พัฒนาขึ้น คงที่ หรือลดลง
- แสดงภาพรวม/กราฟถ้าข้อมูลเพียงพอ

## 3. Out of Scope
- Forecasting หรือ prediction แบบ AI
- Comparisons กับผู้อื่น

## 4. Dependencies
- SPEC-011 Statistics

## 5. Database Changes
- Optional progress summary table or computed data on request
- Not required for MVP

## 6. Backend Changes
- Endpoint:
  - GET /progress?period=week|month
- Response:
  - currentValue, previousValue, deltaPercent, status
- Business Logic:
  - compare current period to previous period
  - thresholds:
    - > 5% = Improving
    - -5% ถึง 5% = Stable
    - < -5% = Declining
- Validation:
  - if data insufficient return progress not available

## 7. Frontend/Mobile Changes
- Screens:
  - Progress screen
- Components:
  - trend summary
  - trend chart
  - status indicator
- States:
  - not enough data
  - improving/stable/declining

## 8. External Services
- none

## 9. Security
- Only current user’s progress data is shown

## 10. Testing
- Unit Test: threshold logic
- Integration Test: previous-vs-current period comparison
- UI Test: improving/stable/declining states

## 11. Acceptance Criteria
- Given ผู้ใช้งานมีประวัติที่เพียงพอ
- When เปิดหน้าพัฒนาการ
- Then ระบบต้องแสดงแนวโน้มและสรุปว่าผู้ใช้งานมีความก้าวหน้าเพิ่มขึ้น/คงที่/ลดลง

- Given ข้อมูลไม่เพียงพอ
- When เปิดหน้าพัฒนาการ
- Then ระบบต้องแจ้งว่าข้อมูลไม่เพียงพอสำหรับการแสดงพัฒนาการ

## 12. Implementation Tasks
- [ ] Create progress calculation service
- [ ] Add progress API endpoint
- [ ] Add trend chart UI
- [ ] Add classification logic for improving/stable/declining
- [ ] Add insufficient-data state
- [ ] Write tests for progress logic

---

