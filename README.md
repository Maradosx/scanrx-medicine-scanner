# ScanRx · เครื่องอ่านฉลากยาอัจฉริยะ

> Web app อ่านฉลากยาด้วย AI สำหรับ **ผู้พิการทางสายตา ผู้สูงอายุ และคนทั่วไป**
> ใช้ Google Gemini Vision + Web Speech API · ทำงานเต็มรูปแบบในเบราว์เซอร์ ไม่ต้องติดตั้งอะไร

---

## ✨ Features

### 📷 สแกนฉลากยา — 2 ทาง
- **กล้องสด** — เปิด webcam ส่องฉลาก กดปุ่ม SCAN
- **อัพโหลดรูป** — กดปุ่ม / ลากวาง / Ctrl+V จาก clipboard

### 🤖 อ่านด้วย Gemini Vision (ภาษาไทย + อังกฤษ)
สกัดข้อมูล 14 ฟิลด์อัตโนมัติ:
- ชื่อทางการค้า / ชื่อสามัญ
- ขนาด / วิธีใช้ / สรรพคุณ / คำเตือน
- วันหมดอายุ / วันผลิต / เลข Lot
- **เลขทะเบียน อย.** / **Barcode** / **QR Code** (ผ่าน jsQR)
- ตัวเลขทุกตัวบนฉลาก
- ผู้ผลิต

### 💬 AI Chat ถามต่อได้
- Quick chips 8 คำถามที่พบบ่อย ("ผลข้างเคียง?" "ห้ามทานพร้อมอะไร?" ฯลฯ)
- **Voice input** — กดไมค์พูดภาษาไทย (Web Speech API)
- AI ตอบ + อ่านออกเสียงอัตโนมัติ
- Multi-turn conversation รักษา context

### ♿ Accessibility-First
- อ่านออกเสียงภาษาไทย (Thai TTS) อัตโนมัติทุกผลลัพธ์
- ปุ่มใหญ่ contrast สูง
- Keyboard shortcuts: `SPACE` สแกน · `U` อัพโหลด · `V` อ่านซ้ำ · `S` บันทึก · `R` รีเซ็ต
- รองรับ screen reader (ARIA labels)

### 📚 ประวัติการสแกน
- เก็บ 12 รายการล่าสุดใน localStorage
- คลิกเพื่อดูซ้ำ + ถาม AI ต่อได้

---

## 🚀 เริ่มใช้งาน (3 ขั้น)

### 1. ขอ Gemini API Key (ฟรี)
1. เข้า [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
2. Sign in ด้วย Google Account
3. กด **Create API key** → คัดลอกคีย์ที่ขึ้นต้นด้วย `AIzaSy...`

> 💡 ดูคู่มือทีละขั้นพร้อมภาพได้ที่ [`api-key-guide.html`](api-key-guide.html)

### 2. เปิด ScanRx
ดับเบิ้ลคลิก [`medicine-scanner.html`](medicine-scanner.html) เพื่อเปิดในเบราว์เซอร์
(ใช้ได้กับ Chrome / Edge / Safari / Firefox)

### 3. ใส่ API Key ครั้งแรก
1. กดปุ่ม **API Key** มุมขวาบน (สีแดง "ยังไม่ตั้ง")
2. วางคีย์ลงในช่อง → กด **บันทึก**
3. คีย์เก็บใน localStorage ของเบราว์เซอร์เท่านั้น — ไม่ส่งออกที่อื่น

---

## 📂 โครงสร้างโปรเจกต์

```
Coding/
├── medicine-scanner.html   # แอปหลัก
├── api-key-guide.html      # คู่มือขอ API key
├── README.md               # ไฟล์นี้
└── .gitignore
```

ทุกไฟล์เป็น **single-file** — HTML/CSS/JS รวมในไฟล์เดียว ไม่ต้อง build

---

## 🛠️ เทคโนโลยีที่ใช้

| | |
|---|---|
| **OCR / Vision** | [Google Gemini 2.0 Flash](https://ai.google.dev/) (REST API) |
| **QR decode** | [jsQR](https://github.com/cozmo/jsQR) (client-side) |
| **Voice TTS** | Web Speech API · `speechSynthesis` |
| **Voice STT** | Web Speech API · `SpeechRecognition` |
| **Camera** | `MediaDevices.getUserMedia()` |
| **Fonts** | Fraunces (display) · IBM Plex Sans Thai · JetBrains Mono |
| **Design** | Pharmaceutical Editorial · zero CSS framework |

---

## ⌨️ Keyboard Shortcuts

| ปุ่ม | ทำงาน |
|---|---|
| `SPACE` | สแกนทันที |
| `U` | เปิดหน้าเลือกไฟล์ |
| `V` | อ่านผลออกเสียง |
| `S` | บันทึกประวัติ |
| `R` | รีเซ็ต |
| `Ctrl/Cmd + V` | วางรูปจาก clipboard |
| `ESC` | ปิด modal |

---

## 🔒 ความเป็นส่วนตัว

- **API key เก็บใน localStorage** ของเบราว์เซอร์เท่านั้น ไม่ commit ขึ้น repo
- **ภาพฉลากยา** ส่งตรงไปยัง Google Gemini API เพื่อวิเคราะห์เท่านั้น
- **ไม่มี backend / server** ของเรา ไม่เก็บ log การใช้งาน
- **ประวัติการสแกน** เก็บใน localStorage บนเครื่องคุณเท่านั้น
- อ่านนโยบาย Gemini ได้ที่ [ai.google.dev/gemini-api/terms](https://ai.google.dev/gemini-api/terms)

---

## 🌐 Browser Support

| Browser | Camera | Upload | TTS (เสียงไทย) | STT (พูดภาษาไทย) |
|---|---|---|---|---|
| Chrome (Mac/Win/Android) | ✅ | ✅ | ✅ | ✅ |
| Edge | ✅ | ✅ | ✅ | ✅ |
| Safari (Mac/iOS) | ✅ | ✅ | ✅ | ⚠️ บางเวอร์ชัน |
| Firefox | ✅ | ✅ | ⚠️ ขึ้นกับ OS | ❌ |

แนะนำ **Chrome หรือ Edge** เพื่อประสบการณ์ที่สมบูรณ์ที่สุด

---

## 🎯 กลุ่มผู้ใช้เป้าหมาย

โปรเจกต์นี้ออกแบบเพื่อช่วย **5 หมวดผู้พิการ** ที่ระบุในระบบสวัสดิการของไทย:

- 👁️ **ทางสายตา** — voice readout + voice chat + auto-speak ทุก response
- 👂 **ทางการได้ยิน** — ผลลัพธ์เป็นตัวอักษรขนาดใหญ่ ชัดเจน
- 🦽 **ทางร่างกาย** — voice input ใน chat (ไม่ต้องพิมพ์)
- 🧠 **ทางสติปัญญา/การเรียนรู้** — AI chat อธิบายเพิ่มเติม คำถามสำเร็จรูป
- 🧓 **ผู้สูงอายุ** — UI ใหญ่ contrast สูง รองรับทุกข้อข้างต้น

---

## 📝 License

MIT — ใช้/แก้ไข/แจกจ่ายได้อย่างเสรี

---

## 🙏 Credits

- AI by [Google Gemini](https://ai.google.dev/)
- QR by [jsQR](https://github.com/cozmo/jsQR)
- Fonts by [Google Fonts](https://fonts.google.com/)

🤖 พัฒนาด้วยความช่วยเหลือจาก Claude (Anthropic)
