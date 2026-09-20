# Plan: จัดการข้อมูลผู้ใช้งาน

## 1. Objective
ให้ admin ดูและจัดการข้อมูลผู้ใช้ เพื่อรักษาความปลอดภัยและควบคุมสิทธิ์การใช้งานตามบทบาท

## 2. Scope
- ดูรายการผู้ใช้
- เปิด/ปิดใช้งานบัญชี
- ปรับ role ของผู้ใช้
- ตรวจสอบการเข้าถึงข้อมูล
- บันทึก audit log

## 3. Out of Scope
- User profile management แบบยืดหยุ่นเกิน MVP
- Data governance แบบกว้างเกินความจำเป็น

## 4. Dependencies
- SPEC-001 Authentication

## 5. Database Changes
- Tables:
  - users
  - roles
  - admin_audit_logs
- Columns:
  - users: id, email, role_id, status, suspended_at, updated_at
  - roles: id, name
  - admin_audit_logs: id, admin_user_id, target_user_id, action, timestamp, details
- Constraints:
  - user status enum ACTIVE|SUSPENDED|DELETED
  - role enum USER|ADMIN
- Indexes:
  - users.role_id
  - users.status

## 6. Backend Changes
- Endpoints:
  - GET /admin/users
  - PATCH /admin/users/{id}/status
  - PATCH /admin/users/{id}/role
- Validation:
  - admin-only access
  - reject unauthorized user management actions
- Business Logic:
  - support soft delete / suspend logic
  - log user state change actions

## 7. Frontend/Mobile Changes
- Screens:
  - Admin user management dashboard
- Components:
  - user table
  - status selector
  - role selector
- States:
  - loading
  - success
  - error

## 8. External Services
- none

## 9. Security
- Admin-only access
- Audit trail for each modification
- Prevent ordinary users from reading or modifying other users

## 10. Testing
- Unit Test: role and status transitions
- Integration Test: admin permission enforcement
- UI Test: user status update and denied access flow

## 11. Acceptance Criteria
- Given ผู้ดูแลระบบเข้าสู่ระบบด้วยสิทธิ์ที่เหมาะสม
- When ดูหรือปรับบทบาทผู้ใช้งาน
- Then ระบบต้องแสดงข้อมูลที่สัมพันธ์และแจ้งผลการเปลี่ยนแปลง

- Given ผู้ใช้งานทั่วไปพยายามเข้าถึงข้อมูลผู้ใช้งานคนอื่น
- When ระบบตรวจสอบสิทธิ์
- Then ระบบต้องปฏิเสธและไม่อนุญาตให้ดำเนินการ

## 12. Implementation Tasks
- [ ] Add role and status constraints
- [ ] Add admin user management APIs
- [ ] Add authorization checks
- [ ] Add admin user dashboard UI
- [ ] Add audit logging
- [ ] Write tests for admin permission and status transitions

---

