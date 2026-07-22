# 🌤️ Weather App

เว็บแอปพยากรณ์อากาศแบบ Full-Stack ที่ผู้ใช้สามารถค้นหาสภาพอากาศปัจจุบันของเมืองใดก็ได้ทั่วโลก ผ่านหน้าเว็บที่เชื่อมต่อกับ Backend API แบบ Real-time พร้อม**ระบบสมัครสมาชิก/เข้าสู่ระบบ**

เป็นส่วนหนึ่งของการเรียนรู้ **DevOps และ Cloud Engineering** — โปรเจกต์นี้เน้นการเชื่อมต่อ Frontend และ Backend ที่ Deploy แยกกันคนละ Cloud Platform เข้าด้วยกัน รวมถึงการทำระบบ Authentication แบบ End-to-End

🔗 **Live Demo:** [weather-jsllbndd5-jirawatdonbantao1.vercel.app](https://weather-app-two-nu-24.vercel.app/)

---

## 📖 เกี่ยวกับโปรเจกต์นี้

Weather App เป็นโปรเจกต์ Full-Stack ที่ฝึกการทำงานร่วมกันระหว่าง:

- **Frontend** ที่ Deploy บน Vercel (2 หน้า: เช็คอากาศ + เข้าสู่ระบบ/สมัครสมาชิก)
- **Backend API** ที่ Deploy บน Railway (คนละ Domain กัน)
- **External API** (WeatherAPI.com) สำหรับดึงข้อมูลอากาศจริง

จุดสำคัญของโปรเจกต์นี้:
- การแก้ปัญหา **CORS** ที่เกิดขึ้นเมื่อ Frontend และ Backend อยู่คนละ Domain กัน
- การเชื่อมต่อระบบ **JWT Authentication** จาก Backend เข้ากับหน้าเว็บจริง
- การเก็บสถานะ Login ด้วย `localStorage` และแสดงผลแบบไดนามิกตามสถานะผู้ใช้

---

## 🛠️ Tech Stack

| เทคโนโลยี | ใช้ทำอะไร |
|---|---|
| **HTML / CSS / JavaScript** | Frontend UI |
| **Fetch API** | เรียกข้อมูลจาก Backend แบบ Asynchronous |
| **localStorage** | เก็บ JWT Token และชื่อผู้ใช้ฝั่ง Browser หลัง Login |
| **Vercel** | Cloud Platform สำหรับ Deploy Frontend |
| **Node.js + Express** | Backend API (Repo แยก: [myfirstapi](https://github.com/JirawatDonbantao/myfirstapi)) |
| **Railway** | Cloud Platform สำหรับ Deploy Backend |
| **WeatherAPI.com** | แหล่งข้อมูลสภาพอากาศจริง |
| **CORS** | อนุญาตการเรียก API ข้าม Domain |

---

## ✨ Features

### หน้าเช็คอากาศ (`index.html`)
- 🔍 ค้นหาสภาพอากาศตามชื่อเมืองได้ทั่วโลก
- 🌡️ แสดงอุณหภูมิจริงและอุณหภูมิที่รู้สึกได้ (Feels Like)
- 💧 แสดงความชื้นในอากาศ
- 🌬️ แสดงความเร็วลม
- 🎨 ไอคอนสภาพอากาศแบบไดนามิกตามสถานการณ์จริง
- ⚡ รองรับการกด Enter เพื่อค้นหา
- 🎯 แสดง Error ที่ชัดเจนเมื่อพิมพ์ชื่อเมืองผิดหรือไม่พบข้อมูล
- 🕐 แสดงประวัติการค้นหาล่าสุดแบบ Clickable Chips
- 📱 ออกแบบ UI แบบ Responsive และทันสมัย (Glassmorphism style)

### หน้าเข้าสู่ระบบ (`login.html`)
- 👤 สมัครสมาชิกและเข้าสู่ระบบในหน้าเดียวกัน (สลับโหมดได้)
- 🔐 ส่งข้อมูลไปยัง Backend เพื่อ Hash Password และรับ JWT Token
- 💾 บันทึก Token ไว้ใน `localStorage` เพื่อใช้งานต่อในหน้าเช็คอากาศ

### ระบบ Authentication ที่เชื่อมทั้ง 2 หน้า
- แถบด้านบนแสดงสถานะ Login (ชื่อผู้ใช้ / ปุ่มเข้าสู่ระบบ-ออกจากระบบ)
- หากเข้าสู่ระบบแล้ว การค้นหาอากาศจะถูกบันทึกประวัติผูกกับผู้ใช้คนนั้นในฐานข้อมูล
- หากไม่ได้เข้าสู่ระบบ ยังสามารถค้นหาอากาศได้ตามปกติ (Login แบบไม่บังคับ)

---

## 🏗️ Architecture

```
ผู้ใช้ (Browser)
      │
      ├──▶ login.html ──▶ Railway (/register, /login) ──▶ PostgreSQL (users)
      │         │
      │    JWT Token เก็บใน localStorage
      │         │
      ▼         ▼
   index.html (แนบ Token ถ้ามี)
      │
      │  fetch() ─── CORS enabled
      ▼
Railway — Backend API (Node.js/Express)
myfirstapi-production-40f1.up.railway.app/weather/:city
      │
      ├──▶ WeatherAPI.com — External Data Source
      └──▶ PostgreSQL — search_history (ผูกกับ user_id ถ้า Login)
```

**จุดสำคัญ:** Frontend และ Backend Deploy แยกกันคนละ Platform และคนละ Domain โดยสิ้นเชิง จึงต้องเปิดใช้งาน CORS ฝั่ง Backend เพื่อให้ Browser อนุญาตการเรียกข้ามโดเมนได้ รวมถึงต้องตั้งค่า `FRONTEND_URL` ฝั่ง Backend ให้ตรงกับ Domain จริงของหน้านี้

---

## 🚀 Getting Started (รันโปรเจกต์นี้เอง)

### สิ่งที่ต้องมีก่อน
- Backend API ต้องรันอยู่แล้ว (ดูที่ [myfirstapi](https://github.com/JirawatDonbantao/myfirstapi))
- เบราว์เซอร์ทั่วไป (ไม่ต้องติดตั้งอะไรเพิ่มสำหรับ Frontend)

### ขั้นตอน

```bash
# Clone โปรเจกต์
git clone https://github.com/JirawatDonbantao/weather-app.git
cd weather-app
```

เปิดไฟล์ `index.html` และ `login.html` แล้วแก้ตัวแปร `API_URL` ให้ชี้ไปที่ Backend ของคุณ:

```javascript
const API_URL = 'https://your-backend-url.up.railway.app'
```

จากนั้นเปิดไฟล์ `index.html` ในเบราว์เซอร์ได้เลย (ดับเบิลคลิก หรือใช้ VS Code Live Server) — เข้า `login.html` ก่อนเพื่อสมัครสมาชิก/เข้าสู่ระบบ แล้วจะถูกพาไปหน้า `index.html` อัตโนมัติ

---

## 📚 สิ่งที่ได้เรียนรู้จากโปรเจกต์นี้

- ความแตกต่างระหว่างเว็บแบบ Static และ Dynamic
- การแยก Deploy Frontend และ Backend คนละ Cloud Platform (Vercel + Railway)
- ปัญหา CORS คืออะไร เกิดขึ้นเมื่อไหร่ และวิธีแก้ด้วย `cors` middleware
- การใช้ `fetch()` เพื่อเรียก API แบบ Asynchronous พร้อมจัดการ Loading และ Error State
- การออกแบบ UI ที่ตอบสนองต่อสถานะต่าง ๆ (Loading, Success, Error)
- การเชื่อมต่อ Frontend เข้ากับ Backend Service ที่มีอยู่แล้วจากโปรเจกต์ก่อนหน้า
- **การเชื่อมระบบ JWT Authentication จาก Backend เข้ากับหน้าเว็บจริง**
- **การใช้ `localStorage` เก็บ Token และจัดการสถานะ Login/Logout**
- **การแนบ Authorization Header (`Bearer <token>`) ไปกับ Request**
- **การออกแบบ UI ให้รองรับทั้งผู้ใช้ที่ Login แล้วและยังไม่ได้ Login (Optional Authentication)**

---

## 🔗 โปรเจกต์ที่เกี่ยวข้อง

- **Backend API:** [myfirstapi](https://github.com/JirawatDonbantao/myfirstapi) — REST API ที่ให้บริการข้อมูลสภาพอากาศ พร้อมระบบ Authentication ด้วย JWT

---

## 🗺️ โปรเจกต์นี้เป็นส่วนหนึ่งของ

คอร์สเรียน **Cloud Computing & DevOps** — เส้นทางสู่การเป็น Cloud/DevOps Engineer

---

*Built with 💻 by [JirawatDonbantao](https://github.com/JirawatDonbantao)*
