# แหล่ง/องค์กร ส่งเสริมการเรียนรู้ อำเภอเทิง

ทำเนียบแหล่งเรียนรู้ แหล่งส่งเสริมการอ่าน ภาคีเครือข่าย และภูมิปัญญาท้องถิ่น
ของ สกร.ระดับอำเภอเทิง จังหวัดเชียงราย แยกตามปีงบประมาณ พ.ศ.
เก็บข้อมูลไว้ใน Firebase (Firestore) ครูเข้าสู่ระบบแล้วแก้ไขได้จากหน้าเว็บโดยตรง

## ไฟล์ใน repository นี้
| ไฟล์ | ใช้ทำอะไร |
|---|---|
| `index.html` | หน้าเว็บ |
| `firebase-config.js` | ค่าการเชื่อมต่อ Firebase (ต้องแก้ตามขั้นตอนที่ 2) |
| `firestore.rules` | กฎสิทธิ์ของฐานข้อมูล (คัดลอกไปวางในขั้นตอนที่ 4) |

> ไฟล์ `setup.html` มีเบอร์โทรครู **ห้ามอัปโหลดขึ้น GitHub**

## ตั้งค่าครั้งแรก (ประมาณ 15 นาที)

**1. สร้างโปรเจกต์ Firebase**
เข้า https://console.firebase.google.com → Add project → ตั้งชื่อ เช่น `thoeng-learning` → ปิด Google Analytics ได้ → Create

**2. สร้าง Web app แล้วคัดลอกค่า config**
หน้า Project overview → กดไอคอน `</>` (Web) → ตั้งชื่อ → Register app
จะเห็น `const firebaseConfig = { apiKey: "...", ... }`
(ใส่ค่าในไฟล์ `firebase-config.js` เรียบร้อยแล้ว)

**3. เปิดการเข้าสู่ระบบด้วยอีเมล/รหัสผ่าน**
Build → Authentication → Get started → Sign-in method → Email/Password → Enable → Save

**4. สร้างฐานข้อมูลและวางกฎสิทธิ์**
Build → Firestore Database → Create database → เลือก location `asia-southeast1 (Singapore)` → Start in **production mode** → Create
จากนั้นแท็บ Rules → ลบของเดิม → วางเนื้อหาจากไฟล์ `firestore.rules` ทั้งหมด → Publish

**5. สร้างบัญชีครู**
เปิดไฟล์ `setup.html` ด้วย Chrome (ดับเบิลคลิก) → กด "สร้างบัญชีทั้งหมด" → รอจนขึ้น "เสร็จแล้ว 24 จาก 24 บัญชี"

**6. (แนะนำ) ปิดการสมัครบัญชีใหม่**
Authentication → Settings → User actions → เอาเครื่องหมายออกที่ "Enable create (sign-up)" → Save

**7. อัปโหลดขึ้น GitHub และเปิด GitHub Pages**
อัปโหลด `index.html`, `firebase-config.js`, `firestore.rules`, `README.md` ขึ้น repository
Settings → Pages → Deploy from a branch → `main` / `(root)` → Save → รอ 1–2 นาที

**8. อนุญาตโดเมน GitHub ใน Firebase**
Authentication → Settings → Authorized domains → Add domain → ใส่ `<ชื่อบัญชี>.github.io`

## การใช้งาน
- ทุกคนเปิดดู ค้นหา และดาวน์โหลด PDF ได้โดยไม่ต้องเข้าสู่ระบบ
- กด "เข้าสู่ระบบเพื่อแก้ไข" → ชื่อผู้ใช้ = ชื่อจริง (เช่น `วีนัส`) · รหัสผ่าน = เบอร์โทรศัพท์
- ครั้งแรกที่ฐานข้อมูลยังว่าง หน้าเว็บจะแสดงข้อมูลปี 2569 ที่ฝังในไฟล์ เมื่อมีคนบันทึกครั้งแรก ข้อมูลจะถูกเก็บขึ้น Firebase
- ระบบจำการเข้าสู่ระบบเฉพาะแท็บที่เปิดอยู่ ปิดแท็บแล้วต้องเข้าสู่ระบบใหม่
- ถ้าครูเปลี่ยนเบอร์โทร: Firebase → Authentication → Users → เลือกบัญชี (t01 = ลำดับ 1 ในไฟล์บุคลากร) → Reset password
- เพิ่มครูใหม่: แจ้งผู้ดูแลให้เพิ่มชื่อในหน้าเว็บ บัญชี Firebase และกฎใน firestore.rules
