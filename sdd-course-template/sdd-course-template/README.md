# <ชื่อระบบของทีม>

รายวิชา 520461-165 Software Requirement Specification and Management | ภาคการศึกษาที่ 1/2569

## ทีม
| ชื่อ | รหัส | บทบาท |
|------|------|--------|
|      |      |        |

## โครง repo (อย่าย้าย specs/ ออกจาก root)
| โฟลเดอร์ | มีไว้ทำอะไร | ใครอ่าน |
|----------|-------------|---------|
| docs/srs/ | SRS ทั้งเล่ม + diagram ทุกภาพ + RTM | คน |
| specs/ | spec.md ทีละฟีเจอร์ (1 โฟลเดอร์ = 1 ฟีเจอร์) | เครื่องมือ AI และคน |
| specs/000-shared/ | data model และ glossary ที่หลายฟีเจอร์ใช้ร่วม | ทุก spec อ้างถึง |
| specs/README.md | ดัชนี: UC-xx <-> โฟลเดอร์ NNN | สถานะ | ผู้รับผิดชอบ | ทุกคน |
| frontend/ | React + Vite (สร้างสัปดาห์หน้า) | AI สร้าง คนตรวจ |
| backend/ | Python FastAPI (สร้างสัปดาห์หน้า) | AI สร้าง คนตรวจ |
| docs/prompt-log/ | บันทึก prompt และคำถามที่ AI ถามกลับ ตามกติการายวิชา | ผู้สอน |
| CLAUDE.md, .github/copilot-instructions.md, .cursor/rules/ | กติกาให้ AI agent อ่านก่อนทำงาน (เนื้อหาเดียวกัน 3 ไฟล์) | AI |

## วิธีเริ่ม (สัปดาห์นี้ ทำบนเว็บ GitHub ได้ทั้งหมด)
1. อัปโหลด SRS (.pdf หรือ .docx) และ diagram เข้า docs/srs/ และ docs/srs/diagrams/
2. เปลี่ยนชื่อโฟลเดอร์ specs/001-feature/ เป็นชื่อฟีเจอร์ เช่น specs/001-booking/
3. กรอก specs/001-.../spec.md และ traceability.md
4. เติมแถวของฟีเจอร์ใน specs/README.md
5. ส่งลิงก์ repo นี้ในระบบส่งงาน

## สัปดาห์หน้า
ให้ AI (Claude Code / Copilot / Cursor) อ่าน specs/001-.../spec.md แล้วถามกลับ ปรับเป็น v2 จากนั้น plan และสร้าง prototype ใน frontend/ และ backend/
