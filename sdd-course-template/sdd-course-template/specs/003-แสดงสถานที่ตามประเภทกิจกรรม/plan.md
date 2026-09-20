# Plan: แสดงสถานที่ตามประเภทกิจกรรม

## 1. Objective
ให้ผู้ใช้เลือกประเภทกิจกรรมแล้วแสดงเฉพาะสถานที่ที่ตรงกับประเภทนั้นอย่างรวดเร็วและชัดเจน

## 2. Scope
- เลือกประเภทกิจกรรม
- แสดงสถานที่ที่เกี่ยวข้อง
- เรียงลำดับตามความเกี่ยวข้อง
- แสดงจำนวนสถานที่ที่พบ
- แจ้งเมื่อไม่มีสถานที่ที่ตรง

## 3. Out of Scope
- การคัดเลือกจากข้อมูล real-time ของผู้ใช้
- Recommendation แบบลึกเกิน MVP

## 4. Dependencies
- SPEC-002 Search
- SPEC-014 Place management

## 5. Database Changes
- Tables:
  - activity_types
  - place_activity_types
- Columns:
  - activity_types: id, name, slug
  - place_activity_types: place_id, activity_type_id
- Constraints:
  - activity type เป็น master data
  - unique combination of place_id + activity_type_id
- Indexes:
  - activity_types.slug
  - place_activity_types.activity_type_id

## 6. Backend Changes
- Endpoints:
  - GET /activity-types
  - GET /places?activityType=...
- Logic:
  - select by activity type
  - allow multi-select activity OR logic
  - show count summary for each type
- Validation:
  - reject unknown activity type
  - return empty result state if no matching places

## 7. Frontend/Mobile Changes
- Components:
  - activity filter cards
  - result list grouped by selected types
- State:
  - selected activity list
  - loading and empty results
- User Flow:
  - ผู้ใช้เลือก activity -> list updates instantly

## 8. External Services
- ไม่ใช้ภายนอก

## 9. Security
- Read-only access for normal users
- Admin only for CRUD of activity type master data

## 10. Testing
- Unit Test: mapping and count logic
- API Test: valid and invalid activityType values
- UI Test: empty state, multi-select behavior

## 11. Acceptance Criteria
- Given ผู้ใช้งานเลือกประเภทกิจกรรม
- When เปิดหน้า filter ตามประเภท
- Then ระบบต้องแสดงเฉพาะสถานที่ที่มีประเภทนั้นเท่านั้น

- Given ไม่มีสถานที่สำหรับประเภทที่เลือก
- When ผู้ใช้งานเลือกประเภทดังกล่าว
- Then ระบบต้องแจ้งว่าไม่มีสถานที่และให้ลองใหม่

## 12. Implementation Tasks
- [ ] Create activity type master data
- [ ] Create place_activity_types mapping table
- [ ] Create category-based query service
- [ ] Add API for activity types and filtered places
- [ ] Add activity category UI
- [ ] Add empty state and retry flow
- [ ] Write tests for selection and no-match logic

---

