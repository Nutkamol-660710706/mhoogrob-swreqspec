# Plan: แนะนำสถานที่ออกกำลังกาย

## 1. Objective
ให้ระบบเสนอสถานที่ที่เหมาะสมที่สุดต่อผู้ใช้งานด้วยการคำนวณแบบ rule-based score โดยไม่ต้องใช้ ML ใน MVP

## 2. Scope
- คำนวณ score จากตัวชี้วัดที่กำหนด
- แสดงรายการสถานที่แนะนำ
- แสดง reason brief สำหรับแต่ละสถานที่
- ให้ไปดูรายละเอียดได้ทันที

## 3. Out of Scope
- ML recommendation แบบซับซ้อน
- Personalization advanced level

## 4. Dependencies
- SPEC-002 Search
- SPEC-003 Activity Type
- SPEC-004 Place Detail
- SPEC-005 Location

## 5. Database Changes
- No database change required for MVP
- Optional: recommendation_cache table for future optimization

## 6. Backend Changes
- Endpoint:
  - GET /recommendations
- Logic:
  - calculate recommendation score with weighted formula
  - fallback to nearby places when insufficient data
- Formula:
  - Activity Match 40%
  - Distance 30%
  - Facility Match 20%
  - Rating 10%
- Validation:
  - no real-time occupancy used in MVP
  - if no data, return nearby list with label

## 7. Frontend/Mobile Changes
- Screens:
  - Recommendation screen
- Components:
  - recommendation cards
  - reason label
  - quick detail CTA
- Empty States:
  - insufficient data
  - nearby fallback

## 8. External Services
- none beyond location service

## 9. Security
- Use only user-authorized location data
- No hidden exposure of personal profile data in recommendations

## 10. Testing
- Unit Test: score formula and fallback logic
- Integration Test: recommendation result ordering
- UI Test: recommendation screen and empty states

## 11. Acceptance Criteria
- Given ผู้ใช้งานเปิดหน้าคำแนะนำสถานที่
- When มีสถานที่ที่เหมาะสม
- Then ระบบต้องแสดงสถานที่แนะนำพร้อมเหตุผลที่สอดคล้อง

- Given ผู้ใช้งานเปลี่ยนเงื่อนไขค้นหา
- When ระบบคำนวณผลลัพธ์ใหม่
- Then รายการแนะนำต้องอัปเดตตามเงื่อนไขใหม่

## 12. Implementation Tasks
- [ ] Define recommendation score formula
- [ ] Build recommendation service
- [ ] Add recommendation API endpoint
- [ ] Add recommendation card UI
- [ ] Add fallback nearby place logic
- [ ] Write recommendation tests

---

