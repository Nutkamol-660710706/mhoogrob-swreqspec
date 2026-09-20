# Plan: สมัครสมาชิกและเข้าสู่ระบบ

## 1. Objective
สร้างระบบลงทะเบียนและเข้าสู่ระบบเพื่อให้ผู้ใช้สามารถเข้าถึงฟีเจอร์ที่ต้องใช้บัญชีได้อย่างปลอดภัยและครบถ้วนใน MVP

## 2. Scope
- สมัครสมาชิกด้วยข้อมูลพื้นฐาน
- ตรวจสอบความถูกต้องของข้อมูล
- สร้างบัญชีผู้ใช้ใหม่
- เข้าสู่ระบบด้วยอีเมล/รหัสผ่าน
- เก็บ session หรือ token
- ออกจากระบบ

## 3. Out of Scope
- ลืมรหัสผ่าน / รีเซ็ตรหัสผ่าน
- MFA
- ผู้ใช้หลายรายมี roles อื่นนอกจาก USER และ ADMIN

## 4. Dependencies
- ไม่มี dependency หลัก

## 5. Database Changes
- Tables:
  - users
  - roles
  - user_sessions
- Columns:
  - users: id, email, password_hash, full_name, role_id, status, created_at, updated_at
  - roles: id, name
  - user_sessions: id, user_id, token, expires_at, created_at
- Constraints:
  - email เป็น unique
  - role default เป็น USER
  - password ต้องเก็บแบบ hash ไม่เก็บ plaintext
- Indexes:
  - users.email
  - user_sessions.user_id

## 6. Backend Changes
- Endpoints:
  - POST /auth/register
  - POST /auth/login
  - POST /auth/logout
  - GET /auth/me
- Request/Response:
  - register: email, password, confirm_password, name
  - login: email, password
  - response: user summary + token/session
- Validation:
  - email format ถูกต้อง
  - password มีความยาว/รูปแบบตามเงื่อนไขที่ตกลง
  - duplicate email ตรงเงื่อนไข reject
- Error Handling:
  - 400 invalid payload
  - 409 duplicate user
  - 401 invalid credentials
  - 403 forbidden when session invalid

## 7. Frontend/Mobile Changes
- Screens:
  - Register screen
  - Login screen
  - Account locked / retry later screen
- States:
  - loading
  - success
  - validation error
  - auth error
- User Flow:
  - ผู้ใช้กรอกข้อมูล -> validate -> submit -> success or error

## 8. External Services
- ไม่ใช้ภายนอกใน MVP

## 9. Security
- HTTPS เท่านั้น
- รหัสผ่านเก็บด้วย bcrypt/argon2
- session/token มี expiry
- ตรวจสอบ role ก่อนอนุญาตเข้าถึงข้อมูลที่ต้องมีสิทธิ์
- จำกัดข้อมูลที่ส่งคืนจาก auth API

## 10. Testing
- Unit Test: validation rules, password hashing, token creation
- Integration Test: register/login/logout flow
- API Test: invalid email, duplicate email, wrong password
- UI Test: error states, lockout state

## 11. Acceptance Criteria
- Given ผู้ใช้งานเปิดหน้าสมัครสมาชิก
- When กรอกข้อมูลครบถ้วนและถูกต้อง
- Then ระบบต้องสร้างบัญชีใหม่และแจ้งความสำเร็จ

- Given ผู้ใช้งานมีบัญชีที่ถูกต้อง
- When เข้าสู่ระบบด้วยอีเมลและรหัสผ่านที่ตรงกัน
- Then ระบบต้องอนุญาตให้เข้าสู่ระบบและสร้าง session

- Given ผู้ใช้งานกรอกข้อมูลซ้ำหรือไม่ถูกต้อง
- When ส่งฟอร์ม
- Then ระบบต้องปฏิเสธและแสดงข้อผิดพลาดที่ชัดเจน

## 12. Implementation Tasks
- [ ] Create user and role tables
- [ ] Create auth service and password hashing
- [ ] Create register/login/logout APIs
- [ ] Add validation and lockout logic
- [ ] Add login/register UI screens
- [ ] Add auth state management
- [ ] Add error and empty states
- [ ] Write tests for auth flow

---

