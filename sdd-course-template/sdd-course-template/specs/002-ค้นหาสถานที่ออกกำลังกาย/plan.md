# Plan: ค้นหาสถานที่ออกกำลังกาย

## 1. Objective
ให้ผู้ใช้ค้นหา gym ที่ต้องการตาม keyword, ประเภทกิจกรรม, สิ่งอำนวยความสะดวก, พื้นที่, และระยะทาง

## 2. Scope
- ค้นหาด้วยคำค้นหา
- ค้นหาตามตำแหน่ง/พื้นที่ใกล้เคียง
- กรองตามประเภทและสิ่งอำนวยความสะดวก
- แสดงรายการผลลัพธ์พร้อมลำดับความเกี่ยวข้อง
- แจ้งเมื่อไม่พบผลลัพธ์

## 3. Out of Scope
- Recommendation engine แบบซับซ้อน
- Booking / payment
- Search analytics ขั้นสูง

## 4. Dependencies
- SPEC-001 Authentication
- SPEC-014 Place management

## 5. Database Changes
- Tables:
  - places
  - place_locations
  - place_activity_types
  - place_amenities
- Relationships:
  - places to place_locations: one-to-one
  - places to activity types: many-to-many
  - places to amenities: many-to-many
- Indexes:
  - place_locations.lat/lng
  - places.name
  - place_activity_types.activity_type_id

## 6. Backend Changes
- Endpoints:
  - GET /places/search
  - GET /places/nearby
- Request:
  - keyword, activityType, facilityIds, radiusKm, lat, lng, manualLocation
- Response:
  - list of places with id, name, distance, rating, activity types, amenities
- Validation:
  - empty keyword allowed only if filters exist
  - radius bounded within supported range
  - location fallback when GPS unavailable
- Business Logic:
  - multiple filters use AND
  - multiple activity types use OR
  - default radius = 5 km
  - fallback to nearby list if query empty

## 7. Frontend/Mobile Changes
- Screens:
  - Search screen
  - Filter panel
  - Nearby result list
- States:
  - loading
  - empty result
  - no-location fallback
  - retry
- User Flow:
  - ผู้ใช้กรอกคำค้นหา/เลือก filter -> ดึงผล -> แสดง card รายการ -> คลิกดูรายละเอียด

## 8. External Services
- Geolocation provider (browser/GPS)
- Optional map service for center/region selection

## 9. Security
- Authentication required for personalized search if needed
- Validate request params
- Do not expose internal coordinates if not needed

## 10. Testing
- Unit Test: filter combinator logic, radius validation
- Integration Test: search with keyword and filters
- API Test: no-result, invalid radius, location fallback
- UI Test: empty state and retry action

## 11. Acceptance Criteria
- Given ผู้ใช้งานอยู่ในหน้าค้นหา
- When ใส่คำค้นหา หรือเลือก filter
- Then ระบบต้องแสดงสถานที่ที่ตรงกับเงื่อนไข

- Given ผู้ใช้งานไม่มี location หรือไม่สามารถระบุตำแหน่งได้
- When เริ่มค้นหา
- Then ระบบต้องแจ้งสถานะและให้เลือกตำแหน่งด้วยตนเองหรือปรับเงื่อนไข

## 12. Implementation Tasks
- [ ] Create place and location tables
- [ ] Create search service and query builder
- [ ] Add filter validation and radius logic
- [ ] Create search API endpoints
- [ ] Add search UI and filter controls
- [ ] Add empty and error states
- [ ] Add fallback manual location flow
- [ ] Write tests for search scenarios

---

