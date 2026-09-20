# Plan: จัดการข้อมูลสถานที่

## 1. Objective
ให้ admin จัดการข้อมูลสถานที่เพื่อให้ข้อมูลอยู่ในสถานะที่ถูกต้อง ครบถ้วน และสามารถใช้งานได้อย่างสม่ำเสมอ

## 2. Scope
- เพิ่มสถานที่ใหม่
- แก้ไขรายละเอียดสถานที่
- ปิดใช้งาน / archive สถานที่
- จัดการสิ่งอำนวยความสะดวกและประเภทกิจกรรม
- เก็บ audit log

## 3. Out of Scope
- Booking, payment
- User management

## 4. Dependencies
- SPEC-014 depends on shared place data model
- Supports SPEC-002 to SPEC-007

## 5. Database Changes
- Tables:
  - places
  - place_activity_types
  - place_amenities
  - admin_audit_logs
- Columns:
  - places: id, name, address, latitude, longitude, status, created_by, updated_by, deleted_at
  - admin_audit_logs: id, user_id, action, target_type, target_id, timestamp, details
- Constraints:
  - status enum ACTIVE|INACTIVE|ARCHIVED
  - soft delete only
- Indexes:
  - places.status
  - admin_audit_logs.user_id

## 6. Backend Changes
- Endpoints:
  - GET /admin/places
  - POST /admin/places
  - PATCH /admin/places/{id}
  - DELETE /admin/places/{id} (soft delete)
- Validation:
  - required fields check before save
  - validate coordinate and activity mapping
- Business Logic:
  - active/inactive/archive states
  - audit logs for each modification

## 7. Frontend/Mobile Changes
- Screens:
  - Admin place dashboard
  - Admin place form
- Components:
  - place table/list
  - status actions
  - form validation
- States:
  - loading
  - success
  - error

## 8. External Services
- none required

## 9. Security
- Admin-only access
- Audit trail for all changes
- Validation before allow update

## 10. Testing
- Unit Test: required fields and status transitions
- Integration Test: create/edit/archive place
- UI Test: admin dashboard actions

## 11. Acceptance Criteria
- Given ผู้ดูแลระบบเข้าสู่ระบบด้วยสิทธิ์ที่เหมาะสม
- When เพิ่มหรือแก้ไขข้อมูลสถานที่
- Then ระบบต้องบันทึกข้อมูลและตรวจสอบความถูกต้องก่อนยืนยัน

- Given ผู้ดูแลระบบต้องการลบหรือปิดใช้งานสถานที่
- When ยืนยันการเปลี่ยนแปลง
- Then ระบบต้องอัปเดตสถานะและแจ้งผลการดำเนินการ

## 12. Implementation Tasks
- [ ] Create place and audit table schema
- [ ] Add admin place API endpoints
- [ ] Add place status logic (active/inactive/archive)
- [ ] Add admin dashboard UI
- [ ] Add soft-delete implementation
- [ ] Add audit logging for place management
- [ ] Write tests for CRUD and status transitions

---

