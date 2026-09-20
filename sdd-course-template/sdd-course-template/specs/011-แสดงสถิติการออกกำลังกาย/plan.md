# Plan: แสดงสถิติการออกกำลังกาย

## 1. Objective
ให้ผู้ใช้เห็นสรุปผลการออกกำลังกายแบบรวมในช่วงเวลาที่เลือก เช่น จำนวนครั้ง เวลารวม และระยะทางรวม

## 2. Scope
- สรุปจำนวนครั้ง
- สรุประยะเวลาและระยะทางรวม
- ประเมินตามช่วงเวลา week/month/all
- แจ้งเมื่อข้อมูลไม่เพียงพอ

## 3. Out of Scope
- Health analytics ขั้นสูง
- Predictive analysis

## 4. Dependencies
- SPEC-010 History

## 5. Database Changes
- Optional summary table or computed aggregation on demand
- No mandatory schema required for MVP

## 6. Backend Changes
- Endpoint:
  - GET /statistics?period=week|month|all
- Response:
  - sessionCount
  - totalDurationSeconds
  - totalDistanceMeters
- Business Logic:
  - aggregate workouts for current user by selected time range
- Validation:
  - if insufficient data, return no-data state

## 7. Frontend/Mobile Changes
- Screens:
  - Statistics dashboard
- Components:
  - stat cards
  - period selector
  - no-data state
- User Flow:
  - choose period -> show updated stats

## 8. External Services
- none

## 9. Security
- only current user’s stats are returned
- no cross-user access

## 10. Testing
- Unit Test: aggregation formulas
- API Test: empty data and valid data cases
- UI Test: period change and empty state

## 11. Acceptance Criteria
- Given ผู้ใช้งานมีประวัติการออกกำลังกาย
- When เปิดหน้าสถิติ
- Then ระบบต้องแสดงสรุปจำนวนครั้ง ระยะเวลา และระยะทางตามช่วงเวลาที่เลือก

- Given ผู้ใช้งานไม่มีข้อมูลเพียงพอ
- When เปิดหน้าสถิติ
- Then ระบบต้องแจ้งว่าข้อมูลไม่เพียงพอและแนะนำให้บันทึกกิจกรรมเพิ่มเติม

## 12. Implementation Tasks
- [ ] Add statistics query service
- [ ] Add statistics API endpoint
- [ ] Add dashboard UI components
- [ ] Add empty-data handling
- [ ] Write aggregation tests

---

