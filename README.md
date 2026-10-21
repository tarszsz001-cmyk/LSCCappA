# LSCC App (Capacitor) — Concept A (Premium Financial: เขียวเข้ม + ทอง)

หน้าตาแอปปรับตามบอร์ด Concept A: ล็อกอิน, หน้าหลัก, บัญชี, บริการ, ขอสินเชื่อ, e-Vote, อื่นๆ
ไอคอนและแบนเนอร์ตัดมาจากบอร์ดที่ให้มา (ความละเอียดจำกัด) ถ้าจะใช้งานจริงควรขอไฟล์ต้นฉบับแทน

## แอปแยกจากเวอร์ชันเก่า
แอปนี้ใช้ package name `th.co.lscc.concepta` และชื่อ "LSCC A" ต่างจากเวอร์ชันเก่า (`th.co.lscc.app`)
จึงติดตั้งคู่กันบนเครื่องเดียวกันได้ ไม่ทับกัน

## ขั้นตอนทำ APK

ต้องมี: Node 18+, JDK 17, Android Studio (หรือ Android SDK)

1. เอา HTML ของ artifact มาวางทับ `www/index.html`
   (ถ้ามีไฟล์รูป/JS/CSS แยก ให้ใส่ใน `www/` ด้วย และอย่าอ้างลิงก์ CDN ถ้าต้องการให้ใช้ออฟไลน์)
2. `npm install`
3. `npx cap add android`
4. `npm run assets`   # สร้างไอคอน/splash จาก resources/ ลง Android
5. `npx cap sync android`
6. สร้าง APK:
   - `cd android && ./gradlew assembleDebug`
   - ได้ไฟล์ที่ `android/app/build/outputs/apk/debug/app-debug.apk`
   - หรือเปิด `npx cap open android` แล้ว Build > Build APK(s)

หมายเหตุ: ถ้าหน้าเว็บเรียก API ภายนอก (เช่น api.anthropic.com) จะใช้ไม่ได้ในแอปโดยตรง
ต้องมี backend คั่น ห้ามใส่ API key ไว้ในแอป

## หมายเหตุเวอร์ชันแอปเต็มจอ
- `www/index.html` เป็นแอปหน้าเดียวเต็มจอ (ไม่มีกรอบโทรศัพท์) สลับหน้าด้วยแถบเมนูล่าง
- ปุ่ม Back ของ Android: ปิดหน้าต่างคำนวณ > ย้อนกลับหน้าก่อนหน้า > ออกจากแอปเมื่ออยู่หน้าหลัก

## เปลี่ยนชื่อแอป/ไอคอนหลัง build ไปแล้ว
ถ้าเคยรัน `npx cap add android` ไปแล้ว ให้ลบโฟลเดอร์ `android/` แล้วทำขั้นตอน 3-6 ใหม่
(หรือแก้ชื่อที่ `android/app/src/main/res/values/strings.xml` ทั้ง app_name และ title_activity_main)
