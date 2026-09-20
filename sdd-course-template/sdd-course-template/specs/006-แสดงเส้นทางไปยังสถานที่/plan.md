# Plan: แสดงเส้นทางไปยังสถานที่

## 1. Objective
แสดงเส้นทางจากผู้ใช้ไปยังสถานที่เลือก พร้อมระยะทางและเวลาโดยประมาณ เพื่อช่วยในการเดินทาง

## 2. Scope
- แสดง route จากตำแหน่งปัจจุบัน/ที่เลือกไปยังสถานที่
- แสดงระยะทางและเวลาโดยประมาณ
- เปิดแผนที่ภายนอกเมื่อผู้ใช้ต้องการนำทางแบบ turn-by-turn

## 3. Out of Scope
- การคำนวณเส้นทางแบบหลายจุด/หลายเส้นทาง
- การจัดเก็บประวัติการนำทาง

## 4. Dependencies
- SPEC-005 User Position and Distance
- SPEC-014 Place management

## 5. Database Changes
- No database change required for basic MVP
- Optional: route_requests log table for debugging/analysis

## 6. Backend Changes
- Endpoint:
  - GET /places/{id}/route
- Request:
  - originLat, originLng, mode = walking|driving
- Response:
  - route summary, eta, distance, external map link
- Validation:
  - if no origin, request manual location before route
- Business Logic:
  - app shows route data
  - external map handles turn-by-turn navigation

## 7. Frontend/Mobile Changes
- Screens:
  - Route screen
- Components:
  - mode selector (walking/driving)
  - map card
  - ETA card
  - open external map button
- States:
  - route loading
  - no location available

## 8. External Services
- External map provider for route and navigation

## 9. Security
- Only use user location when consent is granted
- Route requests should not expose extra user metadata

## 10. Testing
- Unit Test: response formatting and ETA logic
- API Test: no location / invalid coords
- UI Test: route screen and external-link flow

## 11. Acceptance Criteria
- Given ผู้ใช้งานเลือกสถานที่
- When เปิดหน้า route
- Then ระบบต้องแสดงเส้นทางและระยะทางหรือเวลาโดยประมาณ

- Given ระบบไม่สามารถระบุตำแหน่งได้
- When ผู้ใช้งานต้องการดู route
- Then ระบบต้องให้กำหนดจุดเริ่มต้นหรือเลือกตำแหน่งด้วยตนเอง

## 12. Implementation Tasks
- [ ] Add route estimation API
- [ ] Integrate external map provider
- [ ] Add route screen UI
- [ ] Add mode selection for walking/driving
- [ ] Add no-location fallback
- [ ] Add tests for route failure and route success

---

