# Plan: แสดงรายละเอียดสถานที่

## 1. Objective
ให้ผู้ใช้ดูข้อมูลเชิงรายละเอียดของสถานที่ที่เลือกเพื่อประกอบการตัดสินใจเดินทางและวางแผนออกกำลังกาย

## 2. Scope
- แสดงชื่อ, ประเภท, ที่อยู่, เวลาเปิด-ปิด
- แสดงสิ่งอำนวยความสะดวก
- แสดงข้อมูลสำคัญ เช่น ระยะทางและสภาพแวดล้อม
- แสดงสถานะเมื่อไม่มีข้อมูลบางส่วน

## 3. Out of Scope
- Place admin management
- Booking, payment, reservation

## 4. Dependencies
- SPEC-002 Search
- SPEC-014 Place management

## 5. Database Changes
- Tables:
  - places
  - place_amenities
  - place_images
- Relationships:
  - place -> many amenities
  - place -> many images
- Columns:
  - places: id, name, address, latitude, longitude, description, phone, open_hours, rating
- Constraints:
  - required fields: name, address, latitude, longitude, activity type

## 6. Backend Changes
- Endpoint:
  - GET /places/{id}
- Response:
  - place summary, facilities, open hours, rating, distance, image links
- Validation:
  - show placeholder instead of crashing when optional data is absent
  - return 404 for missing place
- Business Logic:
  - aggregate activity type and amenities from master data

## 7. Frontend/Mobile Changes
- Screens:
  - Place detail screen
- Components:
  - image carousel
  - summary card
  - facilities list
  - hours section
  - map/direction CTA
- States:
  - loading
  - empty/missing info
  - error for invalid place id

## 8. External Services
- Optional map/direction provider
- No required external service for the basic detail screen

## 9. Security
- Read-only access for users
- Validate place id and permissions
- Prevent leaking internal admin-only data

## 10. Testing
- Unit Test: place detail serialization and missing field handling
- API Test: valid and invalid place id
- UI Test: missing optional data placeholder

## 11. Acceptance Criteria
- Given ผู้ใช้งานเลือกสถานที่จากรายการ
- When เปิดดูรายละเอียด
- Then ระบบต้องแสดงชื่อ, ที่อยู่, และเวลาเปิด-ปิดอย่างครบถ้วน

- Given ข้อมูลสิ่งอำนวยความสะดวกบางรายการไม่มีข้อมูล
- When เปิดรายละเอียดสถานที่
- Then ระบบต้องแสดงข้อความว่าไม่มีข้อมูลหรือสถานะที่ชัดเจน

## 12. Implementation Tasks
- [ ] Create place detail query model
- [ ] Add place detail API
- [ ] Add facility and hours aggregation logic
- [ ] Add detail UI screen
- [ ] Add missing-data placeholders
- [ ] Add error handling
- [ ] Write tests for detail rendering

---

