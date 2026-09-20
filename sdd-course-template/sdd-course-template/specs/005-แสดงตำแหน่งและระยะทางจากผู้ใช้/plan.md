# Plan: แสดงตำแหน่งและระยะทางจากผู้ใช้

## 1. Objective
ระบุตำแหน่งผู้ใช้และคำนวณระยะทางจากตำแหน่งปัจจุบันไปยังสถานที่ เพื่อช่วยตัดสินใจเลือกสถานที่ที่เหมาะสม

## 2. Scope
- ขอสิทธิ์เข้าถึงพิกัดผู้ใช้
- คำนวณระยะทางจาก GPS หรือ manual location
- แสดงระยะทางในผลการค้นหาและหน้า detail
- แจ้งเมื่อไม่สามารถระบุตำแหน่งได้

## 3. Out of Scope
- Real-time navigation แบบละเอียด
- การคำนวณหลายเส้นทาง

## 4. Dependencies
- SPEC-002 Search
- SPEC-014 Place management

## 5. Database Changes
- Tables:
  - user_locations
  - place_locations
- Columns:
  - user_locations: user_id, latitude, longitude, source, updated_at
  - place_locations: place_id, latitude, longitude
- Constraints:
  - lat/lng must be valid coordinates
- Indexes:
  - user_locations.user_id
  - place_locations.place_id

## 6. Backend Changes
- Endpoints:
  - GET /places/nearby?lat=&lng=
  - POST /users/location/manual
- Business Logic:
  - calculate distance via geospatial formula
  - store distance in meters
  - return distance label in m or km format
- Validation:
  - reject invalid coordinates
  - fallback to manual location when GPS unavailable

## 7. Frontend/Mobile Changes
- Components:
  - permission request banner
  - manual location picker
  - distance display chips
- User Flow:
  - permission prompt -> accept or choose manual location -> search results show distance

## 8. External Services
- Device GPS or browser geolocation

## 9. Security
- Request location only when needed
- Protect location data from unauthorized access
- Ensure user consent before access

## 10. Testing
- Unit Test: distance conversion logic
- Integration Test: GPS allowed / denied
- UI Test: manual location fallback

## 11. Acceptance Criteria
- Given ผู้ใช้งานอนุญาตให้เข้าถึงตำแหน่ง
- When ระบบแสดงรายการสถานที่
- Then ระบบต้องแสดงระยะทางจากตำแหน่งของผู้ใช้งานถึงแต่ละสถานที่

- Given ผู้ใช้งานไม่อนุญาตให้เข้าถึงตำแหน่ง
- When เปิดหน้า search หรือ detail
- Then ระบบต้องแจ้งให้เปิดการเข้าถึงตำแหน่งหรือเลือกพื้นที่ด้วยตนเอง

## 12. Implementation Tasks
- [ ] Create location tables and validation
- [ ] Add distance calculation service
- [ ] Add GPS permission handling
- [ ] Add manual location fallback UI
- [ ] Add location-aware API response
- [ ] Add frontend display for distance labels
- [ ] Write tests for GPS and fallback

---

